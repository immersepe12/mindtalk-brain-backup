# Page Conversion Map — Updated 2026-07-29 (W31)

**Written by:** T19 Conversion Intelligence (Wed 11:00 IST) — overwritten each week.
**Read by:** T10 Strategist, T18 Professional Input, T12 Learner.
**Source:** Mixpanel project 4011856 (unified: mindtalk.in + consult.cadabams.com + app), trailing 7d Jul 22–28.
**Intent signal:** `book_appointment_clicked` (total events) ÷ unique page visitors. Multi-click users inflate rate above 100%; read as relative intensity.

> **W31 data period:** Jul 22–28, 2026. Unique visitors 8,258 (+29.1% vs W28's 6,396).
>
> **⚠️ ADS RE-ACTIVATED (Pan-India Plan, ~W29+).** New Google Ads campaigns (NND_Psychologist, FTA_Professional_Therapist, fta_generic_couple_bangalore, depression_treatment, anxiety_center) running on /experts/* and /lps/* pages. form_submitted surged 5→103 (+1,960%), 92% paid. Visitor surge (+29%) driven by ad traffic. W29+W30 were MCP_DOWN/BLOCKED — 3-week data gap. All WoW comparisons are W31 vs W28.
>
> **REVENUE RECORDS BROKEN.** Payment Successful 193 (+63.6% vs W28). Appointment Booked 232 (+116.8% vs W28). Best revenue week since T19 tracking began. Mix of organic growth + paid reactivation. UTM chain broken on new expert-page ad LPs (215/232 appointments = undefined UTM — cannot cleanly attribute).
>
> **ORGANIC BOOK CLICKS +7.9%.** Organic book clicks: 1,249→1,348. Organic share paradoxically up: 60.5%→67.9% (new ad campaigns land on expert/LP pages without book_appointment_clicked).
>
> **INTENT RATE DILUTED.** Site-wide: 32.3%→24.1% (-8.2pp). Denominator inflation from +2k ad visitors who submit forms instead of clicking book. Organic intent volume healthy.
>
> **chatgpt.com +31% to 203 book clicks.** Pattern 5 Week 5 confirmation.
>
> **GEOGRAPHIC DIVERSIFICATION.** Bengaluru share: 60.2%→51.3%. Mumbai +36%, Delhi +49%, Kolkata +200%, US market ~100 clicks (new category).
>
> **Pattern 7 (Homepage hero) DEMOTED.** Homepage hero payments 9→0. Not sustained.
>
> **NEW CRITICAL UX: /prescriptions** — 887 dead + 127 rage = 1,014 friction events. Highest UX problem in T19 history. Page is functionally broken.

---

## Site-level W31 snapshot (Jul 22–28)

| Metric | W31 | W28 | WoW (vs W28) |
|---|---:|---:|---|
| Unique visitors (site) | 8,258 | 6,396 | +29.1% ⬆️ (ads) |
| book_appointment_clicked (total) | 1,986 | 2,065 | -3.8% |
| lp_form_submitted | 56 | 136 | -58.8% 🔴 |
| whatsapp_clicked | 161 | 136 | +18.4% ✅ |
| call_clicked | 74 | 67 | +10.4% ✅ |
| form_submitted | 103 | 5 | +1,960% 🔥 (92% paid) |
| All intent events | ~2,380 | ~2,409 | ~flat |
| Payment Successful | 193 | 118 | +63.6% 🔥🔥 |
| Appointment Booked | 232 | 107 | +116.8% 🔥🔥 |
| Site-wide intent rate (book/uv) | 24.1% | 32.3% | -8.2pp (denominator dilution) |
| mindtalk_web-attributed payments | 15 | 22 | -31.8% 🔴 |
| mindtalk_web-attributed bookings | 15 | 22 | -31.8% 🔴 |

**Note:** Revenue surge is real but cause is mixed. Ads re-activated driving form_submitted + appointments via expert pages. Organic contribution solid (doctor card 13 for 5th week). Homepage hero 9→0 explains mindtalk_web decline.

---

## Paid vs organic breakdown W31

| Event | Total | Paid (google/GMB/etc) | Organic-attributable | mindtalk_web |
|---|---:|---:|---:|---:|
| book_appointment_clicked | 1,986 | 638 (32.1%) | 1,348 (67.9%) | ~11 est |
| lp_form_submitted | 56 | ~53 (~94%) | ~3 (6%) | 0 |
| whatsapp_clicked | 161 | ~92 (~57%) | ~69 (43%) | 0 |
| call_clicked | 74 | ~42 (~57%) | ~32 (43%) | 0 |
| form_submitted | 103 | ~95 (~92%) | ~8 (8%) | 0 |
| Payment Successful | 193 | 2 (1.0%) | 191 (99%) | 15 (7.8%) |
| Appointment Booked | 232 | 2 (0.9%) | 230 (99.1%) | 15 (6.5%) |

**Paid book breakdown:** google(331)+Google(116)+GMB(145)+gmb(7)+sitelink(5)+meta(13)+ig(8)+paid(13) = 638.
**Organic book clicks:** 1,348 (+7.9% vs W28's 1,249). Steady growth.
**mindtalk_web decline:** 22→15. Homepage hero 9→0. Doctor card stable at 13. New "bottom" CTA: 2.

---

## 6-Layer Attribution Breakdown (W31 — book_appointment_clicked, utm_source)

| Layer | Events | Share | WoW (vs W28) |
|---|---:|---:|---|
| chatgpt.com (utm_source, AI first-touch) | 203 | 10.2% | +31% 🔥 |
| perplexity | 1 | 0.1% | -83% |
| **Total AI search** | **204** | **10.3%** | **+26.7%** |
| undefined (organic + direct mixed) | 1,045 | 52.6% | stable |
| direct | 87 | 4.4% | stable |
| Android search (an) | 12 | 0.6% | stable |
| Paid (Google/GMB/meta/ig/sitelink/paid) | 638 | 32.1% | share declining |

**By initial referring domain (first-ever visit):** Google 1,541 / Direct 329 / chatgpt.com 32 / Android search 22 / Bing 13 / Social 21 / Gemini 7 / mindtalk.in 8 / claude.ai 3 / Google Translate 3.

---

## UTM attribution (mindtalk_web — Week 5)

**Payment Successful by utm_medium (W31):**
| Medium | Payments | Share | WoW | Cumulative (5wk) |
|---|---:|---:|---|---:|
| doctor | 13 | 86.7% | flat | 55 |
| bottom | 2 | 13.3% | 🆕 new | 2 |
| homepage/hero | 0 | 0% | -9 🔴 | 15 |
| **Total mindtalk_web** | **15** | **100%** | **-31.8%** | **72** |

**Doctor card 5-week record:** 13/9/13/13/13 payments — most reliable attribution signal.
**Homepage hero DROPPED 9→0:** Pattern 7 demoted. Investigate homepage UTM.
**Bottom CTA (2):** New. Possibly bottom of illness/blog page. Track W32.

---

## 🟢 Goldmines — protect + amplify

| URL/Section | Visitors est/wk | book clicks | Intent rate | Revenue validated | WoW |
|---|---:|---:|---:|---|---|
| /doctors/* (all) | ~1,100 est | ~1,000+ | 90%+ | 13 payments (doctor_card, W31) | Stable 5 weeks ✅ |
| /doctors (main listing) | ~90 est | ~380+ | ~420%+ | Bengaluru 51% of intent | Stable |
| /experts/* (all) | ~900+ est | ~460+ | 50%+ | form_submitted 95 paid + appointments unclear | Ads running |

**Strategy:** No risky changes. 55 confirmed doctor card payments over 5 weeks = highest-confidence attribution. Every blog/illness internal link → /doctors and /experts.

---

## 🟡 Rockets — high intent, grow traffic

| URL | Visitors est/wk | Intent rate est | WoW geo signal | Notes |
|---|---:|---:|---|---|
| /doctors/telugu-speaking-doctors | ~80 est | ~78% | Hyderabad 99 (stable) | Pattern 1 CONFIRMED 5 WEEKS |
| /doctors/tamil-speaking-doctors | ~75 est | ~71% | Tamil Nadu 83, Chennai 65 | Pattern 1 CONFIRMED 5 WEEKS |

**T5 URGENT (5 weeks — fire immediately at +30 priority):**
1. Malayalam-speaking doctors page (Kerala 20 W31, P8 Week 2)
2. Kannada-speaking doctors page (Karnataka still 53% of all intent)
3. Hindi-speaking doctors page (Delhi NCT +49.4%, 121 book clicks)
4. **NEW — P10 US/NRI page:** California 26, San Francisco 16, Texas 16, Illinois 15 (~100 US book clicks — first major week)

---

## 🔵 Engagement Engines — top-of-funnel discovery

| URL/Section | Visitors est/wk | Direct booking | Role |
|---|---:|---|---|
| /blogs/* | ~1,200+ est | ~0 (0%) | Pattern 3 CONFIRMED 5 WEEKS. Top-of-funnel only. |

---

## 🟠 Homepage — tracking gap / Pattern 7 DEMOTED

| URL | Visitors est/wk | book_appointment_clicked | Revenue via UTM |
|---|---:|---:|---:|
| / (homepage) | ~320 est | 0 (tracking gap) | **0 payments W31 (vs 9 W28)** |

**Pattern 7 DEMOTED.** Homepage hero did not sustain. Investigate: (a) CTA removed/changed, (b) UTM tagging broken, (c) W28 anomaly. Do not classify as Goldmine.

---

## ⚫ Dead weight for direct booking intent

| URL/Section | Visitors est/wk | book clicks | Notes |
|---|---:|---:|---|
| /illnesses/* | ~110 est | ~0 | Tracking gap. SEO equity: keep. |
| /treatments/* | ~240 est | ~0 | Tracking gap. SEO equity: keep. |
| /lps/* | ~420 est | ~53 apparent | ~94% paid. Organic ~3/wk. |

---

## ⚠️ UX Friction W31 — CRITICAL ESCALATIONS

| URL | Rage | Dead | Total | Severity | WoW |
|---|---:|---:|---:|---|---|
| consult.cadabams.com/prescriptions | 127 | 887 | 1,014 | 🔴🔴 NEW CRITICAL #1 | Brand new — page broken |
| consult.cadabams.com/home | 38 | 673 | 711 | 🔴🔴 ESCALATING | Dead: 129→673 (+421%) |
| consult.cadabams.com/consult/find-therapist | 47 | 372 | 419 | 🔴 HIGH PERSISTENT | Dead: 319→372 (+16.6%) |
| consult.cadabams.com/consult/appointments | ~0 | 160 | 160 | 🟡 IMPROVING | 237→160 (-32.5%) ✅ |
| consult.cadabams.com/consult/checkout | ~4 | 69 | 73 | 🔴 PERSISTENT | 68→69, stuck |
| consult.cadabams.com/consult/booking/8796 | 36 | ~50 | ~86 | 🟡 IMPROVING | Rage: 96→36 ✅ |
| journeys/cmraiwmuz*/details | 0 | 75 | 75 | 🟡 MEDIUM | Journey page friction |
| consult.cadabams.com/assessments/* | ~0 | 52 | 52 | 🟡 MEDIUM | New |

**Priority:** (1) /prescriptions — escalate to dev NOW; (2) /home dead click surge — needs immediate investigation; (3) find-therapist still not fixed after 4 weeks; (4) checkout still stuck.

---

## Caveats for downstream tasks

1. Revenue: 193 payments / 232 bookings = record highs, but mix of organic + paid (ads re-activated ~W29).
2. UTM chain broken on new expert-page ad campaigns — 215/232 appointments = undefined.
3. 3-week data gap (W29 MCP_DOWN, W30 MCP_BLOCKED). W31 vs W28 is 3-week delta.
4. Visitor surge (+29.1%) includes ad-driven traffic — intent rate denominator inflated.
5. mindtalk_web attribution decline: homepage hero 9→0. Doctor card rock-solid.
6. US market (~100 book clicks): no US-specific content exists. Pure organic/NRI.
7. GA4 SKIPPED — Supermetrics trial expired.
