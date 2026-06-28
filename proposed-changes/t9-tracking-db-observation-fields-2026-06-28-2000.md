# Proposal: T9 Step 6 tracking-db template — 4 missing/wrong observation fields

**Proposed:** 2026-06-28T20:00:00+05:30
**Source:** task13-meta-learner-2026-06-28
**Apply on:** 2026-07-05T20:00:00+05:30
**Status:** preview

## Issue detected

Every blog auto-shipped by Task 9 silently falls out of the observation pipeline (Task 4) because T9 Step 6's tracking-db JSON template has 4 field errors.

**Evidence:** BRAIN.md operational notes 2026-06-19:
> "Obs-monitor flagged that 6 NEW pages (anger-management-therapy, codependency-signs-causes-treatment, dbt-skills-modules, people-pleasing-how-to-stop, relationship-problems-signs-causes-solutions, what-is-somatic-therapy) carry `status=PUBLISHED` but have no `url_locked` flag, so the Step-1 filter (requires `url_locked==true`) skips them — their day-21 midpoint (~06-30) will be silently missed. This is the *missing-flag* sibling of the 06-16 *status-dimension* filter fix. Tracking-db edits are outside Strategist write scope → escalated to Kushal as BACKLOG #13."

BACKLOG #13 was manually resolved on 2026-06-22 by setting `url_locked=true` on those 6 URLs. But the **root cause — T9's Step 6 JSON template — was never fixed**, so the next batch of T9 ships will repeat the same silent miss.

**Cross-referencing T9 Step 6 template vs T4 field requirements:**

| Field T4 needs | T4 reads it in | T9 Step 6 writes | Issue |
|---|---|---|---|
| `url_locked: true` | Step 1 filter | ❌ not written | T4 Step 1 skips the URL entirely |
| `published_at` | Step 2 (days since...) | ✅ `published_date` (wrong name) | T4 Step 2 never finds it → day-21 midpoint never fires |
| `observation_window_end` | Step 3 (day-42 final eval) | ✅ `watch_window_end` (wrong name) | T4 Step 3 never finds it → day-42 final eval never fires |
| `week_3_check_done: false` | Step 2 (`== false` check) | ❌ not written | T4 Step 2 filter skips (undefined ≠ false) |

Additionally, T9 writes `watch_window_end: TODAY + 14 days` — the observation window duration is 42 days (config.json `observation_window_days: 42`), not 14.

T9 Step 10 says "the workflow's existing observation pipeline (Task 4 — runs daily at 8 AM) will auto-monitor" — that statement is currently FALSE due to these field bugs.

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task9-auto-ship-new-blogs.md`
**Edit type:** line-edit (Step 6, JSON template block, lines 248–261)

### Before
```
```json
{
  "/blogs/{slug}": {
    "type": "NEW_CONTENT",
    "status": "PUBLISHED",
    "published_date": "{TODAY-ISO}",
    "commit_hash": "{commit-hash}",
    "reviewer": "{reviewer-slug}",
    "category": "{category}",
    "auto_shipped": true,
    "auto_shipped_by_task": 9,
    "watch_window_end": "{TODAY + 14 days}"
  }
}
```
```

### After
```
```json
{
  "/blogs/{slug}": {
    "type": "NEW_CONTENT",
    "status": "PUBLISHED",
    "published_at": "{TODAY-ISO}",
    "commit_hash": "{commit-hash}",
    "reviewer": "{reviewer-slug}",
    "category": "{category}",
    "auto_shipped": true,
    "auto_shipped_by_task": 9,
    "url_locked": true,
    "week_3_check_done": false,
    "observation_window_end": "{TODAY + 42 days}"
  }
}
```
```

**Also update T9 Step 10 text** (the inaccurate claim about 14-day trajectory):

### Before (Step 10 body)
```
For each shipped URL, the workflow's existing observation pipeline (Task 4 — runs daily at 8 AM) will auto-monitor for first GSC pickup (~5-7 days) and 14-day rank trajectory. No separate scheduled task needed.
```

### After (Step 10 body)
```
For each shipped URL, the workflow's existing observation pipeline (Task 4 — runs daily at 8 AM) will auto-monitor via day-21 midpoint check and day-42 final evaluation (config `observation_window_days: 42`). The tracking-db entry above includes all 4 required fields (url_locked, published_at, week_3_check_done, observation_window_end) that T4 Step 1–3 depend on. No separate scheduled task needed.
```

## Rationale

Every new blog T9 ships will silently miss both its day-21 midpoint check and its day-42 final evaluation until this is fixed. The fix is purely additive (adds/renames 4 fields in the JSON template T9 follows when updating tracking-db). No logic changes, no production code, no cap changes. Closes the only structural gap between T9 and T4 that isn't already guarded.

## Risk assessment

Near-zero. This changes an output-template instruction in a task spec (T9 Step 6 JSON block and Step 10 comment). No behavioral code path changed. Worst case: a field name in a future tracking-db entry differs from template — T4 would simply log "No URLs in observation" as it does today, no worse than the current broken state.

The 42-day window is consistent with `config.json observation_window_days: 42`. If that config value changes, T9 Step 6 should also be updated (not a hard-coded risk — the proposal text makes the dependency explicit).

## Rollback

Strategist snapshots to `brain/before-snapshots/task9-auto-ship-new-blogs.md-{TIMESTAMP}.bak` before applying. To revert: copy that snapshot back over `cowork-tasks/task9-auto-ship-new-blogs.md`. All tracking-db entries written before the fix retain the old field names; manually set `url_locked=true` and add `published_at`/`observation_window_end`/`week_3_check_done` for any shipped-but-not-yet-observed URLs (same manual procedure as BACKLOG #13).

## Veto instructions

To veto: rename this file to `t9-tracking-db-observation-fields-2026-06-28-2000.vetoed.md` and add a `## Veto reason` section.
To approve early: rename to `t9-tracking-db-observation-fields-2026-06-28-2000.approved.md`.
