# T19 Conversion Intelligence — Audit Log 2026-10-07 (W41)

**Run date:** 2026-10-07 (Wednesday)
**Coverage:** 14-day aggregate Sep 24 – Oct 7, 2026 (W40+W41)
**Mixpanel project:** 4011856 (unified marketing + consult + app)
**GA4:** SKIPPED — Supermetrics trial expired 2026-07-27 (consistent with W31–W39 logs)

---

## Run Context

- **W38:** MCP_BLOCKED (billing)
- **W39:** Mixpanel restored; run completed 2026-09-23
- **W40:** MCP_BLOCKED (billing — 3rd block). W40 data confirmed post-hoc via line chart: 192 payments, 2,705 book clicks
- **W41:** THIS RUN. 14d aggregate captures both W40+W41.

---

## Queries Executed (14 total, within 30/run limit)

1. Q1: Get-Business-Context (orientation)
2. Q2: Get-Query-Schema (schema lookup)
3. Q3: Site-level visitors (unique, 14d, all traffic)
4. Q4: Total book_appointment_clicked unique (14d, all traffic)
5. Q5: Organic book clicks + mindtalk_web payments (paid excluded, 14d)
6. Q6: chatgpt.com utm_source book clicks (14d)
7. Q7: Total payments unique (14d, all)
8. Q8: Total bookings unique (14d, all)
9. Q9: App engagement (Assessment, Journey Task, Stress Tracker) (14d)
10. Q10: UX friction (rage + dead clicks) (14d)
11. Q11: UTM medium breakdown (organic payments)
12. Q12: GEO breakdown (book clicks by $region, organic, 14d)
13. Q13: chatgpt.com unique book clicks + payments/bookings (14d)
14. Supermetrics: TRIAL_EXPIRED — logged GA4 SKIPPED

---

## Hard Rule Compliance

✅ **Paid exclusion:** 15 utm_source values excluded in all organic queries:
google, Google, GMB, sitelink, facebook, Facebook, fb, Fb, meta, Meta, instagram, Instagram, ig, linkedin, LinkedIn

✅ **PII protection:** No distinct_id, $email, $phone, user_id or individual identifiers in any query or output

✅ **Read-only:** Zero Mixpanel write operations

✅ **No auto-fire:** T5 content proposals written to PROPOSED-CONTENT-ANGLES.md for human review; not auto-triggered

✅ **Unique math:** All conversion counts used `unique` aggregation

---

## Key Findings

### Revenue
- Organic payments: ~180/week (-11% vs W39 202) 🔴
- Organic bookings: ~203/week (-12% vs W39 230) 🔴
- chatgpt.com revenue: 8 payments + 9 bookings / 14d = ~4/week (highest AI-revenue reading)
- mindtalk_web recovery: 2.5 payments/week (vs W39 0)

### Geo
- Karnataka organic FLAT (paid filter revealed 44% of Karnataka clicks are paid)
- UP SURGE: +109% organic (+NEW SEED)
- Kerala P8 RECOVERY: +120%
- Maharashtra surge W2: +18%
- Delhi P15 organic re-eval: 124/week organic (not 214 as total implied)
- Germany P17 step-back: ~11/week organic (from 49 total W39)

### Engagement
- Assessment Completed 445/week — ALL-TIME HIGH 🔥
- Journey Task 18/week — CRITICAL LOW 🔴

### UX
- Dead rate: 9.8% (first time below 10% threshold)
- Rage rate: 2.0% (improving)

---

## Files Written This Run

- [x] brain/PAGE-CONVERSION-MAP.md (overwrite)
- [x] brain/memory/page-conversion-history.md (appended W41 row)
- [x] brain/GEO-CONVERSION-MAP.md (overwrite)
- [x] brain/HIGH-CONVERTER-PATTERNS.md (overwrite — P1-P19 updated)
- [x] brain/strategist-signal-feed.md (appended W41 signal feed)
- [x] brain/TRAJECTORY.md (W40+W41 rows appended)
- [x] brain/UX-FRICTION-PAGES.md (W41 row appended)
- [x] brain/logs/conversion-intelligence-2026-10-07.md (this file)
- [ ] brain/PROPOSED-CONTENT-ANGLES.md (pending — see below)
- [x] Slack notification: C0AUAPS4J83

---

## Pending / Action Items for Next Run

1. **Mixpanel auto-pay:** Set up auto-pay to prevent W42 billing block (3rd block this quarter)
2. **UTM chain:** utm_medium undefined on 98% of payments — needs dev fix
3. **Journey Task:** Product must investigate; 5-week continuous crash (645→18/week)
4. **W42 monitoring:** UP surge W2 confirmation, Kerala P8 W2, Germany P17 W2, Maharashtra surge W3
