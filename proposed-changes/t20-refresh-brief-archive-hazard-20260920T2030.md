# Proposal: T20 stale-brief auto-fix must exempt REFRESH- briefs from "slug 200 → archive" sweep
**Proposed:** 2026-09-20T20:30:00+05:30
**Source:** task13-meta-learner-2026-09-20
**Apply on:** 2026-09-27T20:00:00+05:30
**Status:** preview

## Issue detected

T20's REMEDIATION REGISTRY auto-fix for **Stale briefs** reads:

> "Verify each: 200 = shipped, move to `briefs/archive/`"

REFRESH briefs (filenames starting with `REFRESH-`) target pages that are **already live** — the slug is 200 by design. The rule incorrectly archives them as if they were shipped new content.

**Evidence:** T20 2026-09-17 run (BRAIN.md): "`guide-to-reset-your-sleep-cycle` and `psychology-of-love` were NOT archived despite live 200 slugs — both are REFRESH briefs, and the naive 'slug 200 → archive-as-shipped' sweep would have destroyed them. REFRESH-BRIEF-IN-NEW-QUEUE-01 honoured; the rule must read 'slug 200 AND NEW- brief'." T20 had to manually add this exception on 09-17 AND 09-18 — it is not yet codified in the task spec. The next T20 run without this guard will incorrectly archive any REFRESH brief whose target page is live.

**Recurring:** flagged on 09-17, re-honoured manually on 09-18, filed to T13 explicitly. No proposal exists yet.

## Proposed change
**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task20-auto-remediation.md`
**Edit type:** line-edit

### Before
```
| **Stale briefs** (already-live slugs OR no `intent_tier` in queue) | Verify each: 200 = shipped, move to `briefs/archive/`; no `intent_tier` = move to `briefs/archive/`. Never delete. |
```

### After
```
| **Stale briefs** (already-live slugs OR no `intent_tier` in queue) | Verify each: brief filename starts with `NEW-` AND slug returns 200 = shipped, move to `briefs/archive/`; brief filename starts with `REFRESH-` AND slug returns 200 = **DO NOT ARCHIVE** (the page is live by design — the brief is pending a content update); no `intent_tier` = move to `briefs/archive/`. Never delete. |
```

## Rationale

REFRESH briefs exist precisely because the target URL is already live. Archiving them on "slug 200" destroys pending refresh work without executing it. The guard added in the "After" makes the sweep brief-type-aware. The only cost is a filename prefix check before each archive decision — zero risk of false positives because `NEW-` and `REFRESH-` are the two exclusive prefixes in the brief queue.

## Risk assessment

Low. The change narrows what gets auto-archived, never widening it. A REFRESH brief that somehow ends up with a 200 slug that shouldn't exist will be missed — but T20 will still flag it via "Stale briefs" on the next run, and T20 never deletes, only archives.

## Rollback

Copy `brain/before-snapshots/task20-auto-remediation-20260920T2030.bak` back to `cowork-tasks/task20-auto-remediation.md`.

## Veto instructions
To veto: rename this file to `t20-refresh-brief-archive-hazard-20260920T2030.vetoed.md` and add a `## Veto reason` section.
To approve early: rename to `t20-refresh-brief-archive-hazard-20260920T2030.approved.md`.
