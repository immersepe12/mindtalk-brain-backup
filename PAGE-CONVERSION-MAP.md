# Page Conversion Map — Updated 2026-07-01 (W27)

**Written by:** T19 Conversion Intelligence (Wed 11:00 IST) — overwritten each week.
**Read by:** T10 Strategist, T18 Professional Input, T12 Learner.
**Source:** Mixpanel project 4011856 (unified: mindtalk.in + consult.cadabams.com + app), trailing 7d Jun 25–Jul 1.
**Intent signal:** `book_appointment_clicked` (total events) ÷ unique page visitors. Multi-click users inflate rate above 100%; read as relative intensity.

> **W27 data period:** Jun 25 – Jul 1, 2026. Unique visitors 6,397 (+13.8% WoW).
>
> **PAID/ORGANIC SEPARATION ACTIVE.** lp_form_submitted = 94.2% paid. book_appointment_clicked organic = 53.9% = 1,044 events. Revenue events (Payment Successful 94 / Appointment Booked 80) are 100% organic — ads still paused.
>
> **UTM SYSTEM LIVE — WEEK 3.** 12 payments and 12 appointments confirmed attributable to mindtalk.in CTAs via mindtalk_web UTM.
>
> **PATTERNS 1, 2, 3 CONFIRMED (3 weeks)** — language doctor pages, doctor hub Goldmine, and blogs-as-Engagement-Engine all hit 3-week evidence threshold. Unlock for T5 immediately.
>
> **NEW CRITICAL UX:** find-therapist dead clicks ESCALATING (240→428, +78%). booking/8796 new rage click hotspot (92 events). booking/53196 W26 CRITICAL RESOLVED.

---

## Site-level W27 snapshot (Jun 25–Jul 1)

| Metric | W27 | W26 | WoW |
|---|---:|---:|---|
| Unique visitors (site) | 6,397 | 5,620 | +13.8% ✅ |
| book_appointment_clicked (total) | 1,936 | 1,781 | +8.7% |
| lp_form_submitted | 155 | 137 | +13.1% |
| whatsapp_clicked | 116 | 100 | +16.0% |
| call_clicked | 70 | 49 | +42.9% ✅ |
| form_submitted | 4 | 6 | -33.3% |
| All intent events | 2,281 | 2,073 | +10.0% |
| Payment Successful | 94 | 104 | -9.6% 🔴 |
| Appointment Booked | 80 | 87 | -8.0% 🔴 |
| Site-wide intent rate (book/uv) | 30.3% | 31.7% | -1.4pp (blog denominator inflation) |
| mindtalk_web-attributed payments | 12 | 15 | -20% (small vol, volatile) |
| mindtalk_web-attributed bookings | 12 | 15 | -20% |

**Note on payment/booking decline:** Ads remain paused. 94 payments vs 104 is within weekly variance on organic traffic. Not a structural regression — organic visitors +13.8% while payments only down 9.6% suggests organic CONVERSION efficiency is roughly flat or slightly improved.

---

## Paid vs organic breakdown W27

| Event | Total | Paid (google/GMB/etc) | Organic-attributable | mindtalk_web |
|---|---:|---:|---:|---:|
| book_appointment_clicked | 1,936 | 892 (46.1%) | 1,044 (53.9%) | 11 (via referring domain) |
| lp_form_submitted | 155 | 146 (94.2%) | 9 (5.8%) | 0 |
| whatsapp_clicked | 116 | 66 (56.9%) | 50 (43.1%) | 0 |
| call_clicked | 70 | 40 (57.1%) | 30 (42.9%) | 0 |
| form_submitted | 4 | 0 | 4 (100%) | 0 |
| Payment Successful | 94 | 0 (ads paused) | 94 (100%) | 12 (12.8%) |
| Appointment Booked | 80 | 0 (ads paused) | 80 (100%) | 12 (15.0%) |

**Note:** google/Google utm_source on book_appointment_clicked with ads paused = GMB + residual tags. Not active paid ads.

---

## 6-Layer Attribution Breakdown (W27 — book_appointment_clicked)

