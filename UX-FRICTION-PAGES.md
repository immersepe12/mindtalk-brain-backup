# UX Friction Pages — Updated 2026-08-26 (W35)

**Written by:** T19 Conversion Intelligence. Source: Mixpanel $mp_rage_click + $mp_dead_click, trailing 7d Aug 19–25.
**Read by:** T10 Strategist (prevents SEO investment in broken pages) + Product/Dev team.
**NOT for T18** — these are UI bugs, not E-E-A-T problems.

---

## W35 Site totals
- **Rage clicks:** 479
- **Dead clicks:** 3,761 (-15.3% vs W34 4,441 — improving from CRITICAL)

---

## W35 Rage click hotspots (descending by count)

| URL (condensed) | Rage clicks | Status | Likely cause |
|---|---:|---|---|
| consult.cadabams.com/home | 37 | 🔴 CRITICAL | App home page — users frustrated at landing; unclear UX or broken CTAs |
| consult.cadabams.com/auth/login?returnTo=/consult/checkout | 27 | 🔴 CRITICAL | Login wall in payment path — users about to pay, get auth wall, rage |
| consult.cadabams.com/consult/find-therapist | 22 | 🔴 ESCALATING | Persistent W27+ critical. Filter UX or CTA non-responsive |
| consult.cadabams.com/consult/consent | 21 | 🔴 CRITICAL | Consent page blocking payment flow — new critical |
| consult.cadabams.com/consult/booking/8796 | 19 | 🔴 PERSISTENT | Specific doctor page. Known issue since W27. Not resolved. |
| consult.cadabams.com/assessments/[specific] | 9+6 | 🟡 HIGH | Multiple assessment detail pages with friction |
| consult.cadabams.com/consult/booking/8970 | 12 | 🟡 HIGH | Another booking page with friction |
| consult.cadabams.com/consult/booking/59001 | 12 | 🟡 HIGH | In-person booking friction |
| consult.cadabams.com/consult/booking/101166 | 15 | 🟡 HIGH | New high-rage booking page |
| consult.cadabams.com/auth/signup | 9+ | 🟡 HIGH | Signup flow friction |
| consult.cadabams.com/consult/appointments | 4 | 🟡 WATCH | Appointments management page |
| consult.cadabams.com/consult/checkout | 2 | 🟡 WATCH | Checkout itself (low — auth wall catches users before here) |

---

## Most urgent dev actions (W35)

**Priority 1 — IMMEDIATE:** `/auth/login?returnTo=/consult/checkout` (27 rage clicks)
- Users in payment intent are hitting a mandatory login wall
- This is losing conversions at the most critical funnel step
- Fix: auto-complete checkout session after auth, or allow guest checkout for first-time users

**Priority 2 — IMMEDIATE:** `/consult/home` (37 rage clicks)  
- App home page UX is frustrating users — largest rage click count on site
- Likely: broken CTAs, loading states, or unclear navigation

**Priority 3 — ESCALATING:** `/consult/consent` (21 rage clicks)
- Consent page is blocking payment completion
- Users who've chosen a doctor are then stopped by consent UX — investigate form validation, required fields, or confusing copy

**Priority 4 — PERSISTENT W27+:** `/consult/booking/8796` (19 rage clicks)
- This specific doctor's booking page has had critical rage clicks for 8+ weeks
- Needs direct investigation of doctor 8796's booking flow

**Priority 5 — ONGOING:** `/consult/find-therapist` (22 rage clicks)
- The main therapist discovery page continues to accumulate rage clicks
- Filter behavior or booking button non-responsiveness

---

## Historical trend (W35)

| Week | Rage clicks (site) | Dead clicks (site) | Status |
|---|---:|---:|---|
| W27 | ~200 est | ~1,800 est | ESCALATING (find-therapist: 481) |
| W28 | ~220 est | ~2,100 est | CRITICAL (checkout dead clicks new) |
| W31 | — | — | /prescriptions 1,014 NEW CRITICAL |
| W32 | — | 814+803 | /appointments + /assessments critical |
| W34 | ~400 est | 4,441 | 🔴 CRITICAL spike (+111%) |
| **W35** | **479** | **3,761** | ✅ Improving but elevated |
