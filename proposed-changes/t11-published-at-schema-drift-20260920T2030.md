# Proposal: T11 executor must write `published_at` alongside `last_refresh_date` to prevent T4 back-fill loops
**Proposed:** 2026-09-20T20:30:00+05:30
**Source:** task13-meta-learner-2026-09-20
**Apply on:** 2026-09-27T20:00:00+05:30
**Status:** preview

## Issue detected

T11 executor Step 9 writes `last_refresh_date` to tracking-db.json when a refresh ships. T4 observation monitor reads `published_at` (the canonical field). T9's spec correctly writes `published_at` for new pages. But refreshed pages end up with `last_refresh_date` only, leaving `published_at` absent.

**Evidence:** T20 2026-09-19 BRAIN.md: "T4 flagged '7 URLs missing published_at, observation windows cannot be tracked' on 09-18 AND 09-19 and nothing had ever fixed it. Cause is schema drift, not missing data: T9 writes `published_on`, T11 writes `last_refresh_date`, T4 reads `published_at` only. Back-filled from each record's own evidenced field, every one commit- and deploy-confirmed: 4 × 09-16 blogs + therapists-in-bangalore/delhi 09-18 (`1c09372`)." T20 spent time on 09-19 manually back-filling 6 tracking-db records because T11 had never written `published_at`. This is recurring mechanical work that should be prevented at the source.

**Recurring:** T4 raised this flag on both 09-18 and 09-19 — two consecutive days. The 09-19 T20 run fixed the 09-18 and 09-16 cohort only; any T11 run that ships without this fix will re-create the same missing-field condition.

## Proposed change
**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task11-executor.md`
**Edit type:** line-edit

### Before
```
9. Update `tracking-db.json`: status → `PUBLISHED`, `last_refresh_date` → today
```

### After
```
9. Update `tracking-db.json`: status → `PUBLISHED`, `last_refresh_date` → today (ISO-8601), `published_at` → today (ISO-8601, same value — required by T4 observation monitor; without this field T4 cannot track the observation window and will flag missing-published_at on every daily run)
```

## Rationale

T4's observation monitor requires `published_at` to compute day-21 midpoints and day-42 finals. When T11 ships a refresh without writing this field, T4 flags it daily until T20 manually back-fills it. Adding `published_at` to T11's Step 9 instruction prevents the entire feedback loop at zero cost — it's the same date value as `last_refresh_date`.

## Risk assessment

Very low. Writing an extra field to a JSON record that T4 depends on only adds information. Existing records that were already back-filled on 09-19 will not be affected (their `published_at` is already present). The only risk is an LLM accidentally using the wrong date; the instruction makes clear it is the same ISO-8601 value as `last_refresh_date`.

## Rollback

Copy `brain/before-snapshots/task11-executor-20260920T2030.bak` back to `cowork-tasks/task11-executor.md`. Then T20 will resume back-filling `published_at` on subsequent T4 flags — no data is lost.

## Veto instructions
To veto: rename to `t11-published-at-schema-drift-20260920T2030.vetoed.md` and add a `## Veto reason` section.
To approve early: rename to `t11-published-at-schema-drift-20260920T2030.approved.md`.
