# Proposal: T11 Step 4e — BRAIN.md fallback when Slack fails for flag_for_human
**Proposed:** 2026-07-19T20:30:00+05:30
**Source:** task13-meta-learner-2026-07-19
**Apply on:** 2026-07-26T20:00:00+05:30
**Status:** preview

## Issue detected

**Log evidence:** `brain/memory/experiments/2026-07-14-executor-run-summary.md` — T11 attempted `flag_for_human` for `STUB-PILOT-TRIAGE-01`. Slack post returned `ERR_FAILED`. T11 archived the escalation to `brain/memory/experiments/2026-07-14-flag_for_human-STUB-PILOT-TRIAGE-01.md` and then marked the BACKLOG row complete. The escalation was never delivered to Kushal.

**Downstream impact:** `brain/BRAIN.md` (2026-07-18 Strategist run) confirms `STUB-PILOT-DECISION-01` is now at 3rd escalation with no response. STUB-PILOT-TRIAGE-01 has been escalated at least 3 times across multiple runs (Batch 3 auto-fires 2026-07-24) — the root failure was the first Slack delivery that silently dropped on 07-14 and caused T11 to close the row as "done".

**Current step 4e flow (3 steps, no failure handling):**
1. Read context from BACKLOG row
2. Post detailed Slack message
3. Mark BACKLOG row complete

Step 3 executes regardless of whether step 2 succeeded. When Slack fails, the escalation is lost and the BACKLOG row is closed — meaning Strategist won't re-queue it. The only artifact is an experiment log that nothing reads.

## Proposed change
**File to edit:** `cowork-tasks/task11-executor.md`
**Edit type:** line-edit (Step 4e block)

### Before
```
#### 4e. `flag_for_human`

1. Read context from BACKLOG row
2. Post detailed Slack message with: what was detected, why it needs human eye, recommended action, link to relevant logs/briefs
3. Mark BACKLOG row complete
```

### After
```
#### 4e. `flag_for_human`

1. Read context from BACKLOG row
2. Post detailed Slack message with: what was detected, why it needs human eye, recommended action, link to relevant logs/briefs
3. **Check Slack delivery result:**
   - **If Slack post SUCCEEDED:** proceed to step 4 (mark complete).
   - **If Slack post FAILED (ERR_FAILED, network error, or no confirmation):**
     a. Append to `logs/pending-human-actions-{TODAY}.txt` (create file if it doesn't exist):
        ```
        [{TIMESTAMP}] FLAG_FOR_HUMAN SLACK DELIVERY FAILED — {BACKLOG_ID}
        What was detected: {1-line summary from BACKLOG row}
        Recommended action: {recommended_action from BACKLOG row}
        Full context: brain/memory/experiments/{TODAY}-flag_for_human-{target}.md
        Status: UNDELIVERED — Kushal has not seen this. Requires manual follow-up.
        ```
     b. In BACKLOG.md, update the row for this item — prepend to the Why/Notes field:
        `⚠️ SLACK FAIL {TODAY} — see logs/pending-human-actions-{TODAY}.txt`
     c. In BRAIN.md, add under the next "## Strategist — next run" section (or at the top of the Active Watches block if that section doesn't exist yet):
        `🚨 MISSED ESCALATION: {BACKLOG_ID} — Slack failed {TODAY}. Check logs/pending-human-actions-{TODAY}.txt`
     d. **Do NOT mark the BACKLOG row complete.** Leave it open so Strategist re-queues it on the next daily run.
     e. Log this sequence to `brain/memory/experiments/{TODAY}-flag_for_human-{target}.md`: "Slack delivery failed. Escalation archived. BACKLOG row left open for Strategist re-queue. BRAIN.md updated with missed-escalation flag."
4. Mark BACKLOG row complete **(only if Slack delivery in step 2 succeeded)**
```

## Rationale

The current 3-step flow has no branch for failure. When Slack drops (which happens frequently — see recurring ERR_FAILED in Executor logs), the escalation silently disappears. Marking the BACKLOG row complete removes it from Strategist's re-queue loop, so the item stays lost until a human notices the experiment file (which nothing reads automatically). The fix creates two guaranteed fallback surfaces: (1) the pending-human-actions log (which T16 operational health should read — see BACKLOG.md `T16-PENDING-ACTIONS-01` which was queued to address this), and (2) a BRAIN.md flag that Strategist sees on its very next daily run. Neither approach requires Slack to work.

## Risk assessment

Low. The change only activates on Slack failure — the happy path (Slack succeeds) is identical to the current flow. The only new write targets are: `logs/pending-human-actions-{TODAY}.txt` (new file, harmless), a BACKLOG.md row update (in-place edit of existing row text), and a BRAIN.md append (Strategist reads this daily already). The biggest risk is a BRAIN.md write collision if T10 Strategist is running concurrently — but T11 runs at 4:30 PM IST and T10 runs at 8:00 PM IST, so the 3.5h gap eliminates the collision window.

## Rollback

The Before block above contains the original 3-step flow. To revert: replace the new Step 4e block with the original 3-line flow. Rollback snapshot: `brain/proposed-changes/t11-flag-human-slack-fallback-2026-07-19-2030.md` (this file).
