# Proposal: T1 immediately post Slack alert when rank-pull.py fails

**Proposed:** 2026-07-05T20:00:00+05:30
**Source:** task13-meta-learner-2026-07-05
**Apply on:** 2026-07-12T20:00:00+05:30
**Status:** preview

## Issue detected

When `rank-pull.py` fails (API timeout or connection error), Task 1's "Important rules" says: "log the error and stop — do not guess at data." The task then terminates **before reaching Step 8 (Slack post)**. This means the failure is silent from Slack's perspective — no notification fires until the Strategist reads `logs/rank-summary-{TODAY}.txt` at 8 PM IST (7-9 hours later).

**Evidence — this week:**

- 2026-06-30: DataForSEO API timed out. Carried forward 06-29 data. No same-day Slack alert.
- 2026-07-01: API timed out again. Still no same-day Slack alert.
- 2026-07-03: API timed out (3rd time in 5 days). Rank summary log shows "SCRIPT STATUS: rank-pull.py DID NOT COMPLETE" + "ACTION REQUIRED: Re-run rank-pull.py manually". This instruction sat in a log file until Strategist saw it at 8 PM.

Decision log 2026-07-03: "DataForSEO API timed out again (2nd consecutive day; 06-29 carry-forward)." Strategist confirmed the gap: BRAIN.md notes pattern is "intermittent (not 3 consecutive yet; 07-02 was clean). Hard infrastructure alert NOT triggered yet."

This means the system only escalates after **3 consecutive failures** — but it only counts failures that the Strategist can observe. If the Slack notification never fires, Kushal has no real-time visibility. The 3-consecutive rule is only meaningful if each individual failure is visible at detection time.

**The gap:** T1 fires at 7 AM IST. A timeout at 7 AM means no rank data all day. Strategist picks this up at 8 PM IST. That's 13 hours of silent failure.

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task1-rank-surveillance.md`
**Edit type:** line-edit (Important rules section, API error rule)

### Before

```
- If the script fails with an API error, log the error and stop — do not guess at data
```

### After

```
- If the script fails with an API error: (1) write the error to `logs/rank-summary-{TODAY}.txt` with header line `SCRIPT STATUS: rank-pull.py DID NOT COMPLETE — API timeout or connection error`, (2) **immediately post to Slack `#seo-workflow-mindtalk` (channel `C0AUAPS4J83`) before stopping:**

  ```
  ⚠️ *T1 Rank Pull FAILED — {TODAY}*
  Site: mindtalk.in
  Status: rank-pull.py did not complete (API timeout or connection error)
  No fresh rank data today. Carrying forward previous run.
  Manual re-run: `python3 scripts/rank-pull.py`
  ```

  Then (3) stop — do not proceed to Step 8 (the failure alert above replaces the normal Step 8 summary).
```

## Rationale

The Strategist reads rank logs at 8 PM and catches the failure eventually. But Kushal needs real-time visibility — the point of Slack notifications is to surface issues when they happen, not hours later. With DataForSEO timing out 3/5 days this week, the "not 3 consecutive" hard-alert rule is technically unbreached — but without same-day Slack visibility on each failure, the pattern is invisible until the Strategist counts them.

This change adds one `slack_send_message` call at the point of failure (T1, 7 AM IST) instead of relying on the Strategist's evening read. Cost: negligible (one Slack API call). Value: Kushal sees the failure by 7:05 AM and can manually kick off a re-run if needed, or DataForSEO support can be contacted during business hours.

The change also clarifies that the failure alert *replaces* Step 8 — preventing a confusing double-post (failure alert + empty summary).

## Risk assessment

Near-zero. The only change is: add one Slack post when the script fails. The current behavior (stop without alerting) is a silent failure — any change is better than silence.

Edge case: if `slack_send_message` itself fails (e.g., expired token), the task still stops cleanly with the error in the log. The Strategist will still catch it at 8 PM. No regression vs current behavior.

## Rollback

Snapshot: `brain/before-snapshots/task1-rank-surveillance.md-{TIMESTAMP}.bak`

To revert: copy snapshot back. The only effect of rollback is returning to silent API failures — no data is at risk.

## Veto instructions

To veto: rename to `t1-api-failure-slack-alert-2026-07-05-2000.vetoed.md` and add `## Veto reason`.
To approve early: rename to `t1-api-failure-slack-alert-2026-07-05-2000.approved.md`.
