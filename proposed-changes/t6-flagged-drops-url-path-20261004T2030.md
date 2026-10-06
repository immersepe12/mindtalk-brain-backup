# Proposal: T6 must include url_path when writing to flagged-drops.json

**Proposed:** 2026-10-04T20:30:00+05:30
**Source:** task13-meta-learner-2026-10-04
**Apply on:** 2026-10-11T20:00:00+05:30
**Status:** preview

## Issue detected

Category: **Wasted work / cross-task inconsistency (1a + 1b)**

`brain/BRAIN.md` (line matching "T6 appends flagged-drops rows") explicitly states:
> "T6 appends flagged-drops rows without `url_path` (747 unvalidatable) — T13 spec fix needed."

Inspecting `flagged-drops.json` (2026-09-28 entries), T6 writes this format:
```json
{
  "query": "therapist near me",
  "impressions": 1434,
  "position_now": 53.2,
  "position_prev": 39.5,
  "position_delta": 13.7,
  "source": "task6-weekly-report",
  "date": "2026-09-28"
}
```

But Task 2 (`task2-gsc-validator.md`) requires `url_path` in each entry to run GSC validation:
> (task2-gsc-validator.md line 61 example shows: `"url_path": "/illnesses/depression"`)

T2 reads `url_path` to know which page to pull from GSC. Without it, T2 silently skips every T6 row — the drop signal is fully wasted. T6 has fired weekly for months; the 747-row count confirms this has been a persistent data sink.

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task6-weekly-report.md`
**Edit type:** line-edit

### Before
```
### Step 5 — Flag drops for refresh
Review dropping queries and clusters. If any keyword dropped 5+ positions:
- Add to ~/Seo-workflow-mindtalk/mindtalk-setup/flagged-drops.json so Task 2 picks it up
```

### After
```
### Step 5 — Flag drops for refresh
Review dropping queries and clusters. If any keyword dropped 5+ positions:
- Look up the URL path for each flagged query in `keyword-map.json` (find the entry whose `primary_keyword` matches the query, and read its top-level URL path key). If no matching entry exists in keyword-map.json, **skip** — do not add unmappable queries (T2 can do nothing with query-only rows).
- Add to `~/Seo-workflow-mindtalk/mindtalk-setup/flagged-drops.json` with ALL required fields:
  ```json
  {
    "url_path": "/path/to/page",
    "query": "the keyword that dropped",
    "impressions": N,
    "position_now": N.N,
    "position_prev": N.N,
    "position_delta": N.N,
    "source": "task6-weekly-report",
    "date": "{TODAY}"
  }
  ```
  **REQUIRED: `url_path` must be present.** Task 2 uses `url_path` to pull GSC data; entries without it are silently skipped, wasting the drop signal entirely (confirmed: 747 unvalidatable rows as of 2026-10-04 BRAIN.md note).
```

## Rationale

Without `url_path`, every T6 drop signal is a no-op in T2. T6 already flags the right queries (correct signal selection) — the gap is only the format. Fixing this lets T2 validate T6's weekly drops and route confirmed ones into recovery briefs, closing the signal loop. The fix is pure spec clarification with no risk of false positives.

## Risk assessment

Low risk. `keyword-map.json` already maps queries to URL paths. The only failure mode is if a flagged query has no mapping — the spec handles that with "skip unmappable entries", so the only cost is a smaller flagged-drops batch, not a false signal.

## Rollback

Copy `brain/before-snapshots/task6-weekly-report-20261011T2000.bak` back to `cowork-tasks/task6-weekly-report.md`. The current flagged-drops.json entries are unaffected (they're data, not config); T2 will simply continue skipping them.

## Veto instructions
To veto: rename this file from `t6-flagged-drops-url-path-20261004T2030.md` → `t6-flagged-drops-url-path-20261004T2030.vetoed.md` and add a `## Veto reason` section.
To approve early: rename → `t6-flagged-drops-url-path-20261004T2030.approved.md` — Strategist's next 8 PM run will apply it.
If neither, auto-applies on 2026-10-11.
