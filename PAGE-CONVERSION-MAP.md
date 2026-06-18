# Page Conversion Map — Updated 2026-06-17 (INAUGURAL RUN)

**Written by:** T19 Conversion Intelligence (Wed 11:00 IST) — overwritten each week.
**Read by:** T10 Strategist, T18 Professional Input, T12 Learner.
**Source:** Mixpanel project 4011856 (Mindtalk website), trailing 7 days.
**Intent signal:** `book_appointment_clicked` (total) ÷ unique page visitors. book_appointment = ~89% of all booking-intent volume this week; lp_form_submitted (131), whatsapp_clicked (80), call_clicked (57), form_submitted (8) tracked at site level only this run.

> ⚠️ **LIMITED_BASELINE: true.** First run, 7 days of data. Top page = 298 visitors/wk, so the spec's absolute volume gates (Goldmine ≥500, Leaky ≥1000) are structurally unreachable this week. Volume gates **scaled to this week's distribution** (Goldmine vol ≥100, Rocket vol <100, Leaky vol ≥150, Dead vol <30). Re-evaluate after 4 weeks. No WoW diff (no prior week). No patterns confirmed (need ≥3 weeks).

**Median intent rate (classified set, 24 pages ≥30 visitors): 39.6%**
(Intent rate exceeds 100% on some pages because `book_appointment_clicked` is counted as total events ÷ unique visitors — multi-click users inflate it, per spec. Treat as relative intensity, not literal conversion %.)

---

## Tier definitions (inaugural-scaled volume gates)
| Tier | Condition (this run) | Strategy |
|---|---|---|
| 🟢 Goldmine | intent_rate ≥ median×1.5 AND visitors ≥ 100 | Protect + amplify |
| 🟡 Rocket | intent_rate ≥ median×2.0 AND visitors < 100 | Drive more traffic |
| 🔴 Leaky bucket | intent_rate < median×0.5 AND visitors ≥ 150 | T18 professional input + UX/instrumentation audit |
| ⚫ Dead weight | visitors < 30 OR intent_rate < median×0.2 | De-prioritize |
| ⚪ Average | Everything else | Standard treatment |

## 🟢 Goldmines (2) — protect + amplify
| URL | Visitors/wk | Book clicks | Intent rate | Note |
|---|---:|---:|---:|---|
| /doctors | 119 | 382 | 321% | Doctor-listing hub. Extreme booking intent per visitor. Protect, add internal links from blogs/illness pages. |
| /experts/expert-therapists | 138 | 85 | 62% | Paid-LP expert page, strong intent. Defend; no risky changes. |

## 🟡 Rockets (2) — drive more traffic (high intent, low volume)
| URL | Visitors/wk | Book clicks | Intent rate | Note |
|---|---:|---:|---:|---|
| /doctors/telugu-speaking-doctors | 37 | 35 | 95% | Language-specific doctor page converts hot. SEO refresh + internal links = high ROI. |
| /doctors/tamil-speaking-doctors | 35 | 32 | 91% | Same pattern. Strong candidate to replicate (kannada/malayalam/hindi speaking-doctor pages). |

## 🔴 Leaky bucket (1) — high traffic, low/zero tracked intent
| URL | Visitors/wk | Book clicks | Intent rate | Why? |
|---|---:|---:|---:|---|
| / (homepage) | 298 | 0 | 0% | Highest-traffic page, **zero** book_appointment_clicked events. Likely the homepage CTA fires a different event (not in intent set) or booking path isn't instrumented on `/`. **NEEDS INSTRUMENTATION CHECK** before treating as a true leak. |

## ⚫ Dead weight (6 of 24 classified) — de-prioritize for conversion
| URL | Visitors/wk | Book clicks | Note |
|---|---:|---:|---|
| /blogs/understanding-the-hamilton-anxiety-rating-scale | 95 | 0 | Informational blog, no booking CTA / no tracked intent |
| /blogs/guide-to-liebowitz-social-anxiety-scale | 46 | 0 | Assessment-scale explainer |
| /blogs/understanding-dominant-personality-and-dominating-nature | 42 | 0 | Top-of-funnel blog |
| /blogs/understanding-dry-begging-psychology-behind-indirect-requests | 37 | 0 | Top-of-funnel blog |
| /treatments/drug-deaddiction | 32 | 0 | Treatment page, 0 tracked intent — check CTA instrumentation |
| /blogs/exploring-the-intersection-of-blanking-out-and-adhd | 30 | 0 | Top-of-funnel blog |

(Blogs converting 0 booking intent is expected — discovery content. Their job is traffic + internal-link equity into the doctor/expert Goldmines, not direct bookings.)

## ⚪ Average (13) — standard treatment
Includes /centers/indiranagar (140v, 56%), /experts/expert-psychologists (136v, 38%), /experts/psychologists-in-indiranagar (210v, 33%), /lps/mental-health-treatments-therapies-in-bangalore (111v, 34%), plus other paid-LP + center pages near the 39.6% median.

---

## Caveats for downstream tasks (Strategist / T18 / T5)
1. **Homepage 0-intent is almost certainly a tracking gap, not a real leak** — verify instrumentation before acting.
2. **lp_form / whatsapp / call not yet per-page** — paid /lps/ + /experts/ pages are under-credited this week; their true intent is higher than shown.
3. Thresholds are inaugural-scaled. Don't hard-commit budget on a single week.
