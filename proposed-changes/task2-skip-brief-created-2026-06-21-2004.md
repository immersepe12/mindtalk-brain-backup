# Proposal: Task 2 skips URLs already in BRIEF_CREATED state before re-confirming

**Proposed:** 2026-06-21T20:04:41+05:30
**Source:** task13-meta-learner-2026-06-21
**Apply on:** 2026-06-28T20:04:41+05:30
**Status:** preview

## Issue detected

`ANTI-PATTERNS.md` AP7 records: "Task 2 was re-confirming /treatments/psychotherapy 1 day after its brief was created, would have caused duplicate briefs with conflicting recommendations" (logged 2026-06-12). The stated mitigation is "Strategist double-checks tracking-db before fire" — i.e. the guard lives at the *fire* stage, downstream of Task 2.

But Task 2 itself (the GSC validator that runs Mon/Tue/Thu/Fri) still re-validates these URLs every run. Its only tracking-db skip rule today is for `OBSERVING` status:

- `cowork-tasks/task2-gsc-validator.md:36-38` (Step 6) only handles `OBSERVING` — it removes observation-pipeline URLs from `flagged-drops.json` so they aren't "re-validated every run forever." There is no equivalent skip for URLs already at `BRIEF_CREATED`.

Consequence: a URL with a brief already created keeps flowing through GSC validation on every Task 2 run, burning a GSC pull + re-classification each time, and relying entirely on the Strategist's later double-check to prevent the duplicate brief. Pushing the guard one stage earlier (into Task 2) is the cheaper, defence-in-depth fix and is exactly the wasted-work pattern Meta-Learner exists to remove. Matches the first-run note in `task13-meta-learner.md` (issue #2).

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task2-gsc-validator.md`
**Edit type:** line-edit (Step 6, lines 36-38) — append a BRIEF_CREATED bullet

### Before
```
6. Check `~/Seo-workflow-mindtalk/mindtalk-setup/tracking-db.json`:
   - If URL has status OBSERVING with observation_window_end in the future → skip it, log as "still in observation"
   - **Also remove this URL from `flagged-drops.json`** — once a URL is in observation, it is tracked through the observation pipeline (Task 4), not the flagged pipeline. Leaving it in flagged-drops causes it to be re-validated every run forever.
```

### After
```
6. Check `~/Seo-workflow-mindtalk/mindtalk-setup/tracking-db.json`:
   - If URL has status OBSERVING with observation_window_end in the future → skip it, log as "still in observation"
   - **Also remove this URL from `flagged-drops.json`** — once a URL is in observation, it is tracked through the observation pipeline (Task 4), not the flagged pipeline. Leaving it in flagged-drops causes it to be re-validated every run forever.
   - If URL has status BRIEF_CREATED (or PUBLISHED / any post-brief state) → skip it and remove it from `flagged-drops.json`, log as "brief already exists — handed to Strategist/ship pipeline". A brief already encodes the recovery plan; re-validating wastes a GSC pull and risks queuing a duplicate brief (see ANTI-PATTERNS AP7).
```

## Rationale

Moves the duplicate-brief guard upstream from the Strategist fire stage into the Task 2 validation stage, so post-brief URLs exit the flagged pipeline the same way observation URLs already do. Removes recurring wasted GSC pulls + re-classification and adds defence-in-depth behind AP7. Reinforces (does not contradict) AP7 — the existing Strategist double-check stays as a backstop.

## Risk assessment

Low. The change only causes Task 2 to *skip* URLs whose brief already exists — it cannot create or ship anything. Edge case: if a brief is later abandoned/withdrawn and the URL genuinely drops again, it must be re-flagged by Task 1 fresh (Task 1 writes flagged-drops from rank signal independently, so a real new drop re-enters the queue normally). No production code touched.

## Rollback

Strategist snapshots to `brain/before-snapshots/task2-gsc-validator.md-{TIMESTAMP}.bak` before applying. To revert: copy that snapshot back over `cowork-tasks/task2-gsc-validator.md`.

## Veto instructions

To veto: rename this file to `task2-skip-brief-created-2026-06-21-2004.vetoed.md` and add a `## Veto reason` section.
To approve early: rename to `task2-skip-brief-created-2026-06-21-2004.approved.md`.
