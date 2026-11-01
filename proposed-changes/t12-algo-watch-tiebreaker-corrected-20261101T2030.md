# Proposal: T12 — Formalize ALGO_WATCH dual-sensor tiebreaker rule (corrected Before block)

**Proposed:** 2026-11-01T20:30:00+05:30
**Source:** META-LEARNER T13 weekly run 2026-11-01T2030
**Apply on:** 2026-11-08T20:00:00+05:30
**Status:** preview
**Supersedes:** t12-algo-watch-dual-sensor-tiebreaker-20261018T2030 (vetoed 2026-11-01 by T13 — Before block was wrong for 8 MISMATCH-SKIPs)

## Issue detected

The original proposal `t12-algo-watch-dual-sensor-tiebreaker-20261018T2030.md` accumulated
8 consecutive MISMATCH-SKIPs (2026-10-25 through 2026-11-01) because its "Before" block
targeted `#### Step 4b — Core update detection` — a heading that does not exist in
`task12-learner.md`. The actual Step 4b uses a numbered bullet format: `4b. **External
confound guard**`. T13 has vetoed the stuck proposal and re-files with the correct
Before block.

The underlying change is still needed: the dual-sensor tiebreaker rule (when T2 and T12
disagree on ALGO_WATCH status, T12 GSC pattern analysis takes precedence) lives only in
BRAIN.md prose (added 2026-09-28). It is not codified in the operational spec where T12
runs will reliably read it.

**Evidence:**
- `brain/memory/applied-history.md` shows 8 MISMATCH-SKIP entries for the stuck proposal
- `brain/BRAIN.md` 2026-09-28 entry: "Lesson: two sensor sources can give contradictory
  algo-watch verdicts … T12 pattern analysis takes precedence"
- `brain/BACKLOG.md` (2026-10-31): STALE-ALERT logged for original proposal

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task12-learner.md`

**Edit type:** line-edit (append dual-sensor tiebreaker paragraph to end of Step 4b bullet list)

### Before

```
4b. **External confound guard** — when noting an external confound (Core Update, broad algorithm update, QDF, etc.) as the explanation for a 🔴 or ⚫ verdict:
   - Core Update: only cite as confound if `ALGO_WATCH: active` appears in `brain/BRAIN.md`. A Core Update that is announced but not yet started (launch date in the future) is NOT a valid confound — do not attribute today's 0-impression / stale-rank signal to a future event.
   - QDF (Query Deserves Freshness): only cite if the watch was opened within 6 weeks of the page's publish date AND the rank showed an initial positive QDF window that has since normalized.
   - If no confirmed confound exists and ≥50% of a NEW_indexation cohort shows 0 impressions at Day-21, post `⚠ LEARNER FLAG: cohort indexation gap` to Slack and note it in the weekly digest. Do NOT suppress this into "Core Update pending."
```

### After

```
4b. **External confound guard** — when noting an external confound (Core Update, broad algorithm update, QDF, etc.) as the explanation for a 🔴 or ⚫ verdict:
   - Core Update: only cite as confound if `ALGO_WATCH: active` appears in `brain/BRAIN.md`. A Core Update that is announced but not yet started (launch date in the future) is NOT a valid confound — do not attribute today's 0-impression / stale-rank signal to a future event.
   - QDF (Query Deserves Freshness): only cite if the watch was opened within 6 weeks of the page's publish date AND the rank showed an initial positive QDF window that has since normalized.
   - If no confirmed confound exists and ≥50% of a NEW_indexation cohort shows 0 impressions at Day-21, post `⚠ LEARNER FLAG: cohort indexation gap` to Slack and note it in the weekly digest. Do NOT suppress this into "Core Update pending."
   - **Dual-sensor tiebreaker rule (mandatory):** When T2 rank-surveillance reports ALGO_WATCH NOT ACTIVE in its Slack digest but THIS step's GSC pattern analysis shows continued broad ranking volatility (≥3 clusters with unexplained movement, or YMYL queries still oscillating), THIS STEP'S pattern analysis takes precedence. Do NOT write `ALGO_WATCH: cleared` to BRAIN.md solely on the basis of a T2 Slack signal. Only clear ALGO_WATCH when BOTH sensors agree: (1) T2 reports stable, AND (2) this step's GSC pattern analysis shows <2 clusters with unexplained movement. Log any conflict explicitly: `T12 SENSOR CONFLICT: T2=not-active, T12=active — maintaining ALGO_WATCH per dual-sensor rule.`
```

## Rationale

The BOTH-sensors-agree requirement prevents premature ALGO_WATCH clears (the dangerous
failure mode — YMYL restrictions released while volatility persists). Without this rule
codified in task12-learner.md, any T12 run in a new Claude session without full BRAIN.md
context could miss the lesson and clear ALGO_WATCH on T2's signal alone.

The change is a pure spec addition — no production code touched.

## Risk assessment

Low. Worst case: T12 keeps ALGO_WATCH active one extra week if sensors genuinely conflict
(conservative safe outcome — YMYL restrictions remain). The opposite error (premature clear)
is the dangerous one; this proposal prevents it. The ≥3 cluster threshold is consistent with
the original proposal's intent and can be tuned in a follow-up proposal.

## Rollback

Remove the `Dual-sensor tiebreaker rule` bullet from Step 4b. T12 reverts to single-sensor
(T12 GSC pattern only) for ALGO_WATCH decisions — no worse than pre-proposal state.

## Veto instructions

To veto: rename to `t12-algo-watch-tiebreaker-corrected-20261101T2030.vetoed.md`.
To approve early: rename to `t12-algo-watch-tiebreaker-corrected-20261101T2030.approved.md`.
