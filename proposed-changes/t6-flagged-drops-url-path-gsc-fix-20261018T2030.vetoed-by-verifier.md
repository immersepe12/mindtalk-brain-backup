# Proposal: T6 — Fix flagged-drops url_path via GSC page dimension (re-proposal)

**Proposed:** 2026-10-18T20:30:00+05:30
**Source:** META-LEARNER T13 weekly run 2026-10-18T2030
**Apply on:** 2026-10-25T20:00:00+05:30
**Status:** preview

## Issue detected

Original proposal `t6-flagged-drops-url-path-20261004T1900` was vetoed because it
resolved url_path via `keyword-map.json`, which only matches ~5 queries of the 1,577
rows T6 writes to flagged-drops.json. The veto note confirmed the issue is real but
the resolution method was wrong.

T2 (rank surveillance) currently silently skips ALL flagged-drops.json entries that
lack a `url_path` field. T6 Step 5 never writes url_path. This means every keyword
T6 flags for refresh is silently dropped by T2, making the refresh loop entirely
non-functional. 1,577 wasted rows confirmed in vetoed proposal notes.

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task6-weekly-report.md`

**Edit type:** sed-replace (replace Step 5 flag-writing block)

### Before

```markdown
### Step 5 — Flag drops for refresh
Review dropping queries and clusters. If any keyword dropped 5+ positions:
- Add to ~/Seo-workflow-mindtalk/mindtalk-setup/flagged-drops.json so Task 2 picks it up
```

### After

```markdown
### Step 5 — Flag drops for refresh

Review dropping queries and clusters. If any keyword dropped 5+ positions:

1. For each dropped keyword, resolve its canonical URL via the GSC page dimension:
   ```python
   from searchconsole import query
   # Same GSC client T2 already uses
   page_rows = query(
       site="https://mindtalk.in",
       dimensions=["page", "query"],
       filters=[{"dimension": "query", "operator": "equals", "expression": kw}],
       date_range=("last_28_days")
   )
   url_path = page_rows[0]["page"] if page_rows else None
   ```

2. Only write entries where url_path was resolved. Skip (and log) any keyword where
   GSC returns zero page rows — do NOT write url_path-less entries:
   ```python
   entry = {
       "keyword": kw,
       "url_path": url_path,        # ← required by T2; skip if None
       "drop_positions": drop,
       "flagged_by": "T6",
       "flagged_at": today_iso
   }
   ```

3. Append resolved entries to
   `~/Seo-workflow-mindtalk/mindtalk-setup/flagged-drops.json`
   so Task 2 picks them up.

4. Log count: `T6 Step 5: flagged {N} keywords ({M} skipped — no GSC page match)`.
```

## Rationale

T2 already uses the GSC page dimension API in its own Step 1 to map queries to URLs.
Using the same GSC endpoint in T6 Step 5 ensures url_path matches exactly what T2
expects. The original vetoed fix used keyword-map.json (a static file covering only
~5 queries). GSC page dimension is dynamic and covers the full crawled URL set.

Evidence: vetoed proposal `t6-flagged-drops-url-path-20261004T1900.vetoed-by-verifier.md`
confirmed issue is real; veto reason was method only, not the fix itself.

## Risk assessment

Medium. The GSC API call adds ~3 seconds per keyword. T6 runs weekly so latency is not
a concern. Edge case: GSC returns multiple pages for one query — take the highest-click
page (page_rows sorted by clicks desc). If GSC client auth fails, log and skip Step 5
entirely (don't write partial entries); Strategist will see the skip in the weekly log.

## Rollback

Revert task6-weekly-report.md Step 5 to the single-line version. T6 reverts to writing
url_path-less entries (T2 silently skips them, same as today — no regression vs. current).

## Veto instructions

If you believe a different url_path resolution method is better, rename this file to
`t6-flagged-drops-url-path-gsc-fix-20261018T2030.vetoed-by-verifier.md` with a note.
The Strategist will not apply it.
