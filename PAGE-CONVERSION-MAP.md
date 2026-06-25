# Page Conversion Map — Updated 2026-06-25 (W26)

**Written by:** T19 Conversion Intelligence (Wed 11:00 IST) — overwritten each week.
**Read by:** T10 Strategist, T18 Professional Input, T12 Learner.
**Source:** Mixpanel project 4011856 (unified: mindtalk.in + consult.cadabams.com + app), trailing 7d Jun 18-24.
**Intent signal:** `book_appointment_clicked` (total events) ÷ unique page visitors. Multi-click users inflate rate above 100%; read as relative intensity.

> **W26 baseline established.** Volume gates upgraded from W25's scaled thresholds. Total unique visitors 5,620 (+47.4% WoW). Median section intent rate 56.8%.
>
> **PAID/ORGANIC SEPARATION ACTIVE (Step 5.3).** lp_form_submitted = 96.4% paid. book_appointment_clicked organic = 57.6% = 1,026 events. Revenue events (Payment Successful 104 / Appointment Booked 87) are 100% organic — ads paused.
>
> **UTM SYSTEM LIVE:** First full 7-day window of mindtalk_web attribution. 15 payments and 15 appointments confirmed attributable to mindtalk.in CTAs.

---

## Site-level W26 snapshot (Jun 18-24)

| Metric | W26 | W25 | WoW |
|---|---:|---:|---|
| Unique visitors (site) | 5,620 | 3,812 | +47.4% ✅ |
| book_appointment_clicked (total) | 1,781 | 1,620 | +9.9% |
| lp_form_submitted | 137 | 131 | +4.6% |
| whatsapp_clicked | 100 | 80 | +25% |
| call_clicked | 49 | 57 | -14% |
| form_submitted | 6 | 8 | -25% |
| All intent events | 2,073 | 1,896 | +9.3% |
| Payment Successful | 104 | — | W26 baseline |
| Appointment Booked | 87 | — | W26 baseline |
| Site-wide intent rate (book/uv) | 31.7% | 42% | -10.3pp (blog traffic growth = denominator inflation) |
| mindtalk_web-attributed payments | 15 | 0 | First week of UTM data |

---

## Paid vs organic breakdown W26

| Event | Total | Paid (google/GMB/etc) | Organic-attributable | mindtalk_web |
|---|---:|---:|---:|---:|
| book_appointment_clicked | 1,781 | 755 (42.4%) | 1,026 (57.6%) | 0 (fires on mindtalk.in; UTM tracked at consult) |
| lp_form_submitted | 137 | 132 (96.4%) | 5 (3.6%) | 0 |
| whatsapp_clicked | 100 | 48 (48%) | 52 (52%) | 0 |
| call_clicked | 49 | 29 (59.2%) | 20 (40.8%) | 0 |
| Payment Successful | 104 | 0 (ads paused) | 104 (100%) | 15 (14.4%) |
| Appointment Booked | 87 | 0 (ads paused) | 87 (100%) | 15 (17.2%) |

**Note:** google/Google utm_source on book_appointment_clicked with ads paused = GMB (Google My Business) + residual campaign tags. Not active paid ads.

---

## UTM attribution (mindtalk_web — first full week)

**Payment Successful by utm_medium:**
| Medium | Payments | Share |
|---|---:|---:|
| doctor | 10 | 66.7% |
| homepage | 3 | 20.0% |
| site (global) | 2 | 13.3% |

**Payment Successful by utm_content:**
| CTA position | Payments | Share |
|---|---:|---:|
| doctor_card | 10 | 66.7% |
| hero (homepage) | 3 | 20.0% |
| bottom | 2 | 13.3% |

**Top doctor pages by payment attribution:** dr-rayani-m-dessa (2), homepage (3), global (2), kanchana-musrif (1), dr-sneha (1), priyanka-kema (1), aparna-rani (1), juhi-gupta (1), dr-arun-kumar (1), preeti (1), nishmitatj (1).

**Key insight:** Doctor card CTAs → individual booking pages is the #1 converting path (66.7%). Homepage hero is secondary (20%). The `find-therapist` wizard path converts poorly vs direct doctor_card links (supported by UX friction data below).

---

## 🆕 AI Search signal (NEW — Week 1 detection)

| Source | book_appointment_clicked | % of total | Classification |
|---|---:|---:|---|
| chatgpt.com | 57 | 3.2% | AI search organic |
| perplexity | 12 | 0.7% | AI search organic |
| **Total AI search** | **69** | **3.9%** | Growing channel |

**Significance:** chatgpt.com is the #4 source of booking intent — larger than any single Indian city outside Bengaluru/Hyderabad. Mindtalk.in is appearing in ChatGPT responses to mental health queries. Monitor weekly. Feed to AI-SEO / ai-visibility work.

