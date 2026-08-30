# Proposal: T12 Learner — only cite Core Update as confound if ALGO_WATCH is active
**Proposed:** 2026-08-23T20:30:00+05:30
**Source:** task13-meta-learner-2026-08-23
**Apply on:** 2026-08-30T20:00:00+05:30
**Status:** preview

## Issue detected

In the 2026-08-23 T12 Learner run, W30/W31/W32/W33 Day-21 verdicts all cite "August Core Update (2026-08-26, 3 days away)" as confound for 0 GSC impressions. The August Core Update has NOT started yet — it is 3 days in the future.

All four Jul-28 auto-ship blogs show **zero GSC impressions at Day-21**, which is anomalous relative to prior cohorts (Jun-9 cohort had positive signal by Day-21; W24 showed 1,297 impr/wk at Day-14). Pre-attributing a future event as confound masks a potential real indexation issue and defers what might be a LEARNER FLAG situation.

The correct procedure: a Core Update is only a valid confound if `ALGO_WATCH: active` is in `brain/BRAIN.md`, meaning the update has been confirmed as started/running by a prior task run.

## Proposed change
**File to edit:** `cowork-tasks/task12-learner.md`
**Edit type:** line-edit (append a confound gate after Step 2, item 4)

### Before
```
4. Classify:
   - 🟢 **RECOVERED** — within target range (e.g., expected +15-25% → actual +20%)
   - 🟡 **PARTIAL** — moved ≥50% toward target but didn't hit
   - 🔴 **STALLED** — moved <30% toward target
   - ⚫ **WORSE** — went further from target
```

### After
```
4. Classify:
   - 🟢 **RECOVERED** — within target range (e.g., expected +15-25% → actual +20%)
   - 🟡 **PARTIAL** — moved ≥50% toward target but didn't hit
   - 🔴 **STALLED** — moved <30% toward target
   - ⚫ **WORSE** — went further from target

4b. **External confound guard** — when noting an external confound (Core Update, broad algorithm update, QDF, etc.) as the explanation for a 🔴 or ⚫ verdict:
   - Core Update: only cite as confound if `ALGO_WATCH: active` appears in `brain/BRAIN.md`. A Core Update that is announced but not yet started (launch date in the future) is NOT a valid confound — do not attribute today's 0-impression / stale-rank signal to a future event.
   - QDF (Query Deserves Freshness): only cite if the watch was opened within 6 weeks of the page's publish date AND the rank showed an initial positive QDF window that has since normalized.
   - If no confirmed confound exists and ≥50% of a NEW_indexation cohort shows 0 impressions at Day-21, post `⚠ LEARNER FLAG: cohort indexation gap` to Slack and note it in the weekly digest. Do NOT suppress this into "Core Update pending."
```

## Rationale

Pre-emptive Core Update attribution is a systematic bias risk. It makes 0-impression Day-21 reads look like noise when they may be real indexation failures. The fix is simple: check ALGO_WATCH state before citing any update as confound. This also makes the "⚠ LEARNER FLAG >50% red/worse" rule (already in T12 constraints) trigger correctly on bad cohorts rather than being masked by a future event.

## Risk assessment

Low. This is a procedure note added to the evaluation step — it doesn't change how data is pulled or stored. In the worst case, T12 posts an unnecessary LEARNER FLAG that Kushal reviews and dismisses. Better a false positive flag than a masked real indexation failure.

## Rollback

Snapshot: `brain/before-snapshots/task12-learner-{TIMESTAMP}.bak` (created at apply time)
To rollback: restore snapshot to `cowork-tasks/task12-learner.md`.
