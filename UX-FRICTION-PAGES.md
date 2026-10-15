# UX Friction Pages — Updated 2026-10-14 (W42)

**Written by:** T19 Conversion Intelligence. Source: Mixpanel $mp_rage_click + $mp_dead_click, trailing 7d Oct 7–14, 2026.
**Read by:** T10 Strategist (prevents SEO investment in broken pages) + Product/Dev team.
**NOT for T18** — these are UI bugs, not E-E-A-T problems.

---

## W42 Site totals
- **Rage clicks:** 272 unique (+11.0% vs W41 ~245/week) — 🟡 RISING (rage rate 2.2%, still <5% threshold ✅)
- **Dead clicks:** 1,337 unique (+12.7% vs W41 ~1,186/week) — 🔴 ESCALATING (dead rate 10.7% of 12,488 visitors — ABOVE 10% threshold ⚠️)

**W42 Alert:** Dead rate re-crossed 10% threshold after W41 dipped to 9.8%. Both rage and dead trending upward 3rd consecutive week. Journey Task partial recovery (29 unique, up from 18 W41) — UX fix may be in progress.

---

## W42 Dead click hotspots

All dead clicks on consult.cadabams.com (app). SEO website (mindtalk.in) clean.

| URL (condensed) | Dead clicks (W42) | Status | Likely cause |
|---|---:|---|---|
| consult.cadabams.com/home | 649 | 🔴 CRITICAL #1 (persistent W34+) | App home — broken CTAs; 649 down from W37 peak 789 but still dominant |
| consult.cadabams.com/consult/appointments | 269 | 🔴 ESCALATING ⬆️ | Appointments page — was 246 W37, now 269 W42; growing 3 weeks |
| consult.cadabams.com/auth/login | 158 | 🔴 CRITICAL | Login wall friction — persistent 10+ weeks |
| consult.cadabams.com/consult/find-therapist | 130 | 🔴 PERSISTENT (W27+, 15+ weeks) | Filter/CTA non-responsive. On watchlist since W27. Not resolved in 15+ weeks. |
| consult.cadabams.com/assessments/[details] | 78 | 🟡 HIGH | Specific assessment details page broken |
| consult.cadabams.com/consult/checkout | 76 | 🔴 REVENUE CRITICAL | Checkout form issues — direct revenue impact |

---

## W42 Rage click hotspots — NEW CRITICAL

| URL (condensed) | Rage clicks (W42) | Status | Likely cause |
|---|---:|---|---|
| /worksheets/v270kfrkogycucbf4r74yulz/details | 233 | 🔴 NEW CRITICAL — HIGHEST EVER SINGLE PAGE | Worksheet detail page — unknown worksheet. 233 rage = users hammering non-responsive element. Possible worksheet content loading failure or button broken |
| consult.cadabams.com/consult/booking/8796 | 111 | 🔴 PERSISTENT (W27+, 15+ weeks) | booking/8796 has been on critical list since W27 — NEVER RESOLVED |
| consult.cadabams.com/consult/booking/20388 | 23 | 🟡 NEW W42 | New booking page joining rage list |
| consult.cadabams.com/home | 23 | 🟡 HIGH | Home page dual-friction (dead + rage) |
| consult.cadabams.com/consult/booking/86710 | 13 | 🟡 WATCH | Booking page cluster |

---

## Critical connection: Journey Task partial recovery

Started Journey Task: 645 (W34) → 365 (W35) → 124 (W36) → 30 (W37) → 27 (W39) → 18 (W41) → **29 (W42, +61% WoW)**

First positive recovery signal in 8 weeks. W42 29 starts vs W41 18 = +61% WoW. Journey UX may be receiving fixes. Monitor W43 for continuation.

---

## Most urgent dev actions (W42)

**Priority 1 — NEW CRITICAL:** `/worksheets/v270kfrkogycucbf4r74yulz/details` (233 rage clicks)
- Highest single-page rage click count ever recorded on a worksheet page
- 233 rage = users actively frustrated with non-responsive element
- Action: audit that specific worksheet's interactive elements; check if worksheet buttons/navigation are broken; check if this is a recently published worksheet with a broken CTA

**Priority 2 — EMERGENCY (15+ weeks):** `/consult/booking/8796` (111 rage, PERSISTENT W27+)
- Has been on watchlist since W27 — FIFTEEN weeks without resolution
- 111 rage clicks = booking flow at this specific therapist URL is broken
- Action: check if booking/8796 therapist is still active; test booking flow end-to-end

**Priority 3 — ESCALATING:** `/consult/appointments` (269 dead clicks, rising W37→W42)
- Was 246 W37, now 269 W42 = slow escalation, not improving
- Users hitting appointments page are unable to interact with scheduler
- Action: test appointments scheduling UI; check for JS errors in appointments view

**Priority 4 — PAYMENT FUNNEL:** `/consult/checkout` (76 dead clicks)
- Checkout dead clicks are REVENUE CRITICAL — users reaching checkout can't proceed
- Action: test checkout flow end-to-end; check for form field/button rendering issues

**Priority 5 — AUTH WALL:** `/auth/login` (158 dead clicks, PERSISTENT)
- Login wall sustained friction — 10+ weeks without resolution
- Action: check auth/login page for dead CTA elements, loading state issues

**Priority 6 — PERPETUAL:** `/consult/find-therapist` (130 dead clicks, W27+ = 15+ weeks)
- Still broken after 15+ weeks. Second-most persistent unresolved issue after booking/8796.

---

## Historical trend

| Week | Rage clicks (unique) | Dead clicks (unique) | Dead rate | Status |
|---|---:|---:|---:|---|
| W27 | ~200 est | ~1,800 est | ~28% | ESCALATING |
| W34 | ~400 est | 4,441 total | ~47% | 🔴 CRITICAL spike (total, not unique) |
| W35 | 479 | 3,761 | — | ✅ Improving |
| W37 | 729 | 4,635 total | — | 🔴 RE-ESCALATING |
| W39 | 247 | 1,141 | 11.1% | 🔴 HIGH (switching to unique tracking) |
| W41 (14d/2) | ~245/week | ~1,186/week | 9.8% | 🟡 BELOW THRESHOLD (first time since W36) |
| **W42** | **272** | **1,337** | **10.7%** | 🔴 **ABOVE THRESHOLD AGAIN** |

**Trend:** 3rd consecutive week of unique dead click growth. Dead rate re-crossed 10% after brief improvement in W41. New crisis: /worksheets rage (233) is unprecedented for that page type.