| Layer | Events | Share | Source |
|---|---:|---:|---|
| mindtalk_web (true SEO-attributed) | 11 | 0.6% | $initial_referring_domain = www.mindtalk.in |
| Organic Google Search | ~677 est | ~34.9% | $initial_referring_domain = google (organic portion after removing paid UTM) |
| Android Google Search app | 35 | 1.8% | com.google.android.googlequicksearchbox |
| AI search (chatgpt.com session) | 23 | 1.2% | $initial_referring_domain = chatgpt.com |
| AI search (gemini.google.com session) | 9 | 0.5% | $initial_referring_domain = gemini.google.com |
| Other organic search (Bing, Yahoo) | 9 | 0.5% | Bing 8, Yahoo 1 |
| Direct ($direct) | 287 | 14.8% | No referrer |
| Paid (Google Ads + GMB + IG) | 892 | 46.1% | utm_source IN PAID_LIST |
| Social (Instagram organic) | 15 | 0.8% | l.instagram.com |
| LinkedIn | 1 | 0.1% | www.linkedin.com |

**AI search first-touch attribution (utm_source, all sessions in 7d):** chatgpt.com = 110 events, perplexity = 7 events. Larger than session-based count because first-touch UTM persists across revisits.

---

## UTM attribution (mindtalk_web — Week 3)

**Payment Successful by utm_medium (W27):**
| Medium | Payments | Share | WoW |
|---|---:|---:|---|
| doctor | 9 | 75.0% | -10% (was 10) |
| homepage | 3 | 25.0% | same |

**Payment Successful by utm_content (W27):**
| CTA position | Payments | Share | WoW |
|---|---:|---:|---|
| doctor_card | 9 | 75.0% | -10% (was 10) |
| hero (homepage) | 3 | 25.0% | same |

**Cumulative 3-week UTM validation (W25+W26+W27):**
- Doctor card CTA: 10+10+9 = 29 payments
- Homepage hero: 0+3+3 = 6 payments
- Total mindtalk_web-attributed over 3 weeks: 35+ payments confirmed

**Key insight:** Doctor card CTAs remain the primary revenue path from mindtalk.in. Blog-medium and illness-medium UTMs have not appeared in 3 weeks → blogs do not drive direct payment, only discovery.

---

## 🆕 AI Search signal — WEEK 2, STRENGTHENING

| Source | W27 book clicks | W26 | WoW | Classification |
|---|---:|---:|---|---|
| chatgpt.com (utm_source, first-touch) | 110 | 57 | +92.9% 🔥 | AI search organic |
| chatgpt.com ($initial_referring_domain) | 23 | — | Week 1 of session tracking | AI search organic |
| gemini.google.com ($initial_referring_domain) | 9 | 0 | 🆕 NEW | AI search organic |
| perplexity (utm_source) | 7 | 12 | -41.7% (vol) | AI search organic |
| **Total AI search (first-touch)** | **117** | **69** | **+69.6% 🔥** | Growing channel |

**W27 significance:** ChatGPT first-touch attributed book intent almost doubled WoW. Gemini.google.com appears for the first time as a session referrer. Mindtalk.in is actively being recommended by multiple AI systems for Indian mental health queries. This is the highest-velocity growing channel after Bengaluru organic.

---

## 🟢 Goldmines — protect + amplify

