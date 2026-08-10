# Proposal: T16 Part A.5 — Re-file with corrected Before anchor (MISMATCH-SKIP recovery)
**Proposed:** 2026-08-03T20:30:00+05:30
**Source:** task13-meta-learner-2026-08-03
**Apply on:** 2026-08-10T20:00:00+05:30
**Status:** preview

## Issue detected

**Original proposal:** `brain/proposed-changes/t16-read-pending-human-actions-2026-07-26-2030.md`
- Filed 2026-07-26. Apply date 2026-08-02. Passed the 7-day window.
- Strategist 2026-08-03 applied it as **MISMATCH-SKIP**: the Before block in the proposal (`### Part B — Git + deploy state`) no longer exists in `task16-operational-health-backup.md` — it was renamed to `### Part B — Brain Backup` by a prior proposal (`t6-dead-url-prefix-guard`, applied 2026-07-26). BRAIN.md stamp 2026-08-03: *"t16 ⚠️ MISMATCH-SKIP (Before-block '### Part B — Git + deploy state' changed to '### Part B — Brain Backup' by a prior proposal — manual anchor fix needed before re-filing)."*
- **Second MISMATCH-SKIP** confirmed on 2026-08-03 second Strategist run (ADDENDUM stamp).

**Why the original change is still needed:**
The `t11-flag-human-slack-fallback` proposal (applied 2026-07-26) made T11 write missed `flag_for_human` escalations to `logs/pending-human-actions-{TODAY}.txt` as a Slack-delivery fallback. But nothing reads that file. T16 runs Mon/Thu/Sat and has a Slack digest step — it's the right place to surface these missed escalations. Without this addition, any `flag_for_human` whose Slack fails is silently invisible to the system.

Evidence of recurring Slack failure: confirmed ERR_FAILED on T11 runs 2026-07-14, 2026-07-21, 2026-07-23, 2026-07-28. The STUB-PILOT-TRIAGE-01 escalation was silently lost, then re-escalated 3 more times across multiple Strategist runs.

## Proposed change
**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task16-operational-health-backup.md`
**Edit type:** line-edit (insert new Part A.5 block before the existing `### Part B — Brain Backup` section)

### Before
```
### Part B — Brain Backup
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
2. Check if the entry's `BACKLOG_ID` still appears in `brain/BACKLOG.md` with an open (non-completed) status.
3. In the T16 Slack digest (Part C), include a section:
   ```
   ⚠️ *Missed escalations (Slack-delivery failures recovered):*
   • [{BACKLOG_ID}] {1-line summary} — detected {DATE}, still undelivered. Check brain/BACKLOG.md for action.
   ```
4. Do NOT mark these entries as resolved — that is Kushal's job after seeing them in the digest.
5. If no `pending-human-actions-*.txt` files exist from the past 7 days → skip silently (no mention in digest).

This step ensures that any `flag_for_human` whose Slack delivery failed on a previous T11 run is surfaced at least once per T16 run (Mon/Thu/Sat), even if Slack is persistently unavailable.

---

### Part B — Brain Backup
```

## Rationale

The `t11-flag-human-slack-fallback` (applied 2026-07-26) creates a write-side fallback: T11 misses Slack → writes to `logs/pending-human-actions-{TODAY}.txt`. Without a reader, that file is a dead archive. T16 runs 3× per week (Mon/Thu/Sat), has file-system access to `logs/`, and already produces a Slack digest (Part C). Adding this scan closes the loop: T11 writes → T16 reads → surfaces in T16 digest → Kushal sees it.

The BACKLOG row also remains open (per T11 fallback spec), so Strategist re-queues it independently. Two delivery paths = near-zero chance of permanent loss.

## Risk assessment

**Low.** The change is read-only on `logs/pending-human-actions-*.txt`. The only side-effect is optional content added to the T16 Slack digest when missed escalations exist. If no files are found (normal case), the step is a no-op. Degrades gracefully if Slack is also down when T16 runs (entry still appears in T16 run log, BACKLOG row remains open for Strategist).

## Rollback

Copy `brain/before-snapshots/task16-operational-health-backup-{TIMESTAMP}.bak` back to `cowork-tasks/task16-operational-health-backup.md`.

## Veto instructions
To veto: rename this file to `t20-t16-pending-actions-anchor-fix-2026-08-03-2030.vetoed.md` and add a `## Veto reason` section.
To approve early: rename to `t20-t16-pending-actions-anchor-fix-2026-08-03-2030.approved.md`.
If neither, auto-applies 2026-08-10.
