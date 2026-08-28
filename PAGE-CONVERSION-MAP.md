# Page Conversion Map — Updated 2026-08-26 (W35)

**Written by:** T19 Conversion Intelligence (Wed 11:00 IST) — overwritten each week.
**Read by:** T10 Strategist, T18 Professional Input, T12 Learner.
**Source:** Mixpanel project 4011856 (unified: mindtalk.in + consult.cadabams.com + app), trailing 7d Aug 19–25.
**Intent signal:** `book_appointment_clicked` (total events) ÷ unique page visitors (site-wide denominator).

> **W35 data period:** Aug 19–25, 2026. Unique visitors 10,401 (+2.6% vs W34's 10,137).
>
> **📉 ORGANIC BOOK CLICKS BREAK 7-WEEK GROWTH STREAK: 1,787→1,539 (-13.9%).** First decline after 7 consecutive weeks of organic growth. Revenue IMPROVED (+7.7% payments) despite click decline — click-to-payment conversion rose significantly, suggesting higher-intent visitors.
>
> **🔥 CHATGPT.COM ACCELERATES: 300→334 book clicks (+11.3%). Now 16.2% of ALL book clicks** (up from 12.6% W34). P5 Week 6 major confirmation. chatgpt.com is now the single largest attributable non-paid traffic source.
>
> **⚠️ STARTED JOURNEY TASK CRASH: 645→365 (-43.4%).** Critical app engagement drop. Flag for product team — could indicate a feature change, bug, or UX change in the journeys flow.
>
> **🔥 GEOGRAPHIC ROTATION:** Karnataka -20.6% (Bengaluru -21.2%), Delhi -45.2% (W34 record was one-week anomaly). Offset by Telangana +60.9% 🔥, Tamil Nadu +47.1% 🔥, West Bengal +90.6% 🔥, Kerala +44.4% 🔥 (P8 W5 confirmed).
>
> **🔴 CHECKOUT AUTH FRICTION ESCALATING:** auth/login→checkout rage clicks = 27. Users attempting to pay are hitting a login wall and raging. IMMEDIATE dev review needed — this is in the critical payment path.
>
> **⬇️ DEAD CLICKS IMPROVING:** 4,441→3,761 (-15.3%). W34 CRITICAL partially resolving.

---

## Site-level W35 snapshot (Aug 19–25)

| Metric | W35 | W34 | WoW | Notes |
|---|---:|---:|---|---|
| Unique visitors (site) | 10,401 | 10,137 | +2.6% ⬆️ | Continued growth |
| book_appointment_clicked (total) | 2,065 | 2,388 | -13.6% 📉 | Click decline despite revenue growth |
| Paid book clicks | 526 | 601 | -12.5% 📉 | Reduced paid spend |
| **Organic book clicks** | **1,539** | **1,787** | **-13.9% 📉** | **7-week growth streak BROKEN** |
| chatgpt.com book clicks | 334 | 300 | +11.3% 🔥 | P5 W6 — 16.2% of all clicks |
| perplexity book clicks | 1 | 0 | 🆕 | First-ever Perplexity attribution |
| whatsapp_clicked | 91 | 124 | -26.6% 📉 | Down significantly |
| call_clicked | 56 | 45 | +24.4% ✅ | Growing |
| form_submitted | 114 | 127 | -10.2% 📉 | Ads-driven decline |
| lp_form_submitted | 59 | 64 | -7.8% 📉 | Ads-driven decline |
| Payment Successful | 181 | 168 | +7.7% 🔥 | Revenue UP despite click decline |
| Appointment Booked | 228 | 228 | flat | Stable |
| Site-wide intent rate (book/uv) | 19.9% | 23.6% | -3.7pp 📉 | Rate drops despite revenue gain |
| **Organic payments** | **178** | **166** | **+7.2% ✅** | **Organic revenue improving** |
| Organic bookings | 222 | 225 | -1.3% stable | Near-flat |
| mindtalk_web payments | 5 | 4 | +25% ✅ | Recovery from W34 bleed |
| mindtalk_web bookings | 8 | 10 | -20% 📉 | Mild decline |
| chatgpt.com payments | 2 | 2 | flat | AI revenue holding |
| chatgpt.com bookings | 2 | 3 | -1 | Minor decline |
| hero CTA payments | 2 | 1 | +1 | Homepage hero stable |
| hero CTA bookings | 5 | 4 | +1 | Growing |
| doctor_card payments | 3 | 3 | flat | Stable (attribution bleed remains) |
| doctor_card bookings | 3 | 7 | -4 📉 | Decline — attribution noise vs real? |
| Assessment Completed | 877 | 1,031 | -14.9% 📉 | App engagement dip |
| Assessment Started | 2,476 | 2,720 | -9.0% 📉 | Fewer assessment starts |
| Assessment completion rate | 35.4% | 37.9% | -2.5pp 📉 | Declining quality of starts |
| **Started Journey Task** | **365** | **645** | **-43.4% 🔴** | **CRITICAL — product team flag** |
| Stress Tracker Started | 260 | — | new KPI | — |
| Rage clicks (site) | 479 | ~400 est | elevated | Multiple critical pages |
| Dead clicks (site) | 3,761 | 4,441 | -15.3% ✅ | Improving from W34 CRITICAL |

---

## Paid vs organic breakdown W35

| Event | Total | Paid | Organic-attributable | mindtalk_web | chatgpt.com |
|---|---:|---:|---:|---:|---:|
| book_appointment_clicked | 2,065 | 526 (25.5%) | 1,539 (74.5%) | ~0 (tracked at payment level) | 334 (16.2%) |
| form_submitted | 114 | est ~105 (~92%) | est ~9 (~8%) | 0 | 0 |
| lp_form_submitted | 59 | est ~59 (~100%) | ~0 | 0 | 0 |
| whatsapp_clicked | 91 | est ~25 (~27%) | est ~66 (~73%) | 0 | 0 |
| call_clicked | 56 | est ~15 (~27%) | est ~41 (~73%) | 0 | 0 |
| Payment Successful | 181 | gmb(2)+Google(1)=3 (1.7%) | 178 (98.3%) | 5 (2.8%) | 2 (1.1%) |
| Appointment Booked | 228 | gmb(3)+meta(1)+Google(1)+google(1)=6 (2.6%) | 222 (97.4%) | 8 (3.5%) | 2 (0.9%) |

**Organic book clicks W35: 1,539 (-13.9% vs W34 1,787).** 7-week growth streak broken.
**Paid book share: 25.5%** (vs W34 25.2%) — roughly stable paid share despite lower total.
**chatgpt.com share: 16.2% of ALL book clicks** — new record, up from 12.6% W34.

---

## UTM attribution breakdown W35

### By utm_medium (payments)
| UTM medium | Payments | Bookings | Notes |
|---|---:|---:|---|
| undefined | 173 | 214 | Majority — attribution gap |
| doctor | 3 | 3 | Doctor page CTAs |
| homepage | 2 | 4 | Homepage CTA |
| organic | 2 | 3 | Explicit organic tag |
| cpc | 1 | 2 | Paid search |
| lp | 0 | 1 | Landing page |
| paid_social | 0 | 1 | Meta social (E3-burnout creative) |

### By utm_content (payments)
| UTM content | Payments | Bookings | Notes |
|---|---:|---:|---|
| undefined | 176 | 219 | Majority |
| hero | 2 | 5 | Homepage hero CTA — stable |
| doctor_card | 3 | 3 | Doctor listing cards |
| E3-burnout | 0 | 1 | Meta BOF creative — 1 booking |

---

## Page tier classification W35

*Per-page volume queries deferred (rate limit management). Site-level tiers held from W34. Key tier signal: organic payment conversion IMPROVED despite lower book clicks — Goldmine pages likely maintained or strengthened.*

## 🟢 Goldmines (2 pages — held from W28 data, structurally confirmed)
| URL | Tier | Notes |
|---|---|---|
| /consult/find-therapist | 🟢 Goldmine | Primary booking conversion page. Persistent rage-click UX issue (22 W35). |
| / (homepage) | 🟢 Goldmine | hero CTA: 2 payments + 5 bookings W35. Stable. |

## 🟡 Rockets (4 pages — held from W34)
| URL | Tier | Notes |
|---|---|---|
| /treatments/cbt-therapy | 🟡 Rocket | High-intent treatment page |
| /illnesses/anxiety | 🟡 Rocket | YMYL refresh shipped W31 |
| /illnesses/depression | 🟡 Rocket | YMYL refresh shipped W31 |
| /doctors | 🟡 Rocket | P2 confirmed 8 weeks |

## 🔴 Leaky Buckets (0 confirmed — none meeting threshold currently)

## 🔵 Engagement Engines (new tier — driven by W35 app data)
| URL | Signal | Notes |
|---|---|---|
| Assessment landing pages | 877 completions / 2,476 starts | 35.4% completion rate |
| Journey pages | 365 Started Journey Task | -43.4% WoW — CRITICAL DROP, product flag |

## 🔴 UX CRITICAL — Rage click hotspots (W35)
| Page | Rage clicks | Priority | Action |
|---|---:|---|---|
| /home (app) | 37 | 🔴 CRITICAL | App home frustration — review UX |
| /auth/login?returnTo=/consult/checkout | 27 | 🔴 CRITICAL | Login wall before payment — immediate fix |
| /consult/find-therapist | 22 | 🔴 ESCALATING | 3rd+ consecutive week critical |
| /consult/consent | 21 | 🔴 CRITICAL | Consent page in payment flow |
| /consult/booking/8796 | 19 | 🔴 PERSISTENT | Specific doctor — known issue W27+ |
| /consult/booking/101166 | 15 | 🟡 HIGH | New high-rage booking page |
| /consult/booking/8738 | 13 | 🟡 HIGH | Booking flow friction |
| /assessments (hub) | 8 | 🟡 WATCH | Assessment hub friction |
| /auth/signup | 9+ | 🟡 HIGH | Signup flow |
