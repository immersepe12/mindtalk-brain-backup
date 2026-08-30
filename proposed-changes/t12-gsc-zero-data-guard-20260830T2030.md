# Proposal: T12 Learner — guard against all-zero GSC cohort before recording verdicts
**Proposed:** 2026-08-30T20:30:00+05:30
**Source:** task13-meta-learner-2026-08-30
**Apply on:** 2026-09-06T20:00:00+05:30
**Status:** preview

## Issue detected

T20 Auto-Remediation (2026-08-23) confirmed that T12's Sunday run issued five 🔴 STALLED verdicts (W30/W31/W32/W33/W39) entirely based on GSC data files containing `keywords: []` and 0 impressions across all five URLs. Root cause: `scripts/gsc-pull.py` was called with a full URL (`--url https://mindtalk.in/blogs/...`) instead of a path, causing the script (line 80) to build `full_url = PAGE_URL_BASE + url_path` → `https://www.mindtalk.inhttps://mindtalk.in/...`, which matched zero GSC rows.

The T12 spec has no guard: Step 2 goes directly from "Pull fresh rank data" to "Classify." A cohort where ALL watches return 0 impressions is statistically implausible for pages that rank page-1 — but the spec has no check for this and T12 proceeded to record verdicts, update BRAIN.md with a false "broad pre-Core-Update stall" narrative, and post a Slack digest — all based on measurement artifacts.

Evidence: T20 verified that the same 5 pages have 4,584 total impressions and 20 clicks in the same window when pulled correctly (path form). One URL (`/blogs/how-to-fix-your-sleep-schedule-quickly`) holds position 1.8. T12 recorded it as 0 impressions.

## Proposed change
**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task12-learner.md`
**Edit type:** line-edit (insert new step 1b between steps 1 and 2 of the watch evaluation loop)

### Before
```
1. Pull fresh rank data for the watched URL/query
2. Compare to baseline (the URL state at watch open)
3. Compute delta: position change, impressions change, clicks change, CTR change
4. Classify:
```

### After
```
1. Pull fresh rank data for the watched URL/query

1b. **Zero-data guard** — before proceeding, inspect the raw GSC file for this URL:
   - If the file contains `"keywords": []` or total impressions = 0 across all queries, DO NOT classify yet.
   - Cross-check by pulling the same URL using path form (e.g., `/blogs/my-page`) if the original pull used a full URL — `scripts/gsc-pull.py` builds `full_url = PAGE_URL_BASE + url_path` (line 80), so passing a full URL produces a double-prefix that returns zero rows.
   - If ALL watches in the current evaluation batch show 0 impressions, treat the entire batch as a **measurement error** and post `⚠ LEARNER WARNING: zero-impression cohort — possible GSC pull format bug` to Slack before recording any verdicts. Do NOT write 🔴 STALLED or ⚫ WORSE verdicts based on zero-impression data.
   - If ≥1 watch in the batch has non-zero impressions, proceed normally for those; flag only the zero-impression watches as `pending_evaluation (data error)`.

2. Compare to baseline (the URL state at watch open)
3. Compute delta: position change, impressions change, clicks change, CTR change
4. Classify:
```

## Rationale
Five corrupted verdicts propagated false negatives into BRAIN.md, created a false "broad stall" narrative, and caused T10 to treat 5 page-1 posts as stalled when they were performing normally. The guard is cheap (inspect raw file before classify) and directly targets the only known failure mode — a GSC pull returning zero rows. The batch-level check (all-zero = measurement error) is a strong signal that's computationally trivial to implement.

## Risk assessment
Low. The guard adds a pre-classify check that only fires on zero-impression data. For normal runs (all watches have data), step 1b is a pass-through. False positive risk: a genuinely deindexed URL could look like a zero-impression measurement error — but the guard only blocks classification if the entire cohort is zero, which is nearly impossible for a genuinely mixed cohort unless there's a systematic bug.

## Rollback
Snapshot target file before apply: `brain/before-snapshots/task12-learner-20260906T200000.bak`
Remove the `1b. **Zero-data guard**` paragraph to revert.
