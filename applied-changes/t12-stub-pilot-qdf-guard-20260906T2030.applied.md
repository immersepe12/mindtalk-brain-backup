# Proposal: T12 Learner — add QDF_RISK_INTERIM guard for stub-pilot Day-14 verdicts
**Proposed:** 2026-09-06T20:30:00+05:30
**Source:** task13-meta-learner-2026-09-06
**Apply on:** 2026-09-13T20:30:00+05:30
**Status:** preview

## Issue detected

T12 closed watch W24 (`/mindful-minutes/4-7-8-breathing`) as 🟢 EXCEPTIONAL at Day-14 (interim, 2026-08-09) with position 2.5. At Day-42 (2026-09-04/05) the same page returned position 36.2 — a QDF false positive that misled the engine for 4 weeks. The BRAIN.md (2026-09-06 T12 weekly run) formally documents: *"QDF false positives: 4-7-8-breathing was exceptional at Day-14 (pos 2.5) but crashed to pos 36.2 by Day-42. Day-14 interim verdicts for stub-pilot content are NOT reliable — Day-42 is the true signal."*

The stub-pilot Day-42 batch closed 0🟢/0🟡/1🔴/5⚫ — the worst single-batch outcome in system history. Of the 5⚫ WORSE verdicts, at least 1 was driven by a QDF spike that made Day-14 appear positive. T12's spec (Step 3a / Step 4b) contains a general QDF guard, but it applies only when the *analyst* cites QDF as an explanation post-hoc — there is no proactive "do not close as 🟢 at Day-14 for stub-pilot class" rule.

**Evidence:**
- `brain/BRAIN.md` 2026-09-06: "Day-14 interim verdicts for stub-pilot content are NOT reliable — Day-42 is the true signal."
- `brain/WATCH.md` W24: 🟢 EXCEPTIONAL at Day-14 → ⚫ WORSE at Day-42.
- `brain/memory/experiments/closed-stubpilot-day42-batch-2026-09-06.md`: all 5 stub-pilot pages stalled/worse.
- `logs/observation-2026-09-05.txt`: 4-7-8-breathing pos 36.2 at Day-42 vs pos 2.5 at Day-14.

## Proposed change
**File to edit:** `cowork-tasks/task12-learner.md`
**Edit type:** sed-replace

### Before
```
4b. **External confound guard** — when noting an external confound (Core Update, broad algorithm update, QDF, etc.) as the explanation for a 🔴 or ⚫ verdict:
```

### After
```
4a-stub. **Stub-pilot Day-14 QDF guard (mandatory)** — For any watch where `auto_shipped_by_task: stub-pilot` (or watch ID starts with W24/W25/W26/W27/W28 from the mindful-minutes pilot, or any future stub-pilot batch):
   - At **Day-14**: record the position but label the verdict `QDF_RISK_INTERIM`. Do NOT close the watch. Do NOT label as 🟢 EXCEPTIONAL or 🟢 RECOVERED regardless of position.
   - Rationale: stub-pilot content targets named-protocol queries that frequently receive a short QDF spike (Google freshness boost for new unique content); the spike can produce sub-pos-5 readings at Day-14 that fully normalize by Day-42.
   - Write in the watch log: `QDF_RISK_INTERIM: pos {X} at Day-14 — stub-pilot class, Day-42 is the mandatory evaluation gate. Do not close.`
   - At **Day-42**: close normally with standard verdict criteria.

4b. **External confound guard** — when noting an external confound (Core Update, broad algorithm update, QDF, etc.) as the explanation for a 🔴 or ⚫ verdict:
```

## Rationale

The stub-pilot is a distinct content class (named-protocol short-form pages targeting specific technique queries). These pages get a measurable QDF spike at Day-14 that doesn't reflect steady-state rank. A false 🟢 EXCEPTIONAL verdict at Day-14 (1) inflates P12 evidence base, (2) misleads Strategist into believing stub-pilot works, and (3) delays the correct STALLED/WORSE diagnosis by 28 days. Adding a mandatory `QDF_RISK_INTERIM` label at Day-14 for this content class prevents these errors without requiring any script changes.

## Risk assessment

Low. The change delays closing stub-pilot watches from Day-14 to Day-42 — they stay OPEN longer but with correct labeling. Non-stub-pilot watches are unaffected. If the rule is too broad, worst case is a stub-pilot page that genuinely recovers (not QDF) getting held open 28 extra days before a final 🟢.

## Rollback

Before-snapshot: current `cowork-tasks/task12-learner.md` line 45 onward. To revert, delete the `4a-stub.` block added above (everything between the new `4a-stub.` header and the existing `4b.` header).
