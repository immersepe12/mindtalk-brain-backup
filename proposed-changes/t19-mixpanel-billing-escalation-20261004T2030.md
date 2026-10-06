# Proposal: Add billing-block guard + PushNotification escalation to Task 19 Step 2
**Proposed:** 2026-10-04T20:30:00+05:30
**Source:** task13-meta-learner-2026-10-04
**Apply on:** 2026-10-11T20:00:00+05:30
**Status:** preview

## Issue detected
Task 19 (Conversion Intelligence) has been silently blocked by Mixpanel billing failures on 3 separate occasions: W30 (2026-07-22), W38 (2026-09-16), W40 (2026-09-30). Log evidence: `brain/logs/conversion-intelligence-2026-09-30.md` shows `Run status: MCP_BLOCKED — "Your account is blocked because payment is required"`. BRAIN.md entry: `"Mixpanel billing blocked a 3rd time (W30, W38, W40; auto-pay recommended). MIXPANEL-BILLING-BLOCK-01 CLOSED (09-27) was premature — re-opened as -02."`

The current T19 spec has no billing-block detection in Step 2. The run proceeds to attempt Mixpanel queries (failing), and only logs failure at Step 11 (9 steps later). On a billing block, all downstream steps that depend on Mixpanel data (Steps 3–10) produce empty or stale output, but no immediate escalation fires. Kushal learns about the block only by reviewing T19 logs — not via push notification. The run has been silently producing degraded output for 3 consecutive months.

Evidence: `brain/logs/conversion-intelligence-2026-09-30.md` (W40 block), `brain/BRAIN.md` MIXPANEL-BILLING-BLOCK-01/-02 entries.

## Proposed change
**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task19-conversion-intelligence.md`
**Edit type:** sed-replace

### Before
```
### Step 2 — Pull per-page Mixpanel data (project 4011856 — UNIFIED)

For each URL with ≥100 page views in trailing 7 days, query Mixpanel via MCP for THREE event groups:
```

### After
```
### Step 2 — Pull per-page Mixpanel data (project 4011856 — UNIFIED)

#### Step 2-PRE. Billing-block guard (run ONCE before any Mixpanel queries)
Fire a single lightweight test query to Mixpanel before pulling real data:
- Query: `Run-Query` on project 4011856 with `event_name: "$mp_web_page_view"`, `date_range: last_1_days`, `limit: 1`
- If the query succeeds → proceed to Step 2 normally.
- If the query returns an error containing "blocked", "payment required", "billing", or "account suspended":
  1. Log: `MIXPANEL_BILLING_BLOCK: {error message} — run W{week_number} {date}`
  2. Check `brain/BRAIN.md` for prior MIXPANEL-BILLING-BLOCK entries. If any prior block exists within the last 60 days → this is a **repeat block**.
  3. On a repeat block: send PushNotification immediately:
     ```
     T19 BLOCKED (repeat): Mixpanel billing block W{week_number}. This is the {N}th block (prior: {dates}). Auto-pay likely needed on Mixpanel account. Conversion intelligence data gap this week.
     ```
  4. Skip Steps 2–10. Jump directly to Step 11 with `mixpanel_status: BILLING_BLOCKED` and log the block date and repeat count.
  5. On a first-time block (no prior block in BRAIN.md within 60 days): log the block and continue to Step 11 with `mixpanel_status: BILLING_BLOCKED`. Do NOT push notify on first occurrence.

For each URL with ≥100 page views in trailing 7 days, query Mixpanel via MCP for THREE event groups:
```

## Rationale
3 billing blocks in 11 weeks means the system is producing silently degraded conversion-intelligence output for 3+ weeks per quarter without Kushal knowing in real time. A PushNotification on repeat blocks gives Kushal an actionable signal the moment the block is detected — not hours later when reviewing logs. The GA4 fallback already exists for Supermetrics unavailability (Step 2.5); this adds an equivalent early-exit for Mixpanel billing blocks, keeping the pattern consistent. The first-occurrence exception avoids alert fatigue for one-off transient errors.

## Risk assessment
Low risk. The guard adds one cheap test query per T19 run (well within the 30-query rate limit). If the test query erroneously returns a billing error (false positive), T19 skips Mixpanel for that week — same outcome as the billing block itself. False negatives (billing block not detected by the test query) are unlikely but leave behavior unchanged from today. The PushNotification fires only on confirmed repeat blocks, so not a spam risk.

## Rollback
Copy `brain/before-snapshots/task19-conversion-intelligence.md-{TIMESTAMP}.bak` back to `cowork-tasks/task19-conversion-intelligence.md`.

## Veto instructions
To veto: rename this file from `t19-mixpanel-billing-escalation-20261004T2030.md` to `t19-mixpanel-billing-escalation-20261004T2030.vetoed.md` and add a `## Veto reason` section explaining why.

To approve early: rename to `t19-mixpanel-billing-escalation-20261004T2030.approved.md` — Strategist's next 8 PM run will apply it.
