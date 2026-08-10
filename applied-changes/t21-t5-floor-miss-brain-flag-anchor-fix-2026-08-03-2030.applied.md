# Proposal: T5 Step 7 — Re-file BRAIN.md floor-miss flag with corrected Before anchor (MISMATCH-SKIP recovery)
**Proposed:** 2026-08-03T20:30:00+05:30
**Source:** task13-meta-learner-2026-08-03
**Apply on:** 2026-08-10T20:00:00+05:30
**Status:** preview

## Issue detected

**Original proposal:** `brain/proposed-changes/t5-floor-miss-brain-flag-2026-07-26-2030.md`
- Filed 2026-07-26. Apply date 2026-08-02. Passed the 7-day window.
- Strategist 2026-08-03 applied it as **MISMATCH-SKIP**: the Before block in the proposal (`- NEVER write \`5/5 quota\` or any \`N/5\` denominator...`) no longer exists in `task5-new-content-discovery.md` — it was replaced by the `t5-floor-12-output-enforcement` proposal (applied 2026-07-20, Kushal-directed early apply) with a REGRESSION HISTORY block and the INTENT/REDUNDANCY GATE. BRAIN.md stamp 2026-08-03: *"t5 ⚠️ MISMATCH-SKIP (Before-block 'NEVER write 5/5 quota' superseded by regression-history block from t5-floor-12-output-enforcement — manual anchor fix needed before re-filing)."*
- **Second MISMATCH-SKIP** confirmed on 2026-08-03 second Strategist run (ADDENDUM stamp).

**Why the original change is still needed:**
T5 can miss its 12-brief floor and the only notification path is a Slack post. Slack ERR_FAILED is a recurring pattern (confirmed multiple T11 runs). If T5's floor-miss Slack post also fails, the floor miss becomes invisible — Strategist's next daily run won't know T9 is about to be starved for briefs. BRAIN.md is Strategist's primary input; writing a flag there closes the gap.

Evidence of the cost: T5 missed its floor on 2026-07-20 (4 of 12). T16 brief-runway check (count of BRIEF_CREATED ≥ 15) is a lagging indicator — by the time runway drops below 15, starvation has already started. T5-REFILL-NOW has appeared as a CRITICAL Strategist flag for 4+ consecutive runs (BRAIN.md 2026-08-03 stamp: *"PATTERN NOTE: T5-REFILL-NOW has been a recurring CRITICAL for 4+ consecutive Strategist runs — if T5 does not fire on Mac Mini within 48h, T9 velocity collapses to 0."*).

## Proposed change
**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task5-new-content-discovery.md`
**Edit type:** line-edit (append new BRAIN.md floor-miss flag bullet immediately after the floor-miss Slack description)

### Before
```
- If count < 12 after all tiers exhausted: continue with what you have, but the Step 7 summary MUST include: `⚠️ BRIEF FLOOR MISS: [N] of 12 minimum. Queue exhausted at vol > 200.` and this line must also be included in the Slack post (Step 8).
```

### After
```
- If count < 12 after all tiers exhausted: continue with what you have, but the Step 7 summary MUST include: `⚠️ BRIEF FLOOR MISS: [N] of 12 minimum. Queue exhausted at vol > 200.` and this line must also be included in the Slack post (Step 8).
- **BRAIN.md floor-miss flag (Slack-independent):** If briefs created this run is < 12, append the following line to `brain/BRAIN.md` (prepend before all existing content so Strategist sees it on the very next read):
  ```
  ⚠️ T5 FLOOR MISS {TODAY}: {N}/12 briefs created. Brief runway depletes in ~{N_WEEKS} weeks at current T9 velocity. T5 run log: logs/new-content-{TODAY}.txt. Trigger live Mac Mini T5 run before T9 next fires.
  ```
  Where `N_WEEKS = current BRIEF_CREATED count in tracking-db ÷ 6` (conservative weekly ship velocity estimate). This write happens AFTER the Slack step (Step 8), regardless of whether Slack delivery succeeded. Strategist's next daily run (Mon–Sat 8 PM) will see this flag in BRAIN.md and can act on it (trigger off-cycle T5 on Mac Mini, or lower discovery threshold temporarily). Do NOT write this flag if briefs this run ≥ 12 (healthy run).
```

## Rationale

T5 floor miss is the leading indicator of T9 brief starvation, but currently only visible through Slack (unreliable) or T5's run log (Strategist does not read `logs/`). Adding a BRAIN.md prepend makes the floor miss visible to Strategist within 24 hours regardless of Slack status. This pattern is already established: the `t11-flag-human-slack-fallback` (applied 2026-07-26) follows the same logic (Slack fail → write to file as fallback). This proposal adds the equivalent fallback for T5.

Context: T5-REFILL-NOW has triggered CRITICAL escalation for 4+ consecutive Strategist runs (BRAIN.md 2026-08-03). The Strategist note is explicit: *"Strategist cannot self-heal this: requires Kushal action."* The BRAIN.md write doesn't fix the root cause (Mac Mini must run T5) but ensures Strategist knows within 24h that the problem exists — rather than discovering it 1-2 weeks later when T9 has already stalled.

## Risk assessment

**Very low.** The only new write is a conditional BRAIN.md prepend when T5 misses the floor — an already-abnormal state. On healthy T5 runs (≥ 12 briefs), no BRAIN.md write occurs. The prepend is additive — it doesn't modify existing BRAIN.md content. Strategist already handles BRAIN.md flags on every daily run.

Edge case: if T5 misses the floor weekly, BRAIN.md accumulates weekly flags. Strategist should clear stale floor-miss flags after acknowledging them. This is manageable — Strategist already edits BRAIN.md on every run.

## Rollback

Remove the `BRAIN.md floor-miss flag (Slack-independent):` bullet from the T5 Step 7 section. Rollback snapshot: `brain/before-snapshots/task5-new-content-discovery-{TIMESTAMP}.bak` (created by Strategist at apply time).

## Veto instructions
To veto: rename this file to `t21-t5-floor-miss-brain-flag-anchor-fix-2026-08-03-2030.vetoed.md` and add a `## Veto reason` section.
To approve early: rename to `t21-t5-floor-miss-brain-flag-anchor-fix-2026-08-03-2030.approved.md`.
If neither, auto-applies 2026-08-10.
