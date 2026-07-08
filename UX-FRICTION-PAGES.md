# UX Friction Pages

**Written by:** T19 Conversion Intelligence (weekly, Wednesdays)
**Source:** Mixpanel 4011856 — `$mp_rage_click` (frustrated clicking) + `$mp_dead_click` (non-responsive UI element)
**Scope:** consult.cadabams.com (the booking/app layer). These events do NOT fire on mindtalk.in itself.
**Purpose:** Surface booking-flow friction that depresses downstream conversion from mindtalk.in → consult → payment.

---

## W28 Friction Table (Jul 2–8, 2026)

| Page / URL | Rage clicks | Dead clicks | Total | Severity | WoW | Suspected cause |
|---|---:|---:|---:|---|---|---|
| consult.cadabams.com/consult/booking/8796?mode=online | 96 | 87 | **183** | 🔴 CRITICAL ESCALATING | Dead: 16→87 (+444%) | Aparna-rani booking broken. Availability broken or UI unresponsive. Was W26/W27 rage-only; dead clicks now exploding. |
| consult.cadabams.com/consult/find-therapist | 52 | 319 | **371** | 🟡 HIGH — IMPROVING | 481→371 (-22.9%) | Wizard dead clicks reducing — fix may be partially working. Still high. |
| consult.cadabams.com/consult/appointments | ~0 | 237 | **237** | 🔴 HIGH | flat from 240 | Appointments list — non-responsive elements. Persisting. |
| consult.cadabams.com/consult/checkout | ~4 | 68 | **72** | 🔴 NEW HIGH — PAYMENT FLOW | 🆕 new | **Dead clicks in the payment completion flow. Direct revenue impact. HIGHEST URGENCY.** |
| consult.cadabams.com/home | 14 | 129 | **143** | 🟡 HIGH — IMPROVING | 192→143 (-25%) | Home screen dead clicks reducing. ✅ |
| consult.cadabams.com/profile | 15 | 45 | **60** | 🟡 MEDIUM | 🆕 new | Profile page non-responsive elements. |
| consult.cadabams.com/baseline-assessment | 8 | 43 | **51** | 🟡 MEDIUM | ~stable (46→51) | Assessment dead click persists. |
| consult.cadabams.com/consult/booking/94441?mode=online | 21 | 1 | **22** | 🟡 NEW | 🆕 new | New rage hotspot. Check slot availability. |
| consult.cadabams.com/consult/booking/20508?mode=online | 19 | 12 | **31** | 🟡 MEDIUM NEW | 🆕 new | Dr. Srishti Agrawal. 19 rage = possible slot availability issue. |

---

## Priority actions W28

### 🔴 CRITICAL P1: /consult/checkout — 68 dead clicks (PAYMENT FLOW)
**This is the highest urgency issue this week.** Dead clicks in the checkout flow = users trying to complete payment and failing to interact with elements. This is post-intent abandonment — the hardest type to recover.

**Possible causes:**
1. Payment button not clickable in certain states (mobile, specific browsers)
2. Form field validation errors that prevent submission but don't show clearly
3. Promo code / coupon field that looks editable but isn't
4. Terms checkbox that is non-functional

**Action:** Dev team to reproduce checkout dead click flow on mobile + desktop. Record session replays for the 68 dead-click sessions if available in Mixpanel. Fix before next week.

---

### 🔴 CRITICAL P2: booking/8796 (aparna-rani) — 183 friction events
Dead clicks ESCALATED 16→87 (+444%). Rage persisting at 96. Combined 183 = **most broken page on the platform this week.**

**Action:** Check if Dr. Aparna Rani has available slots. If her schedule is full/inactive, remove from listings. If active — trace the dead click to specific UI element (likely the slot-picker or date-picker).

---

### 🟡 P3: find-therapist — 371 total (IMPROVING)
Dead clicks reduced 428→319. This is positive — fix may be partially deployed. Monitor W29. If drops below 200, consider it substantially resolved.

---

### 🟡 P4: /consult/appointments — 237 dead clicks (PERSISTING)
Three weeks of ~240 dead clicks. This is likely a structural UI issue (not a transient bug). Appointment list likely has an element that looks interactive but isn't — pagination? Filter? A table row that looks clickable but doesn't navigate?

---

## Trend (weekly summary)

| Week | Top friction page | Total friction events | CRITICAL pages | New this week |
|---|---|---:|---:|---|
| W25 | Not tracked | — | — | — |
| W26 | booking/53196 | 1,200+ | 1 | booking/53196 (CRITICAL) |
| W27 | find-therapist | 1,100+ | 2 | booking/8796 (NEW CRITICAL) |
| W28 | booking/8796 | 1,400+ | 3 | checkout dead clicks (CRITICAL) · booking/94441 · booking/20508 |

**Trend:** Total friction events increasing despite find-therapist improvement. booking/8796 escalating. New checkout issue is most dangerous — it's in the payment funnel.

**RESOLVED W27:** booking/53196 — 444 events W26, 3 events W28. Confirmed fixed. ✅

---

## Structural note

All friction events are on **consult.cadabams.com** (the booking/therapy app), NOT on mindtalk.in. The mindtalk.in pages have no rage/dead click instrumentation — this is a gap.

**Open action:** Add `$mp_rage_click` and `$mp_dead_click` tracking to mindtalk.in /illnesses/* and /treatments/* pages (currently showing 0 book intent — may be due to broken CTAs we can't see).
