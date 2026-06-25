# UX Friction Pages

**Written by:** T19 Conversion Intelligence (weekly, Wednesdays)
**Source:** Mixpanel 4011856 — `$mp_rage_click` (frustrated clicking) + `$mp_dead_click` (non-responsive UI element)
**Scope:** consult.cadabams.com (the booking/app layer). These events do NOT fire on mindtalk.in itself.
**Purpose:** Surface booking-flow friction that depresses downstream conversion from mindtalk.in → consult → payment.

---

## W26 Friction Table (Jun 18-24, 2026)

| Page / URL | Rage clicks | Dead clicks | Total | Severity | Suspected cause |
|---|---:|---:|---:|---|---|
| consult.cadabams.com/consult/booking/53196 | 273 | 171 | **444** | 🔴 CRITICAL | Doctor slot availability broken — users clicking unavailable slots repeatedly |
| consult.cadabams.com/consult/find-therapist | 53 | 240 | **293** | 🔴 HIGH | Wizard UI elements not responding (filters? dropdowns?) |
| consult.cadabams.com/consult/appointments | 0 | 157 | **157** | 🟡 MEDIUM | Appointments list UI unresponsive element |
| consult.cadabams.com/home | 0 | 108 | **108** | 🟡 MEDIUM | App homepage — unclear which element |
| consult.cadabams.com/baseline-assessment | 0 | 50 | **50** | 🟡 LOW-MEDIUM | Assessment flow dead click |

---

## Priority actions

### 🔴 CRITICAL: booking/53196 — 444 friction events
**Likely cause:** Doctor #53196 has a broken or fully-blocked availability calendar. Users who reach this doctor's booking page find no available slots but the UI doesn't clearly communicate this — they keep clicking expecting something to happen.

**Impact:** If this doctor appears in search results, doctor listings, or is recommended anywhere in the app, all traffic to them is converting to frustration. Zero bookings possible from this page while it's broken.

**Action:** Dev team must check:
1. Is doctor 53196 still active? (If deactivated, remove from all listings immediately)
2. If active — is their availability calendar connected? Are slots loading?
3. If slots are available — is the slot-click handler broken?

**Priority:** Immediate — this is a live revenue leak.

---

### 🔴 HIGH: find-therapist wizard — 293 friction events (240 dead clicks)
**Likely cause:** The find-therapist wizard has UI elements (filter dropdowns, radio buttons, "next step" buttons, or therapist card CTAs) that are not responding to clicks. Users are trying to filter or advance through the wizard and nothing is happening.

**Impact:** This is the alternative path to direct doctor_card CTAs. UTM data already shows direct doctor_card links outperform (66.7% of payments). If the wizard is also broken, there's no fallback path for users who don't know which doctor they want.

**Action:** QA the find-therapist flow end-to-end. Test every interactive element: specialty filter, price filter, language filter, therapist card "Book" button.

---

### 🟡 MEDIUM: /consult/appointments + /home — 265 combined dead clicks
**Likely cause:** Post-booking app pages (appointments history, home screen) have non-responsive elements. May be cosmetic (links that look clickable but aren't) rather than critical conversion blockers.

**Action:** Flag for next sprint. Lower priority than booking/53196 and find-therapist.

---

## Trend

| Week | Top friction page | Total events | CRITICAL pages |
|---|---|---:|---:|
| W25 | Not tracked (consult project was inaccessible) | — | — |
| W26 | booking/53196 | 444 | 1 |

*W25 inaccessible — W26 is de facto baseline.*

---

## Structural note

All friction events are on **consult.cadabams.com** (the booking/therapy app), NOT on mindtalk.in. The mindtalk.in pages have no rage/dead click instrumentation — this is a gap. If users are rage-clicking on mindtalk.in (e.g., broken CTAs on illness pages that show `book_appointment_clicked = 0`), we won't see it.

**Future action:** Add `$mp_rage_click` and `$mp_dead_click` tracking to mindtalk.in, particularly on /illnesses/* and /treatments/* pages where intent tracking shows 0 clicks (may be instrumentation gaps).
