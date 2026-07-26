# Proposal: T16 Part A — Scan and surface pending-human-actions fallback files
**Proposed:** 2026-07-26T20:30:00+05:30
**Source:** task13-meta-learner-2026-07-26
**Apply on:** 2026-08-02T20:00:00+05:30
**Status:** preview

## Issue detected

**Log evidence chain:**
1. `brain/memory/experiments/2026-07-14-flag_for_human-STUB-PILOT-TRIAGE-01.md` — T11 `flag_for_human` for STUB-PILOT-TRIAGE-01 had Slack ERR_FAILED. The escalation was silently lost; T11 marked the BACKLOG row complete. STUB-PILOT-DECISION-01 then escalated 3 more times across multiple Strategist runs with no human response (confirmed in BRAIN.md 2026-07-18 stamp).
2. The `t11-flag-human-slack-fallback` proposal (applying **tonight at 8 PM**) fixes T11's failure mode by writing missed escalations to `logs/pending-human-actions-{TODAY}.txt`. This is a write-only fix: nothing currently reads that file.
3. T16 (`task16-operational-health-backup.md`) reads `logs/` for various health signals but has no step that scans for `logs/pending-human-actions-*.txt` files. The BACKLOG entry "T16-PENDING-ACTIONS-01" referenced in the t11 proposal was never created (confirmed: grep of BACKLOG.md for "T16-PENDING-ACTIONS-01" = 0 matches).
4. Strategist reads BRAIN.md and BACKLOG.md on every run — NOT arbitrary `logs/` files. So an unread pending-human-actions file is invisible to Strategist until T16 surfaces it.

**Impact:** Without this fix, the t11 fallback creates a write-only archive. Any `flag_for_human` that fails Slack delivery stays invisible to the whole system. Recurring ERR_FAILED pattern (confirmed in T11 logs 07-14, 07-21, 07-23) makes this a near-certainty to recur.

## Proposed change
**File to edit:** `cowork-tasks/task16-operational-health-backup.md`
**Edit type:** line-edit (append new Part A sub-step after the existing Part A health-check logic, before Part B git-sync check)

### Before
```
### Part B — Git + deploy state
```

### After
```
### Part A.5 — Pending human-action escalations (missed Slack deliveries)

Check for any `logs/pending-human-actions-*.txt` files created in the **past 7 days**:

```bash
find ~/Seo-workflow-mindtalk/mindtalk-setup/logs/ -name "pending-human-actions-*.txt" -newermt "$(date -d '7 days ago' +%F)" 2>/dev/null
```

For each file found:
1. Read its contents. Extract each `FLAG_FOR_HUMAN SLACK DELIVERY FAILED` entry.
2. Check if the entry's `BACKLOG_ID` still appears in `brain/BACKLOG.md` with an open (non-completed) status. If the BACKLOG row was left open (as T11's fallback spec requires), it should still be there.
3. In the T16 Slack digest (Part C), include a section:
   ```
   ⚠️ *Missed escalations (Slack-delivery failures recovered):*
   • [{BACKLOG_ID}] {1-line summary} — detected {DATE}, still undelivered. Check brain/BACKLOG.md for action.
   ```
4. Do NOT mark these entries as resolved — that is Kushal's job after seeing them in the digest.
5. If no `pending-human-actions-*.txt` files exist from the past 7 days → skip silently (no mention in digest).

This step ensures that any `flag_for_human` whose Slack delivery failed on a previous T11 run is surfaced at least once per T16 run (Mon/Thu/Sat), even if Slack is persistently unavailable.

### Part B — Git + deploy state
```

## Rationale

The `t11-flag-human-slack-fallback` proposal (applying tonight) creates the `pending-human-actions` file as a write-side fallback. Without a reader, the file is a dead archive. T16 runs 3× per week (Mon/Thu/Sat), has file-system access to `logs/`, and already includes a Slack digest step (Part C). Adding a 5-line scan to T16's Part A makes the fallback loop complete: T11 writes the missed escalation → T16 reads it → surfaces in T16's next Slack digest → Kushal sees it. The BACKLOG row remains open (per T11 fallback spec) so Strategist also re-queues it on the next daily run — two independent paths to delivery.

## Risk assessment

**Low.** The change is purely read-only on `logs/pending-human-actions-*.txt`. The only write side-effect is adding optional content to the T16 Slack digest when missed escalations are found. If no files exist (happy path), the step is a no-op. If Slack is also down when T16 runs, the entry still appears in the T16 run log, and the BACKLOG row remains open for Strategist.

The only edge case: if T11's fallback (t11 proposal) doesn't apply tonight for some reason, there will be no `pending-human-actions-*.txt` files to find. This proposal degrades gracefully — it only adds value once the t11 proposal is live.

## Rollback

Replace the inserted Part A.5 block with nothing (delete the entire section from `### Part A.5 —` through the closing line before `### Part B`). The BEFORE text is the absence of Part A.5 — no file snapshot needed. Rollback snapshot: `brain/proposed-changes/t16-read-pending-human-actions-2026-07-26-2030.md` (this file).

## Veto instructions
To veto: rename this file to `t16-read-pending-human-actions-2026-07-26-2030.vetoed.md` and add a `## Veto reason` section.
To approve early: rename to `t16-read-pending-human-actions-2026-07-26-2030.approved.md`.
If neither, auto-applies 2026-08-02.
