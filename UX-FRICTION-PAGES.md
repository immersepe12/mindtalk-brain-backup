# UX Friction Pages — Updated 2026-09-23 (W39)

**Written by:** T19 Conversion Intelligence. Source: Mixpanel $mp_rage_click + $mp_dead_click, trailing 7d Sep 16–22.
**Read by:** T10 Strategist (prevents SEO investment in broken pages) + Product/Dev team.
**NOT for T18** — these are UI bugs, not E-E-A-T problems.

---

## W39 Site totals
- **Rage clicks:** 750 total / 247 unique (+2.9% vs W37 729) — 🔴 SUSTAINED HIGH
- **Dead clicks:** 4,883 total / 1,141 unique (+5.3% vs W37 4,635) — 🔴 ESCALATING (dead rate 11.1% of visitors)

**Note (W38 gap):** W38 had Mixpanel billing block. W39 vs W37 comparison (2-week gap) — values are directionally comparable.

---

## W39 Dead click hotspots (same pattern as W37 — app UX unchanged)

All dead clicks on consult.cadabams.com (app), NOT mindtalk.in (website). SEO website clean.

**Critical pages persist:**
- consult.cadabams.com/home — highest single-page dead clicks (pattern sustained)
- consult.cadabams.com/consult/find-therapist — PERSISTENT W27+ (now W39, 12+ weeks unresolved)
- consult.cadabams.com/consult/checkout + /consult/consent — payment funnel blocked
- consult.cadabams.com/auth/login — login wall friction

**Journey Task crash deepening:** Started Journey Task: 645 (W34) → 365 (W35) → 124 (W36) → 30 (W37) → 27 (W39). Near-zero for 3+ weeks. Journey UX dead clicks confirm hypothesis: buttons non-responsive.

---

## W37 Dead click hotspots (reference)

---

## W37 Dead click hotspots (descending by count — top 20 of 898 pages)

| URL (condensed) | Dead clicks | Status | Likely cause |
|---|---:|---|---|
| consult.cadabams.com/home | 789 | 🔴 CRITICAL #1 | App home — broken CTAs or loading failures; 789 is highest single-page total ever |
| consult.cadabams.com/consult/appointments | 246 | 🔴 CRITICAL | Appointments page UX broken — scheduler unresponsive |
| consult.cadabams.com/consult/find-therapist | 237 | 🔴 PERSISTENT (W27+) | Filter/CTA non-responsive. On watchlist since W27. Not resolved. |
| consult.cadabams.com/auth/login | 151 | 🔴 CRITICAL | Login wall frustration — users expect to proceed, hit gate |
| consult.cadabams.com/consult/checkout | 82 | 🔴 HIGH | Checkout form issues — buttons/fields dead |
| consult.cadabams.com/assessments/[specific] | 72 | 🟡 HIGH | Specific assessment details page broken |
| consult.cadabams.com/assessments | 72 | 🟡 HIGH | Assessments hub — navigation unresponsive |
| consult.cadabams.com/consult/find-therapist?p=2 | 61 | 🟡 HIGH | Pagination dead — page 2 therapist list broken |
| consult.cadabams.com/consult/find-therapist?p=1 | 60 | 🟡 HIGH | Pagination dead — page 1 also affected |
| consult.cadabams.com/consult/appointments/1444571 | 56 | 🟡 HIGH | Specific appointment detail unresponsive |
| consult.cadabams.com/assessments/cmpc9j73l00jp01qp5xcf9l3d/details | 50 | 🟡 HIGH | Assessment detail page broken |
| consult.cadabams.com/consult/consent | 48 | 🟡 HIGH | Consent page blocking payment completion |
| consult.cadabams.com/wellness/mindful-minutes/sleep-and-deep-relaxation | 47 | 🟡 HIGH | Wellness content page — Journey Task adjacent? |
| consult.cadabams.com/profile | 44 | 🟡 HIGH | Profile page UX unresponsive |
| consult.cadabams.com/consult/booking/[id] | 36–29 | 🟡 HIGH | Multiple booking pages with dead clicks |
| consult.cadabams.com/documents | 28 | 🟡 WATCH | Documents section |
| consult.cadabams.com/journeys/[id]/details | 27 | 🟡 WATCH | Journey detail page — likely connected to Journey Task crash |

**Note:** ALL dead clicks on consult.cadabams.com (the app), NOT on mindtalk.in (the website). SEO website is clean. App UX is broken.

---

## Critical connection: Journey Task crash + UX friction

Started Journey Task: 645 → 365 → 124 → **30** (W34→W37, -95.4% in 4 weeks)

The `/journeys/[id]/details` dead clicks AND the `/wellness/mindful-minutes/sleep-and-deep-relaxation` dead clicks (47) suggest journey content is unresponsive. **Hypothesis: Journey Task crash is a UX bug, not behavioral.** Users may be trying to start tasks but the buttons/navigation are dead.

This warrants immediate product investigation:
1. Is `Started Journey Task` event still firing correctly?
2. Are journey task buttons rendering/clickable?
3. Is there a broken state on journey cards post-assessment?

---

## Most urgent dev actions (W37)

**Priority 1 — EMERGENCY:** `/consult/home` (789 dead clicks)
- App home page is the single biggest friction point on the entire platform
- 789 dead clicks = 8.4% of unique visitors hitting non-responsive elements
- Fix: audit every CTA, card, and navigation element on the home page

**Priority 2 — EMERGENCY (Journey Task crash):** `/journeys/*` and `/wellness/*`
- Journey-related pages have dead clicks
- 4-week crash: 645→365→124→30 starts journey tasks is a product emergency
- Fix: check if `Started Journey Task` event is firing, audit journey card UX

**Priority 3 — PERSISTENT W27+:** `/consult/find-therapist` (237 dead + pagination)
- Combined find-therapist pages (main + p1 + p2) = 358 dead clicks total
- Filter UI or booking button non-responsive — persistent 10+ week issue

**Priority 4 — PAYMENT FUNNEL:** `/consult/checkout` (82) + `/consult/consent` (48)
- Users reaching checkout are hitting dead elements — direct revenue impact
- Consent page blocking payment completion (48 dead)

**Priority 5 — AUTH WALL:** `/auth/login` (151 dead clicks)
- Login wall still creating massive friction in mid-funnel

---

## Historical trend

| Week | Rage clicks | Dead clicks | Status |
|---|---:|---:|---|
| W27 | ~200 est | ~1,800 est | ESCALATING |
| W28 | ~220 est | ~2,100 est | CRITICAL (checkout dead clicks new) |
| W34 | ~400 est | 4,441 | 🔴 CRITICAL spike (+111%) |
| W35 | 479 | 3,761 | ✅ Improving |
| W36 | ~500 est | 3,761 | ⚪ Flat (W35 data held) |
| **W37** | **729** | **4,635** | 🔴 RE-ESCALATING |
| **W39** | **750 (247 uniq)** | **4,883 (1,141 uniq)** | 🔴 ESCALATING (dead rate 11.1%) |
