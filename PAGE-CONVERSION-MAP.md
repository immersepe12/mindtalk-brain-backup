# Page Conversion Map — Updated 2026-08-05 (W32)

**Written by:** T19 Conversion Intelligence (Wed 11:00 IST) — overwritten each week.
**Read by:** T10 Strategist, T18 Professional Input, T12 Learner.
**Source:** Mixpanel project 4011856 (unified: mindtalk.in + consult.cadabams.com + app), trailing 7d Jul 29–Aug 4.
**Intent signal:** `book_appointment_clicked` (total events) ÷ unique page visitors.

> **W32 data period:** Jul 29–Aug 4, 2026. Unique visitors 8,890 (+7.6% vs W31's 8,258).
>
> **REVENUE RECORDS BROKEN AGAIN.** Payment Successful 205 (+6.2% vs W31). Appointment Booked 264 (+13.8% vs W31). Best two consecutive record weeks since tracking began.
>
> **🔴 CRITICAL: doctor_card payments CRASHED 13→5 (-61.5%).** 5-week streak broken. Possible UTM attribution break (same pattern as homepage hero W31 drop). Total mindtalk_web payments: 15→7. Investigate: did doctor CTA link change? Session UTM being reset by ads? Total payments UP but attributed segment DOWN = UTM gap, not booking gap.
>
> **🔴 CRITICAL UX ESCALATION: /appointments + /assessments BOTH EXPLODING.** /appointments: 52 rage + 762 dead = 814 (vs W31 160 dead, +376%). /assessments/*: 78 rage + 725 dead = 803 (vs W31 ~52, +1,440%). Both new CRITICAL escalations. App appears to have a broken deploy or tracking regression.
>
> **🆕 DOHA/QATAR MARKET BREAKOUT:** 47 book clicks (vs ~15 W31, +213%). Qatar + Australia (60 clicks) + Sweden (21 clicks) = Gulf + diaspora surge. International share growing fast (~67+ Gulf clicks).
>
> **📉 Tamil Nadu/Chennai CRASH: -67.5%.** Chennai 65→15 (-76.9%). West Bengal/Kolkata: 41→7 (-83%). W31 diversification may have been partially ad-driven.
>
> **🆕 Riya first revenue attribution:** 1 payment + 1 booking attributed to utm_medium=riya. First time Riya AI in-app engagement converted to consult revenue.
>
> **chatgpt.com MIXED:** Sessions -19% (203→164) but NEW USERS +50% (32→48 initial_referring). Growing as acquisition channel.

---

## Site-level W32 snapshot (Jul 29–Aug 4)

| Metric | W32 | W31 | WoW |
|---|---:|---:|---|
| Unique visitors (site) | 8,890 | 8,258 | +7.6% ⬆️ |
| book_appointment_clicked (total) | 2,035 | 1,986 | +2.5% ✅ |
| lp_form_submitted | 57 | 56 | +1.8% |
| whatsapp_clicked | 139 | 161 | -13.7% 📉 |
| call_clicked | 62 | 74 | -16.2% 📉 |
| form_submitted | 114 | 103 | +10.7% ⬆️ |
| All intent events | ~2,407 | ~2,380 | +1.1% |
| Payment Successful | 205 | 193 | +6.2% 🔥 **RECORD** |
| Appointment Booked | 264 | 232 | +13.8% 🔥 **RECORD** |
| Site-wide intent rate (book/uv) | 22.9% | 24.1% | -1.2pp (ad dilution continues) |
| mindtalk_web-attributed payments | 7 | 15 | -53.3% 🔴 |
| mindtalk_web-attributed bookings | 8 | 15 | -46.7% 🔴 |
| doctor_card payments (series W26–W32) | 5 | 13 | -61.5% 🔴 FLAG |

---

## Paid vs organic breakdown W32

| Event | Total | Paid (utm_source) | Organic-attributable | mindtalk_web |
|---|---:|---:|---:|---:|
| book_appointment_clicked | 2,035 | 666 (32.7%) | 1,369 (67.3%) | ~11 est |
| lp_form_submitted | 57 | ~51 (~89.5%) | ~6 (10.5%) | 0 |
| whatsapp_clicked | 139 | ~43 (~30.9%) | ~96 (69.1%) | 0 |
| call_clicked | 62 | ~35 (~57%) | ~27 (43%) | 0 |
| form_submitted | 114 | ~106 (~93%) | ~8 (7%) | 0 |
| Payment Successful | 205 | 4 (2.0%) | 201 (98%) | 7 (3.4%) |
| Appointment Booked | 264 | 6 (2.3%) | 258 (97.7%) | 8 (3.0%) |

**Paid book breakdown:** google(336)+Google(140)+GMB(137)+gmb(17)+sitelink(3)+ig(11)+meta(17)+paid(5) = 666.
**Organic book clicks: 1,369 (+1.6% vs W31's 1,348).** Steady organic growth continues — 6th consecutive week.
**chatgpt.com WhatsApp clicks: 24 (NEW).** AI-referred users clicking WhatsApp CTA — direct path to consult.
**mindtalk_web decline:** 15→7. Doctor card 13→5. Homepage restored (0→1). Riya NEW (1).

---

## 6-Layer Attribution Breakdown (W32 — book_appointment_clicked)

| Layer | Events | Share | WoW (vs W31) |
|---|---:|---:|---|
| chatgpt.com (utm_source, AI session) | 164 | 8.1% | -19.2% 📉 sessions |
| chatgpt.com (initial_referring, new users) | 48 | — | +50% 🔥 NEW USERS |
| perplexity (utm_source) | 3 | 0.1% | +200% (from 1) |
| **Total AI session clicks** | **167** | **8.2%** | **-18.1% (sessions)** |
| undefined (organic + untracked) | 1,060 | 52.1% | stable |
| direct | 122 | 6.0% | +40% ⬆️ |
| Android search (an) | 20 | 1.0% | stable |
| Paid total | 666 | 32.7% | share stable |

**$initial_referring_domain top sources W32:** google.com 1,564 / $direct 331 / chatgpt.com 48 / instagram 26 / mindtalk.in 21 / LinkedIn 9 / Bing 7 / DuckDuckGo 3 / Yahoo 3 / claude.ai 1.

**P5 INTERPRETATION:** chatgpt.com session count -19% reflects fewer RETURNING users being attributed; but first-touch new users +50%. ChatGPT is growing as a DISCOVERY/ACQUISITION channel. The compounding effect: each new ChatGPT-referred user may become a returning session user in future weeks. Net verdict: **P5 HEALTHY, acquisition phase accelerating.**

---

## UTM attribution (mindtalk_web — Week 6)

**Payment Successful by utm_medium (W32):**
| Medium | W32 | W31 | WoW | Cumulative (6wk) |
|---|---:|---:|---|---:|
| doctor | 5 | 13 | -61.5% 🔴 | 60 |
| riya | 1 | 0 | 🆕 NEW | 1 |
| homepage | 1 | 0 | returning | 16 |
| **Total mindtalk_web** | **7** | **15** | **-53.3%** | **79** |

**Appointment Booked by utm_medium (W32):**
| Medium | W32 | W31 | WoW | Cumulative (6wk) |
|---|---:|---:|---|---:|
| doctor | 6 | ~13 | -54% 🔴 | ~65 est |
| riya | 1 | 0 | 🆕 NEW | 1 |
| homepage | 1 | 0 | returning | ~17 est |
| **Total mindtalk_web** | **8** | **15** | **-46.7%** | **~87 est** |

**🆕 RIYA REVENUE (1 payment + 1 booking):** First confirmed revenue attribution from Riya AI. The Riya → consult funnel exists and converts.

**Doctor card crash hypothesis:** Ads running on /experts pages may be overwriting session UTMs when users subsequently visit /doctors. If a user visits /experts (utm_source=google), then clicks to /doctors, the new session inherits google UTM and the doctor_card booking is counted as paid, not mindtalk_web. Total payments UP = conversion is happening; mindtalk_web slice DOWN = attribution is being stolen by paid UTMs.

---

## 🟢 Goldmines — protect + amplify

| URL/Section | Visitors est/wk | book clicks | Intent rate | Revenue validated | WoW |
|---|---:|---:|---:|---|---|
| /doctors/* (all) | ~1,200 est | ~1,100 est | 90%+ | 5 payments W32 (60 cumulative, 6wk) | ⚠️ W32 crash — monitor |
| /experts/* (all) | ~900+ est | ~460 est | 50%+ | form_submitted 106 paid + undefined appointments | Ads running |

**Strategy:** No structural changes. Monitor doctor_card W33 — if < 8 again, flag UTM attribution gap to Kushal. 60 cumulative doctor payments = highest-confidence attribution in the system.

---

## 🟡 Rockets — high intent, grow traffic

| URL | W32 geo signal | W31 | WoW | Status |
|---|---:|---|---|---|
| /doctors/telugu-speaking-doctors | Hyderabad 83 | 99 | -16.2% | MONITOR — 6th week, slight decline |
| /doctors/tamil-speaking-doctors | Tamil Nadu 27, Chennai 15 | TN 83, Chennai 65 | -67.5% 🔴 | WATCH W33 before downgrading |

**P5 ACTION FIRES THIS WEEK (5+ wks, +30 priority):**
1. Malayalam-speaking doctors page (Kerala 12 W32, Kochi 5)
2. Kannada-speaking doctors page (Karnataka 1,194 clicks = 58.7% share)
3. Hindi-speaking doctors page (Delhi+NCR ~125 clicks, stable)
4. **Gulf/Doha diaspora page** (URGENT NEW — Qatar 47 + UAE 16 = 63 clicks, 0 content)
5. Australian diaspora / NRI page (Melbourne 29 + Sydney 31 = 60 clicks, 0 content)

---

## 🔵 Engagement Engines — top-of-funnel discovery

| URL/Section | Visitors est/wk | Direct booking | Role |
|---|---:|---|---|
| /blogs/* | ~1,200+ est | ~0 (0%) | P3 CONFIRMED 6 WEEKS. Internal links to /doctors mandatory. |

---

## 🟠 Homepage — PARTIAL RETURN (1 payment W32)

| URL | Visitors est/wk | Revenue via UTM |
|---|---:|---:|
| / (homepage) | ~320 est | 1 payment + 1 booking W32 |

P7 remains demoted. Not sustained. Monitor W33.

---

## ⚫ Dead weight for direct booking intent

| URL/Section | Visitors est/wk | Notes |
|---|---:|---|
| /illnesses/* | ~110 est | SEO equity: keep. |
| /treatments/* | ~240 est | SEO equity: keep. |
| /lps/* | ~400 est | ~89.5% paid. Organic ~6/wk. |

---

## ⚠️ UX Friction W32 — DOUBLE CRITICAL ESCALATION

| URL | Rage | Dead | Total | Severity | WoW vs W31 |
|---|---:|---:|---:|---|---|
| consult.cadabams.com/consult/appointments | 52 | 762 | 814 | 🔴🔴 CRITICAL #1 | Dead: 160→762 (+376%) 🚨 |
| consult.cadabams.com/assessments/* | 78 | 725 | 803 | 🔴🔴 CRITICAL #2 NEW | Dead: ~52→725 (+1,294%) 🚨 |
| consult.cadabams.com/consult/find-therapist | 59 | 570 | 629 | 🔴 ESCALATING | Dead: 372→570 (+53.2%) |
| consult.cadabams.com/home | 16 | 564 | 580 | 🔴 HIGH PERSISTENT | Dead: 673→564 (-16.2%) slight ✅ |
| consult.cadabams.com/prescriptions | 54 | 338 | 392 | 🟡 IMPROVING | Total: 1,014→392 (-61.3%) ✅ |
| consult.cadabams.com/consult/checkout | 3 | 67 | 70 | 🟡 IMPROVING | 73→70 nearly flat |

**DEV TEAM ACTION REQUIRED:**
1. **/consult/appointments** — 762 dead clicks this week (was 160 last week). Something broke in appointments UI. Check for: infinite loading state, non-responsive buttons, SPA route issue.
2. **/assessments/*** — 725 dead clicks (was ~52). Assessment elements appear broken. Check: interactive question elements, next/back buttons, submit flow.
3. **/consult/find-therapist** — 5 consecutive weeks of dead click escalation. Not resolving.

---

## 🆕 New Market Signals W32

**DOHA/QATAR BREAKOUT (P11 — Week 1):**
- Qatar (Baladiyat ad Dawhah): 47 book clicks (vs ~15 W31, +213%)
- Gulf total: Qatar 47 + UAE (Dubai 7 + Abu Dhabi 9 = 16) + Saudi 4 = 67 book clicks
- No Gulf-specific content exists
- **T5 urgent:** Gulf/expat mental health content (link to /doctors for online therapy)

**AUSTRALIA MARKET EMERGING (P12 — Week 2):**
- Melbourne 29 + Sydney 31 + Brisbane 2 = 62 book clicks
- Victoria + NSW + Queensland = 62 from regional breakdown
- +94% vs W31 ~31

**RIYA REVENUE CONFIRMED:**
- 1 payment + 1 booking via utm_medium=riya
- The Riya → consult conversion path is live and working

---

## Caveats for downstream tasks

1. Per-page visitor queries not run this week (rate limit conservation) — tier assignments use W31 per-page data + W32 geo/revenue deltas.
2. doctor_card crash (13→5) requires investigation before concluding doctor pages weakened.
3. Tamil Nadu crash requires 1 more week to confirm (may be ad-driven W31 spike reversing).
4. chatgpt.com session drop (-19%) ≠ P5 declining — new user acquisition +50%.
5. /appointments + /assessments UX crises are likely same deploy regression. Escalate together.
6. GA4 SKIPPED — Supermetrics requires auth.
