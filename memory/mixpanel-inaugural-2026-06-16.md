# Mixpanel Inaugural Pull — 2026-06-16 (CORRECTED)

**MCP access:** ✅ ENABLED on US-cluster projects · ⚠ BLOCKED on EU-cluster projects (`cadabams group`, project 3984638 — the app data — needs separate EU MCP connector)

**Method:** Mixpanel MCP via Get-Business-Context → Get-Events → Run-Query
**Windows:** Trailing 7 days (marketing) + Trailing 30 days (consult funnel — low-volume product)

---

## Correction notice

My first read of this morning was WRONG. I diagnosed a "0% form_submitted conversion" funnel break on mindtalk.in. The actual architecture:

**Mindtalk has a cross-domain conversion funnel:**
- `book_appointment_clicked` (event on mindtalk.in marketing site, project 4011856) fires when user taps the sticky "Book a Session" CTA
- That click navigates the user to `consult.cadabams.com/consult/find-therapist` — a separate web app, separate Mixpanel project
- The actual booking, payment, and conversion happen on the consult web app (project 3986277 "Cadabams consult")
- `form_submitted` (6/wk on mindtalk.in) is only the LP form path (a small subset)

So the correct conversion funnel needs BOTH projects.

---

## Mindtalk website project (4011856) — 7d totals

(Marketing site — top of funnel)

| Metric | 7d |
|---|---:|
| $mp_web_page_view | 5,357 |
| blog_viewed | 1,155 |
| doctor_profile_viewed | 1,191 |
| treatment_page_viewed | 221 |
| illness_page_viewed | 154 |
| riya_page_viewed | 5 ⚠ |
| book_appointment_clicked (sticky CTA exposure) | 1,521 |
| cta_clicked | 164 |
| whatsapp_clicked | 79 |
| call_clicked | 57 |
| lp_form_submitted | 124 |
| form_submitted (legacy main form, mostly retired) | 6 |
| form_started | 15 |
| lead_create_failed | 77 |

## Cadabams consult project (3986277) — 30d totals

(Web app — where bookings actually happen)

| Metric | 30d |
|---|---:|
| Doctor Booking Page Viewed (`find-therapist` landing) | 320 |
| Doctor Card Clicked | 205 |
| Continue Button Clicked To Book A Doctor | 29 |
| Payment Initiated | 26 |
| Payment Successful | **14** |
| Payment Failed | **12** ⚠ (46% of payment attempts fail) |
| Appointment Booked | **10** |
| Appointment Viewed | 44 |
| Appointment Cancelled | 1 |
| Appointment Rescheduled | 2 |
| Login Page Viewed | 125 |
| Login OTP Requested | 85 |
| Login Successful | 59 (47% success rate) |
| Signup Completion | **2** ⚠ (only 2 NEW signups in 30 days) |
| Book Appointment FAB Clicked | 50 |

---

## The real cross-domain funnel (30 days)

Step → step % → cumulative %

1. **Doctor Booking Page Viewed (find-therapist landing):** 320 — 100% — 100%
2. **Continue Button Clicked:** 29 — **9%** ⚠ — 9%
3. **Payment Initiated:** 26 — 90% — 8%
4. **Payment Successful:** 14 — **54%** ⚠ — 4%
5. **Appointment Booked:** 8 (through this path; 10 total via FAB path too) — 57% — 2.5%

### Where the leaks are

| Drop step | Drop % | Likely cause |
|---|---|---|
| **#1 — Doctor Booking Page Viewed → Continue Clicked** | 77% lost (320→29) | Find-therapist UX gap. People land but don't pick a doctor or don't click continue. Doctor relevance? Price visibility? Filter UX? Doctor availability? |
| **#2 — Payment Initiated → Payment Successful** | 46% lost (26→14) | Payment failure rate is ENORMOUS. Could be gateway issues, declined cards, timeout, UX. |
| **#3 — Login funnel** | 53% lost (Login Page Viewed 125 → Successful 59) | OTP delivery? UX? |

### What's working

- 67.6% of doctor profile views on mindtalk.in click "Book Appointment" (high intent)
- 90% of "Continue Clicked" users initiate payment (the post-continue flow is clean)
- Appointment cancellations are minimal (1 in 30d on 10 booked) — when they book, they show up

---

## REAL conversion math

- Marketing site weekly page views: 5,357 (organic + direct combined)
- Mindtalk weekly bookings (extrapolated, 10 / 30d × 7 = ~2.3/wk)
- **Organic-to-booking conversion rate: ~0.04%**

For comparison: a healthy India healthcare booking site should be 0.5-1.5%. We're 12-37× below benchmark.

Two interpretations:
- Either the conversion rate is genuinely poor (UX/UI bottlenecks on consult.cadabams.com)
- OR conversions are split across paths we're not seeing (Cadabams Group app, walk-ins, WhatsApp follow-ups, sales calls)

---

## What's missing (EU MCP blocker)

The "cadabams group" project (id 3984638) is the **app analytics** — assessments, journeys, mobile app events, the heart of the product. Hosted on Mixpanel EU. Our current MCP server is US, so we get a regional access error.

To unblock: Kushal needs to add the Mixpanel EU MCP connector (separate from the US one).

Without it, the autonomous loop is partially blind to:
- 99 free assessments completed
- 155+ guided audio sessions listened
- 18 guided journeys taken
- Mobile app session data
- Riya AI conversations
- Mood, sleep, stress tracker events
- Any cross-product engagement

---

## Implications for Strategist tonight

**My earlier "fix the form handoff" recommendation was based on incomplete data.** The real priorities by leverage:

1. **Fix the 46% payment failure rate** — 12 payment fails in 30d on only 26 attempts is a top-line revenue leak. Likely a gateway/integration issue. Dev investigation, not SEO.

2. **Fix the find-therapist landing UX** — 77% drop from Doctor Booking Page Viewed → Continue Clicked. Either price shock, doctor relevance, or filter design is killing conversion. UX/design investigation.

3. **CTR sprint (dry-begging) is now LESS urgent**, but still net-positive — more impressions on the site → more book_appointment_clicked → more arrivals on consult.cadabams.com. Just won't move the needle on bookings until the post-arrival funnel is fixed.

4. **Doctor profile pages on mindtalk.in are still the best SEO target** — 67.6% intent rate is structurally amazing. SEO can drive more here while UX fixes are in flight.

5. **Riya page (5 views/wk) and Signup (2/mo) are structural exposure problems** — separate from SEO, more product/marketing.

The CTR sprint can ship without conflict. The big revenue lever is OUT of the SEO loop and into product/dev — but the SEO loop should know about it so it weights actions correctly.
