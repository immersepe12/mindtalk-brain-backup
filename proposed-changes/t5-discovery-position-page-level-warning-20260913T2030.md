# Proposal: task5 — add warning that discovery avg_position is page-level, NOT query-level
**Proposed:** 2026-09-13T20:30:00+05:30
**Source:** task13-meta-learner-2026-09-13
**Apply on:** 2026-09-20T20:30:00+05:30
**Status:** preview

## Issue detected

T20 Auto-Remediation (2026-09-12) established Standing Rule (f): *"a query's position/impressions must come from `dimensions=[query]`. The stock discovery script's `avg_position` is a naive per-page mean across every site URL on the SERP (reported pos 41.6 for a query the site holds at 4.7; inflated demand up to 6×). Every T5 brief inherits this → DISCOVERY-AVG-POSITION-IS-NOT-QUERY-POSITION-01 filed to T13."*

Rule (g): *"Never close a query-level alert with page rows or a 2-window comparison."*

Currently `task5-new-content-discovery.md` has no warning about this. T5 reads the discovery script output and uses `avg_position` values to rank content opportunities and populate briefs with estimated competitive difficulty. If T5 treats a page-level avg_position of 41.6 as the query-level position, it will:
1. Over-estimate opportunity size (site appears to rank at 41.6 when it actually holds the query at pos 4.7)
2. Generate briefs for URLs the site already dominates at query level — wasting brief capacity
3. Set incorrect baseline_position values in briefs, causing T12 watches to open with wrong expectations

This was the root cause of the "SYSTEM-UNDERUTILISED W33-W34" finding (T9 doctor-listing-backlog-escalation): demand was systematically over-estimated using page-level position, and the wrong briefs were prioritised.

**Evidence:**
- `brain/BRAIN.md` 2026-09-12 T20: *"Rule (f): a query's position must come from `dimensions=[query]`. discovery script's avg_position is a naive per-page mean... inflated demand up to 6×. Every T5 brief inherits this → DISCOVERY-AVG-POSITION-IS-NOT-QUERY-POSITION-01 filed to T13."*
- `brain/BRAIN.md` 2026-09-12 T20: *"Rule (g): never close a query-level alert with page rows or a 2-window comparison."*
- `brain/applied-changes/t9-doctor-listing-backlog-escalation-20260816T2030.applied.md`: root cause of underutilisation was brief queue fed with wrong-priority content.
- Verifier sub-agent confirmation 2026-09-12: "query claims need `dimensions=[query]`; discovery's per-page position mean is not a query position."

## Proposed change
**File to edit:** `cowork-tasks/task5-new-content-discovery.md`
**Edit type:** append (add after Step 1 discovery script section)

### Before
*(No position-integrity warning exists in the file. The section after Step 1 immediately proceeds to brief ranking logic.)*

### After
*(Insert the following block immediately after the Step 1 bash command block and before Step 2:)*

```
> ⚠️ **POSITION DATA INTEGRITY WARNING (Rule f/g — 2026-09-12)**
> The discovery script's `avg_position` output is a **page-level mean** across every URL on the SERP,
> NOT a query-level position. It is inflated by up to 6× (example: page-level mean = 41.6 for a query
> the site actually holds at pos 4.7 via `dimensions=[query]`).
>
> **NEVER use `avg_position` from discovery output as a proxy for how the site ranks on a specific query.**
> Before generating a brief that relies on a position estimate, verify with GSC query-dimension pull
> (`dimensions=["query"]`, not `["page"]`). If GSC query data is unavailable, note in the brief:
> `baseline_position: UNVERIFIED (page-level estimate only)` and flag for T12 watch recalibration.
>
> Similarly, NEVER close a query-level rank alert using page-row data or a 2-window comparison alone
> (Rule g). Query-level position is the authoritative signal.
```

## Rationale

Makes the known position-data caveat explicit in the task spec that generates briefs. Every future T5 run will read this warning before ranking opportunities. Prevents recurrence of inflated-demand prioritisation that wasted brief capacity in W33-W34 and caused misaligned T12 watch baselines.

## Risk assessment

Low — append only, no existing content removed. The warning is advisory; it adds a verification step to brief generation but does not block any action. The only risk is that T5 over-checks GSC, which is a minor efficiency cost (one GSC call per brief for top candidates) vs. the cost of wrong-priority brief queues.

## Rollback

Remove the inserted warning block from `cowork-tasks/task5-new-content-discovery.md`. Git history is the rollback source. No snapshot file required.