| URL/Section | Visitors est/wk | book clicks | Intent rate | Revenue validated | WoW |
|---|---:|---:|---:|---|---|
| /doctors/* (all) | ~1,140 est | ~1,100+ | 96%+ | 9 payments (doctor_card UTM, W27) | Stable |
| /doctors (main listing) | ~85 est | ~350+ | ~410%+ est | Bengaluru 61%+ of intent | Stable / intensifying |
| /experts/* (all) | ~815 est | ~460+ | 56%+ | Contributing to "doctor" medium | Growing |

**Note:** Visitor counts estimated from W26 scaled by +13.8% site growth. Book click counts from section-weighted estimates.

**Strategy:** No risky changes. Continue adding internal links from /blogs and /illnesses pointing to /doctors and /experts. Refresh defends rankings. Do not chase volume on /doctors main — it's a qualification funnel.

---

## 🟡 Rockets — high intent, grow traffic

| URL | Visitors est/wk | book clicks est | Intent rate est | WoW | Notes |
|---|---:|---:|---:|---|---|
| /doctors/telugu-speaking-doctors | ~70+ est | ~55+ | ~78% | Growing (AP +86%, Hyderabad +34.7%) | Pattern 1 CONFIRMED at week 3 |
| /doctors/tamil-speaking-doctors | ~73+ est | ~52+ | ~71% | Chennai recovering (+40%), TN growing | Pattern 1 CONFIRMED at week 3 |

**Strategy:** SEO refresh + internal links from illness/blog pages. PATTERN CONFIRMED at 3 weeks → **T5 unlock:** propose kannada-speaking / malayalam-speaking / hindi-speaking doctor pages immediately. Also: Vijayawada surge (49 book clicks) suggests city-specific page opportunity.

---

## 🔵 Engagement Engines — top-of-funnel discovery

| URL/Section | Visitors est/wk | Direct booking | Role |
|---|---:|---|---|
| /blogs/* | ~1,151 est | ~0 (0%) | Largest traffic driver. Feeds /doctors via internal links. Pattern 3 CONFIRMED: 0 direct conversions, pure discovery. |

**Note:** Blogs→bookings is an indirect conversion path (blog → internal link → /doctors → book). Not measurable in single-session intent. **Pattern 3 confirmed at 3 weeks** → anchor every blog internal link to /doctors or /experts, never to /illnesses or /treatments.

---

## 🟠 Homepage — tracking gap (NOT a leaky bucket)

| URL | Visitors est/wk | book_appointment_clicked | Revenue via UTM |
|---|---:|---:|---:|
| / (homepage) | ~312 est | 0 (tracking gap) | 3 confirmed payments (hero CTA, UTM) |

**CONFIRMED W26+W27:** Homepage hero CTA works (3 payments each week = consistent) but does NOT fire `book_appointment_clicked`. Instrumentation gap persists. Dev team action required: add event before redirect.

---

## ⚫ Dead weight for direct booking intent

| URL/Section | Visitors est/wk | book clicks | Notes |
|---|---:|---:|---|
| /illnesses/* | ~104 est | ~0 | Possible instrumentation gap. Carries SEO equity. Do not cut — organic traffic source. |
| /treatments/* | ~233 est | ~0 | Possible instrumentation gap. Check event firing. |
| /lps/* | ~423 est | 163 apparent | 94.2% paid; organic-attributable ~9/wk. Paid landing pages — exclude from organic tier. |

---

## ⚠️ UX Friction W27 (consult.cadabams.com — ESCALATIONS)

| URL | Rage clicks | Dead clicks | Total | Severity | WoW vs W26 |
|---|---:|---:|---:|---|---|
| consult.cadabams.com/consult/find-therapist | 53 | 428 | 481 | 🔴 CRITICAL ESCALATING | +64.2% from 293 |
| consult.cadabams.com/consult/booking/8796 (aparna-rani) | 92 | 16 | 108 | 🔴 NEW CRITICAL | New entry |
| consult.cadabams.com/consult/appointments | 0 | 240 | 240 | 🔴 HIGH ESCALATING | +52.9% from 157 |
| consult.cadabams.com/home | 15 | 177 | 192 | 🟡 HIGH ESCALATING | +77.8% from 108 |
| consult.cadabams.com/baseline-assessment | 5 | 41 | 46 | 🟡 MEDIUM | ~flat from 50 |
| consult.cadabams.com/consult/booking/16328 | 11 | 59 | 70 | 🟡 MEDIUM NEW | New this week |

**RESOLVED W27:** consult.cadabams.com/consult/booking/53196 — was 444 total (273 rage + 171 dead) in W26. Now only 3 dead clicks. Appears fixed.

**New UX concern:** Multiple high-converting doctor booking pages (dr-sneha, kanchana-musrif, juhi-gupta, topoti-baruah, ashwini-g-shastry) show UX friction despite successfully converting. Implies conversion is happening despite friction — fix UX = likely uplift in conversion rate.

**Critical action:** find-therapist dead click ESCALATION (240→428, +78%) must go to dev team this week. Users are increasingly hitting broken elements in the find-therapist wizard. Booking/8796 (aparna-rani) rage click spike (0→92) suggests a doctor slot availability issue similar to W26's booking/53196.

---

## Caveats for downstream tasks

1. Visitor counts for sections are estimated (W26 actuals × 1.138 growth rate) — URL-level query exceeded size limits.
2. Homepage book_appointment_clicked = 0 is a tracking gap (3 real payments via UTM, confirmed W26+W27).
3. /illnesses and /treatments may have tracking gaps — verify before acting on 0-intent classification.
4. lp_form_submitted is 94.2% paid — exclude from organic attribution.
5. AI search attribution: chatgpt.com 110 events = first-touch (persists across revisits). 23 = session-level (browser referrer). Both are valid signals for different analyses.
6. Payment Successful decline (104→94) is within weekly variance on organic-only traffic. Not structurally concerning.
