# Conversion Intelligence Audit Log — 2026-09-16 (W38)

**Run date:** 2026-09-16
**Status:** MCP_BLOCKED

## Data Source Status

| Source | Status | Reason |
|---|---|---|
| Mixpanel project 4011856 | ❌ BLOCKED | Billing payment required |
| Supermetrics (MIX) | ❌ BLOCKED | Trial expired — NOT_AUTHENTICATED |

## Queries attempted

- book_appointment_clicked (unique, 7d) → BLOCKED
- Payment Successful (unique, 7d) → BLOCKED
- Appointment Booked (unique, 7d) → BLOCKED
- $mp_rage_click / $mp_dead_click → BLOCKED
- book clicks by utm_source → BLOCKED

**Total queries used: 0 / 30**

## Actions taken

1. page-conversion-history.md — W38 row appended: MCP_BLOCKED
2. Slack posted to C0AUAPS4J83: billing block notification
3. W37 tier classifications held (no change)

## W37 Classifications held

- 🟢 Goldmines: /treatments/cbt-therapy + /doctors/* cluster
- 🟡 Rockets: /illnesses/anxiety, /illnesses/depression, /blogs/anxiety-working-professionals, /blogs/[chatgpt-cited pages]
- 🔴 Leaky Buckets: 0
- ⚫ Dead: 3

## Pending confirmations (carry to W39)

- Kerala P8 W8 check (W37 regression — is it bounce-back or real?)
- Journey Task EMERGENCY (30 events W37 — 4-wk crash; product must investigate)
- chatgpt.com P5 W8 trajectory
- Europe diaspora W3 signal
- Dead clicks re-escalation (4,635 W37, +23.2% — needs W38 confirmation)

## Action needed for W39 to run

1. Mixpanel billing settled
2. Supermetrics trial renewed OR alternative Mixpanel access method established