---

## 🟢 Goldmines — protect + amplify

| URL/Section | Unique visitors/wk | book clicks (total) | Intent rate | Revenue validated | WoW |
|---|---:|---:|---:|---|---|
| /doctors/* (all) | 1,003 | 1,132 | 113% | 10 payments (doctor_card UTM) | ↑ large |
| /doctors (main listing) | 93 | 363 | 390% (up from 321%) | 2 payments (dr-rayani) | Visitors -21.8%, intent ↑ |
| /experts/* (all) | 716 | 407 | 56.8% | Contributing to "doctor" medium payments | Visitors ↑ |

**Strategy:** No risky changes. Add internal links from /blogs and /illnesses pointing to /doctors and /experts. Refresh defends. /doctors main listing: fewer but more qualified visitors — do not chase volume, protect quality.

---

## 🟡 Rockets — high intent, grow traffic

| URL | Visitors/wk | book clicks | Intent rate | WoW | Notes |
|---|---:|---:|---:|---|---|
| /doctors/telugu-speaking-doctors | 59 | 43 | 72.9% | +59.5% visitors ✅ | Language pattern week 2 |
| /doctors/tamil-speaking-doctors | 64 | 45 | 70.3% | +82.9% visitors ✅ | Language pattern week 2 |

**Strategy:** SEO refresh + internal links from illness/blog pages. Confirm by week 3 → propose kannada/malayalam/hindi-speaking-doctor pages.

---

## 🔵 Engagement Engines — top-of-funnel discovery

| URL/Section | Visitors/wk | Direct booking | Role |
|---|---:|---|---|
| /blogs/* | 1,011 | ~0 (0%) | Largest traffic driver. Feeds /doctors via internal links. Discovery-only, 0 direct conversions. |

**Note:** Blogs→bookings is an indirect conversion (user visits blog → follows internal link → books on /doctors). Not measurable in single-session intent events. Lag cohort analysis needed (Week 5+).

---

## 🟠 Homepage — tracking gap (NOT a leaky bucket)

| URL | Visitors/wk | book_appointment_clicked | Revenue via UTM |
|---|---:|---:|---:|
| / (homepage) | 274 | 0 | 3 confirmed payments (hero CTA, UTM validated) |

**CONFIRMED W26:** Homepage hero CTA works (3 payments) but does NOT fire `book_appointment_clicked`. Instrumentation gap. Action: dev team to add event firing before redirect. Do NOT treat as leaky bucket.

---

## ⚫ Dead weight for direct booking intent

| URL/Section | Visitors/wk | book clicks | Notes |
|---|---:|---:|---|
| /illnesses/* | 91 | ~0 | May be instrumentation gap. Carries SEO equity. |
| /treatments/* | 204 | ~0 | May be instrumentation gap. Check event firing. |
| /lps/* | 371 | 163 apparent | 96.4% paid; organic-attributable ~5/wk. Paid landing pages, not SEO pages. |

---

## ⚠️ UX Friction (consult.cadabams.com app — affects conversion funnel)

| URL | Rage clicks | Dead clicks | Total | Severity |
|---|---:|---:|---:|---|
| consult.cadabams.com/consult/booking/53196 | 273 | 171 | 444 | 🔴 CRITICAL — dev investigate |
| consult.cadabams.com/consult/find-therapist | 53 | 240 | 293 | 🔴 HIGH |
| consult.cadabams.com/consult/appointments | 0 | 157 | 157 | 🟡 MEDIUM |
| consult.cadabams.com/home | 0 | 108 | 108 | 🟡 MEDIUM |
| consult.cadabams.com/baseline-assessment | 0 | 50 | 50 | 🟡 LOW-MEDIUM |

**Critical finding:** booking/53196 = single doctor's booking page, 444 friction events. Likely broken/unavailable doctor slot. Immediate dev review needed.

**Conversion implication:** find-therapist wizard path (293 friction events) vs doctor_card direct links (10 payments, low friction). Data argues strongly for prioritizing direct doctor_card CTAs over find-therapist funnels.

---

## Caveats for downstream tasks

1. Homepage book_appointment_clicked = 0 is a tracking gap (3 real payments via UTM).
2. /illnesses and /treatments may also have tracking gaps — verify before acting on 0-intent classification.
3. lp_form_submitted is 96.4% paid — exclude from organic attribution.
4. AI search (chatgpt.com) = organic intent, not separated above but is included in organic-attributable.
5. Median intent rate: 42% (W25) → 31.7% (W26) due to blog traffic denominator inflation. Section-level rates are more stable comparisons.
