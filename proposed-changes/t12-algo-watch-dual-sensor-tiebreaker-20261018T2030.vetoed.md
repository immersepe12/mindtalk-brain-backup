# Proposal: T12 — Formalize ALGO_WATCH dual-sensor tiebreaker rule in task spec

**Proposed:** 2026-10-18T20:30:00+05:30
**Source:** META-LEARNER T13 weekly run 2026-10-18T2030
**Apply on:** 2026-10-25T20:00:00+05:30
**Status:** preview

## Issue detected

On 2026-09-28 the Strategist added a lesson to BRAIN.md prose:

> "Lesson: two sensor sources can give contradictory algo-watch verdicts. T2 sensor
> reported ALGO_WATCH NOT ACTIVE while T12 GSC pattern analysis showed ACTIVE posture.
> Resolution: T12 pattern analysis takes precedence; never relax YMYL restrictions
> based on T2 single-sensor signal alone."

This rule lives only in BRAIN.md prose. It is NOT codified in task12-learner.md Step 4b
(the ALGO_WATCH core update detection logic). T2 and T12 can still produce conflicting
verdicts on any future run, and a future T12 run could clear ALGO_WATCH based on T2's
signal while GSC patterns still show volatility. That would re-enable YMYL content
prematurely. ALGO_WATCH persisted 3+ extra weeks (confirmed in BRAIN.md 2026-10-18
entry: ALGO_WATCH CLEARED ✅ only now) partly because the conflict resolution was
undocumented in the operational spec.

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task12-learner.md`

**Edit type:** line-edit (append tiebreaker paragraph to Step 4b)

### Before

```markdown
#### Step 4b — Core update detection
Core Update: only cite as confound if `ALGO_WATCH: active` appears in `brain/BRAIN.md`.
```

### After

```markdown
#### Step 4b — Core update detection
Core Update: only cite as confound if `ALGO_WATCH: active` appears in `brain/BRAIN.md`.

**Dual-sensor tiebreaker rule (mandatory):** When T2 rank-surveillance reports ALGO_WATCH
NOT ACTIVE in its Slack digest but T12 GSC pattern analysis (this step) shows continued
broad ranking volatility (≥3 clusters with unexplained movement, or YMYL queries still
oscillating), T12's pattern analysis takes precedence. Do NOT write `ALGO_WATCH: cleared`
to BRAIN.md solely on the basis of a T2 Slack signal. Only clear ALGO_WATCH when BOTH
sensors agree: (1) T2 reports stable, AND (2) T12 pattern analysis shows <2 clusters
with unexplained movement. Log the conflict explicitly:
`T12 SENSOR CONFLICT: T2=not-active, T12=active — maintaining ALGO_WATCH per dual-sensor rule.`
```

## Rationale

The lesson from 2026-09-28 (Strategist decision log) demonstrates this conflict is
real and repeatable. Formalizing the rule in the T12 spec ensures any future T12 run
— even in a new Claude session without recent BRAIN.md context — applies the correct
tiebreaker. Without this, the rule only exists in BRAIN.md prose, which may not be
read on every T12 run.

The BOTH-sensors-agree requirement prevents false clears while keeping clear-path
simple: when both sensors say not-active, T12 clears normally.

## Risk assessment

Low. This is a config/spec edit only. No scripts or production code touched. The
worst case: T12 maintains ALGO_WATCH one extra week if sensors are genuinely
conflicted — that is the conservative safe outcome (YMYL restrictions stay on).
The opposite error (premature clear) is the dangerous one; this proposal prevents it.

## Rollback

Remove the "Dual-sensor tiebreaker rule" paragraph from task12-learner.md Step 4b.
T12 reverts to single-sensor (T12 GSC pattern alone) for ALGO_WATCH decisions —
no worse than current state, since T2 signal was never formally consulted anyway.

## Veto instructions

If you believe the ≥3 cluster threshold is too high or too low, or the BOTH-agree
requirement is too conservative, rename this file to
`t12-algo-watch-dual-sensor-tiebreaker-20261018T2030.vetoed-by-verifier.md` with
a threshold suggestion. The Strategist will not apply until revised.
