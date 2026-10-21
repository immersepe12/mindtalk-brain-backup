# UX Friction Pages — Updated 2026-10-21 (W43)

**Source:** T19 Conversion Intelligence. Rage click threshold: >5% page rate. Dead click threshold: >10% site rate.
**Read by:** T10 Strategist, T18 Professional Input (Leaky Bucket UX audits)

---

## W43 Friction Summary (Oct 14–21)

| Metric | W43 | W42 | Δ% |
|---|---|---|---|
| Rage clicks (unique) | 222 | 272 | -18.4% 🟢 improving |
| Dead clicks (unique) | 1,296 | 1,337 | -3.1% 🟢 improving |
| Dead rate (site) | 10.6% | 10.7% | ⚠️ still above 10% |
| Rage rate (site) | ~1.8% | 2.2% | improving ✅ |

---

## Top Rage Click Pages (W43 — total rage events)

| Rank | Page | Rage events | Severity | Notes |
|---|---|---|---|---|
| 1 | assessments/ks2r5bcpvv4p9yw4x4ym8lbr (returnTo param) | 36 | 🔴 HIGH | Assessment with redirect param — frustration at flow |
| 2 | consult/booking/8796?mode=online | 32 | 🔴 HIGH | Persistent from W42 — booking UX broken |
| 3 | consult/booking/20388?mode=online | 30 | 🔴 HIGH | Same booking flow pattern |
| 4 | consult/booking/102290?mode=online | 29 | 🔴 HIGH | Booking UX systemic issue |
| 5 | wellness/mindful-minutes/v7ajmjtv2glmpoau1p1eallx | 27 | 🟡 MEDIUM | App wellness feature |
| 6 | profile | 25 | 🟡 MEDIUM | User profile page |
| 7 | home | 23 | 🟡 MEDIUM | App homepage |
| 8 | onboarding/start | 22 | 🟡 MEDIUM | Onboarding friction |

**Pattern:** booking/* pages with ?mode=online consistently generating high rage. Likely broken UI element or payment failure feedback loop.

---

## Top Dead Click Pages (W43 — total dead click events)

| Rank | Page | Dead events | Severity | Notes |
|---|---|---|---|---|
| 1 | home | 679 | 🔴 CRITICAL PERSISTENT | W37+ multi-week. App homepage unresponsive elements |
| 2 | consult/find-therapist | 129 | 🔴 HIGH | Therapist discovery flow — elements not clickable |
| 3 | consult/appointments | 102 | 🔴 HIGH | Appointment management — persistent multi-week |
| 4 | profile | 95 | 🔴 HIGH | Profile page elements dead |
| 5 | care | 78 | 🟡 MEDIUM | Care hub page |
| 6 | auth/login (returnTo assessment) | 62 | 🟡 MEDIUM | Login redirect friction |
| 7 | consult/checkout | 61 | 🔴 HIGH NEW | **NEW W43 — PAYMENT FLOW. Dead clicks at checkout = lost revenue.** |
| 8 | find-therapist?p=2 | 54 | 🟡 MEDIUM | Pagination dead elements |
| 9 | assessments/woi1cncqbbzftmo6f0260mqo/details | 50 | 🟡 MEDIUM | google organic referral |
| 10 | assessments/v2cm5muphut23y8wzl0sybct/details | 50 | 🟡 MEDIUM | google organic referral |

---

## CRITICAL ALERTS (Action Required)

### 🔴 CRITICAL: /consult/checkout — 61 dead clicks (NEW W43)
**Impact:** Direct revenue loss. Dead clicks on checkout page = abandoned payment transactions. With organic payments down -31% in W43, checkout friction is a PLAUSIBLE CONTRIBUTING CAUSE alongside seasonal effects.
**Action:** Product team must audit /consult/checkout UX immediately. Which elements are receiving dead clicks? CTA button? Payment form? Back navigation?
**Priority:** P0 (revenue-impacting)

### 🔴 CRITICAL PERSISTENT: /home — 679 dead clicks (multi-week since W37)
**Impact:** App landing page broken UX — erodes trust and navigation efficiency.
**Status:** Unresolved since W37. Weeks: W37, W38, W39, W40, W41, W42, W43 — 7 weeks unresolved.
**Action:** Escalate to product engineering. This requires code fix, not content change.

### 🔴 HIGH: /consult/booking/* (mode=online) — systemic rage click pattern
**Impact:** Booking flow generates persistent rage across multiple doctor booking pages.
**Pattern:** booking/8796, booking/20388, booking/102290 all showing high rage in W42 + W43.
**Action:** Investigate online booking mode vs in-person mode UX differences. Likely a shared component bug.

---

## Week-over-Week Trend

| Page | W42 | W43 | Trend |
|---|---|---|---|
| /home dead | ~679 | 679 | 🔴 STABLE HIGH |
| /consult/checkout dead | 61 (W42 unclear) | 61 | 🔴 NEW/ESCALATING |
| /consult/appointments dead | 102 (W42: 814) | 102 | 🟢 MASSIVE IMPROVEMENT |
| /consult/find-therapist dead | 129 | 129 | 🟡 STABLE |
| /worksheets rage | 233 | 0 (not in top) | 🟢 RESOLVED |
| booking/* rage | ~87+ | 91 total | 🔴 PERSISTENT |

---

## Historical Friction Notes
- W42: /worksheets 233 unprecedented rage (RESOLVED W43)
- W41: /assessments 515 completions despite friction — engagement strong
- W39: Dead rate 11.1% (site) — crossed threshold
- W37: /home dead clicks began (now 7 weeks unresolved)
- W36: Journey Task crash deepened (now recovering W42-W43)
