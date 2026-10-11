# Proposal: Add DataForSEO 402 billing-block detection to Task 1 with PushNotification on repeat
**Proposed:** 2026-10-11T20:30:00+05:30
**Source:** task13-meta-learner-2026-10-11
**Apply on:** 2026-10-18T20:00:00+05:30
**Status:** preview

## Issue detected

Category: **Slack notification gap / wasted work / missing signals (1b + 1f)**

DataForSEO returned 402 Payment Required (billing block) on 4 consecutive run-days: 2026-09-29 → 2026-10-05. BRAIN.md entry (2026-10-06): *"DataForSEO-402 ~Day 21 (4 failed run-days 09-29..10-05 -> infra FLAG pushed)."* Prior 402: 2026-09-18 (*"may be genuine billing/balance issue — escalated to Kushal via Slack"*).

**Current T1 gap:** `cowork-tasks/task1-rank-surveillance.md` "Important rules" section handles script failures generically as "API timeout or connection error" with a single Slack message. It has no specific detection of 402 (billing) vs transient network errors. On a billing block:
- The wrapper script runs, gets 402, writes a partial or empty output, and returns a non-zero exit code.
- T1 posts the generic "rank-pull.py DID NOT COMPLETE" alert.
- No PushNotification fires.
- On repeat blocks (09-18 + 09-29..10-05 = 2 billing events in 17 days), Kushal receives only Slack messages buried in the #seo-workflow-mindtalk feed — no phone notification distinguishing "billing issue needing payment action" from "transient API blip that auto-resolves."

4 blind days of rank data is the direct cost of missed early detection. Parallel precedent: T19 Mixpanel billing guard (proposal `t19-mixpanel-billing-escalation-20261004T2030.md`, applies today) addresses the identical pattern for Mixpanel.

## Proposed change
**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task1-rank-surveillance.md`
**Edit type:** sed-replace

### Before
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

### After
```
- **Before running the wrapper script**, check the last 50 lines of `logs/rank-summary-*.txt` (most recent file) for any prior `DATAFORSEO_BILLING_BLOCK` entry. Set `prior_block_found=true` if any exists within the past 60 days.

- If the script exits non-zero AND its output (captured to a temp variable or log) contains "402" or "Payment Required" or "payment_required" or "billing":
  1. Write to `logs/rank-summary-{TODAY}.txt`: `SCRIPT STATUS: DATAFORSEO_BILLING_BLOCK — 402 Payment Required received. Rank pull not started.`
  2. If `prior_block_found=true` (repeat block — same as 2026-09-18 + 2026-09-29..10-05 pattern):
     Send PushNotification immediately:
     ```
     T1 BLOCKED (repeat): DataForSEO 402 billing block. No rank data today. Refill account at dataforseo.com → Billing. Prior block also within last 60 days.
     ```
  3. Post to Slack `#seo-workflow-mindtalk` (C0AUAPS4J83):
     ```
     ⚠️ *T1 Rank Pull BILLING BLOCK — {TODAY}*
     Site: mindtalk.in
     Status: DataForSEO 402 Payment Required — rank pull not started.
     Action required: refill DataForSEO account at dataforseo.com → Billing.
     No fresh rank data today. Carrying forward previous run.
     ```
  4. Stop — do not proceed to Step 8.

- If the script exits non-zero AND output does NOT contain a billing indicator (transient error, timeout, network):
  (1) write the error to `logs/rank-summary-{TODAY}.txt` with header line `SCRIPT STATUS: rank-pull.py DID NOT COMPLETE — API timeout or connection error`, (2) **immediately post to Slack `#seo-workflow-mindtalk` (channel `C0AUAPS4J83`) before stopping:**

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
4 consecutive blind days (2026-09-29–10-05) resulted from a billing block that went undetected as billing-specific. Distinguishing 402 billing blocks from transient API errors lets Kushal take the correct action (refill account) immediately on his phone, rather than reading a generic Slack failure message that looks the same as a network blip. The pattern is now recurring (2+ events); PushNotification on repeat blocks turns it from "noise you might miss" to an urgent phone alert. Consistent with the T19 Mixpanel billing guard proposal (same architecture, different API).

## Risk assessment
Low. The change adds an output-inspection step before the existing error path — if the pattern check fails to match a billing error (false negative), the old Slack alert still fires. If it incorrectly classifies a non-billing error as billing (false positive), a harmless Slack billing message fires instead of the timeout message; operator action (refilling account) would confirm it was false. PushNotification only on repeat blocks limits phone alert volume.

## Rollback
Copy `brain/before-snapshots/task1-rank-surveillance.md-20261011T2030.bak` back to `cowork-tasks/task1-rank-surveillance.md`.

## Veto instructions
To veto: rename `t1-dataforseo-402-billing-guard-20261011T2030.md` → `t1-dataforseo-402-billing-guard-20261011T2030.vetoed.md` and add a `## Veto reason` section.
To approve early: rename → `t1-dataforseo-402-billing-guard-20261011T2030.approved.md` — Strategist's next 8 PM run will apply it.
If neither, auto-applies on 2026-10-18.
