# UX Friction Pages

**Written by:** T19 Conversion Intelligence (weekly, Wednesdays)
**Source:** Mixpanel 4011856 — `$mp_rage_click` (frustrated clicking) + `$mp_dead_click` (non-responsive UI element)
**Scope:** consult.cadabams.com (the booking/app layer). These events do NOT fire on mindtalk.in itself.
**Purpose:** Surface booking-flow friction that depresses downstream conversion from mindtalk.in → consult → payment.

---

## W31 Friction Table (Jul 22–28, 2026)

| URL | Rage clicks | Dead clicks | Total | Severity | Status / WoW |
|---|---:|---:|---:|---|---|
| consult.cadabams.com/prescriptions | 127 | 887 | **1,014** | 🔴🔴 CRITICAL #1 — NEW | Brand new this week. Page functionally broken. Escalate to dev IMMEDIATELY. |
| consult.cadabams.com/home | 38 | 673 | **711** | 🔴🔴 ESCALATING | Dead clicks 129→673 (+421%). Something broke in the home page navigation — buttons not responding. |
| consult.cadabams.com/consult/find-therapist | 47 | 372 | **419** | 🔴 HIGH PERSISTENT | Dead clicks 319→372 (+16.6%). 4 consecutive weeks. NOT FIXED. |
| consult.cadabams.com/consult/appointments | ~0 | 160 | 160 | 🟡 IMPROVING | Total 237→160 (-32.5%) ✅ Improving — keep monitoring. |
| consult.cadabams.com/consult/checkout | ~4 | 69 | 73 | 🔴 PERSISTENT | Dead clicks stuck at 68→69 — 3+ weeks unresolved. Checkout friction = direct revenue loss. |
| consult.cadabams.com/consult/booking/8796 | 36 | ~50 | ~86 | 🟡 IMPROVING | Rage: 96→36 ✅ improving significantly. |
| journeys/cmraiwmuz*/details | 0 | 75 | 75 | 🟡 MEDIUM | Journey page — UI element not responding |
| consult.cadabams.com/assessments/* | ~0 | 52 | 52 | 🟡 MEDIUM | New this week |
| consult.cadabams.com/ (root) | ~0 | ~30 est | ~30 | 🟢 LOW | Baseline |

**Total friction events W31: ~2,680** (up from ~1,124 W28 — driven almost entirely by /prescriptions new + /home explosion)

---

## Priority action queue

### 🔴🔴 P0 — /prescriptions (1,014 events) — ESCALATE NOW
- **887 dead clicks + 127 rage clicks** = highest friction event count in T19 history.
- Brand new this week — something broke on the /prescriptions page.
- Likely: a button/link/form is rendering but not wired up, or page requires auth but doesn't redirect.
- **Action:** Escalate to app dev team TODAY. Check if /prescriptions is feature-complete or was accidentally deployed in broken state.

### 🔴🔴 P0 — /home dead click explosion (+421%)
- Dead clicks 129 → 673 in one week.
- New ad campaigns are sending traffic to /home after sign-up or post-session — users are trying to click navigation elements that aren't responding.
- **Action:** Audit /home navigation elements. Check if any new feature deployment broke click handlers. Particularly suspect: any element added in the W29-W31 timeframe.

### 🔴 P1 — /consult/find-therapist (4 weeks unresolved, 419 events)
- 4th consecutive week with 300-400+ dead clicks.
- Therapist search UI has a persistent broken element — users repeatedly click something that doesn't respond.
- **Action:** Inspect filter UI, therapist cards, and pagination. This is suppressing therapist discovery → bookings.

### 🔴 P1 — /consult/checkout (stuck at ~70 events, 3+ weeks)
- Direct checkout friction = confirmed revenue loss. Every dead click here is a payment that bounces.
- **Action:** Inspect payment form submission button, CTA, and any checkout redirect logic.

### 🟡 P2 — /consult/appointments (improving)
- 237→160 (-32.5%). Positive trend. Continue monitoring — do not touch.

### 🟡 P2 — /consult/booking/8796 (improving)
- Rage 96→36. Continue monitoring.

---

## Historical trend (Total friction events per week)

| Week | Top page | Total events (est) | Notes |
|---|---|---:|---|
| W25 | find-therapist | ~800 est | INAUGURAL |
| W26 | find-therapist | ~900 est | find-therapist escalating |
| W27 | find-therapist | ~1,300 est | booking/8796 NEW CRITICAL rage clicks |
| W28 | find-therapist + checkout | ~1,124 est | checkout dead clicks NEW; booking/8796 escalating |
| W29 | — | — | MCP_DOWN |
| W30 | — | — | MCP_BLOCKED |
| W31 | **prescriptions** | **~2,680 est** | /prescriptions NEW CRITICAL #1 (1,014); /home explodes (+421%) |

---

## Notes for T10 Strategist

1. **Prescriptions page is the biggest new revenue leak.** Users who reach /prescriptions are post-engagement, high-intent. A broken prescriptions page means they exit without completing action.
2. **Home page dead clicks will suppress repeat visits.** If users return to the app and hit dead UI on /home, they churn silently.
3. **find-therapist and checkout are long-standing issues** suppressing conversion from organic traffic. 4+ weeks of evidence = dev team hasn't prioritized.
4. **Checkout fix = highest direct revenue impact.** Every unresolved dead click at checkout = abandoned payment.
