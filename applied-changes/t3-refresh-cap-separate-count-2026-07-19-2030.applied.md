# Proposal: T3 Step 1 — Count only REFRESH briefs against T3 cap (not T5 new-content briefs)
**Proposed:** 2026-07-19T20:30:00+05:30
**Source:** task13-meta-learner-2026-07-19
**Apply on:** 2026-07-26T20:00:00+05:30
**Status:** preview

## Issue detected

**Log evidence:** `logs/briefs-2026-07-13.txt` header reads `"Weekly total: 6/10"` — T3 counted 1 T3 refresh brief + 5 T5 new-content briefs against a combined denominator of "10". The correct count is 1/20 for T3 refreshes.

**Root cause:** T3 Step 1's tracking-db check queries `status = BRIEF_CREATED with date this week` with no source/type filter. T5 new-content briefs also land with `status: BRIEF_CREATED` in the same week. T3 counts them all, producing inflated combined counts and a stale "10" denominator. The cap note at line 37 says "NEW content has its own 20/week cap — see Task 5" but does NOT tell the agent to exclude those entries from the T3 count query.

**Hardening verification 2026-07-17:** FAIL #1 — "T3 ran at 6/10 quotas" (wrong denominator confirms the filter is missing).

**Note:** Prior applied fix `cap-mismatch-task3-log-template` (applied 2026-06-28) only corrected the log *template* line (X/10 → X/20). It did NOT add the source-filter logic to Step 1's tracking-db query. This proposal fixes the underlying query, not just the display.

## Proposed change
**File to edit:** `cowork-tasks/task3-serp-analysis-briefs.md`
**Edit type:** line-edit (Step 1 tracking-db check block — lines 33–37)

### Before
```
Check `~/Seo-workflow-mindtalk/mindtalk-setup/tracking-db.json` to see how many URLs were already processed 
into briefs this week (status = BRIEF_CREATED with date this week).
Maximum 20 per week total. If already at 20, log "Weekly limit reached" and stop.

> **Cap:** 20 refresh briefs per week (config.json `max_urls_per_week=20`). NEW content has its own 20/week cap — see Task 5.
```

### After
```
Check `~/Seo-workflow-mindtalk/mindtalk-setup/tracking-db.json` to see how many **refresh** briefs were already processed this week. Count only entries where ALL of the following are true:
- `status == "BRIEF_CREATED"`
- `brief_created_at` is within the current week (Mon–Sun)
- `type == "REFRESH"` OR `brief_path` starts with `"briefs/REFRESH-"` OR `brief_path` starts with `"briefs/"` but does NOT start with `"briefs/NEW-"`

**Do NOT count T5 new-content briefs** (entries with `type: "NEW_CONTENT"` or `brief_path` starting with `"briefs/NEW-"`). Those have their own separate 20/week cap tracked by Task 5.

Maximum 20 REFRESH briefs per week (config.json `max_urls_per_week=20`). If already at 20, log "Weekly limit reached (20/20 refresh briefs)" and stop.

Log the count as: `Refresh briefs this week: [N]/20`

> **Cap:** 20 refresh briefs per week (config.json `max_urls_per_week=20`). NEW content briefs have their own separate 20/week cap — see Task 5. Never combine the two counts.
```

## Rationale

The prior fix (2026-06-28) corrected the display string but not the count logic. T3 continued counting T5 briefs against its own cap, producing false "limit reached" signals and causing T3 to under-process confirmed-drop URLs. Separating the count by type ensures T3 always operates against its own true cap, independent of T5 activity.

## Risk assessment

Low. This is a read-only filter change — it can only increase the number of T3 briefs T3 creates (no longer falsely blocked by T5 counts). The worst case is T3 creates more refresh briefs than expected in a week where T5 is also very active, but the T3 cap of 20 still holds.

## Rollback

The "Before" block above contains the original text. To revert: replace the new Step 1 tracking-db check block with the Before text above. Rollback snapshot: `brain/proposed-changes/t3-refresh-cap-separate-count-2026-07-19-2030.md` (this file).
