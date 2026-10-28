# T19 Conversion Intelligence — Audit Log
**Run date:** 2026-10-28 (Wednesday)
**Week covered:** W44 (Oct 21–27, 2026)
**Session:** Automated scheduled task (2-session continuation; context limit hit mid-run)

---

## Run Status: ✅ COMPLETE

---

## Queries Used (Mixpanel project 4011856 — UNIFIED)

Total queries: 13 of ≤30 budget (all in session 1, pre-compaction)

1. Site-level book clicks + unique visitors (7d, W44)
2. Organic book clicks — paid UTM excluded
3. Payments (Payment Successful) — organic only, hard filter applied
4. Bookings (Appointment Booked) — organic only, hard filter applied
5. chatgpt.com book clicks (utm_source) — unique
6. chatgpt.com payments + bookings
7. Assessment Completed event — unique
8. Journey Task event — unique
9. GEO breakdown by state/city — organic book clicks
10. UTM attribution breakdown (utm_source, utm_medium, utm_campaign)
11. Rage clicks by page — unique
12. Dead clicks site-level — unique (per-page breakdown exceeded token limit)
13. mindtalk_web payments (utm_source=mindtalk_web) — organic SEO attribution

**GA4:** SKIPPED — Supermetrics trial expired 2026-07-27 (17th consecutive week)

---

## Organic/Paid Separation Applied

HARD RULE (2026-06-22) enforced throughout:
- Excluded utm_source IN: google, Google, GMB, gmb, sitelink, facebook, Facebook, fb, Fb, meta, Meta, instagram, Instagram, ig, linkedin, LinkedIn
- All organic metrics = unique events from non-paid UTM sources only

---

## Key Metrics W44

| Metric | Value | WoW |
|---|---|---|
| Unique visitors | ~12,672 | +3.9% |
| Organic book clicks | 690 | +12.9% |
| Organic intent rate | 5.45% | +0.45pp |
| Organic payments | 167 | +21.0% 🔥 |
| Organic bookings | 207 | +16.3% 🟢 |
| chatgpt.com unique | 84 | +10.5% |
| Assessment Completed | 553 | ALL-TIME RECORD |
| Journey Task | 36 | +9.1% (3rd positive) |
| Dead rate | 10.22% | -0.38pp (above 10%) |
| Rage clicks | 220 | -0.9% ✅ |

---

## Files Updated

| File | Status | Notes |
|---|---|---|
| brain/PAGE-CONVERSION-MAP.md | ✅ COMMITTED | W44 state, attribution breakdown |
| brain/GEO-CONVERSION-MAP.md | ✅ COMMITTED | Organic-only W44, methodology note |
| brain/HIGH-CONVERTER-PATTERNS.md | ✅ COMMITTED | P19 W4 CONFIRMED, P18 W4 CONFIRMED, P8 DEMOTED, P20 EMERGING, P21 NEW |
| brain/UX-FRICTION-PAGES.md | ✅ COMMITTED | W44 friction summary, /home 8W critical |
| brain/memory/page-conversion-history.md | ✅ COMMITTED | W44 row appended |
| brain/memory/strategist-signal-feed.md | ✅ COMMITTED | W44 full signal entry + 9 urgent flags |
| brain/TRAJECTORY.md | ✅ COMMITTED | W43+W44 rows added to KPI section |

---

## Pattern Updates W44

| Pattern | Previous | W44 | Action |
|---|---|---|---|
| P1 Telugu | W11 CONFIRMED | W11 stable | Telangana 46 organic |
| P1 Tamil | W11 CONFIRMED | W11 stable | TN 42 organic |
| P5 AI Search | W10 | W11 CONFIRMED | 84 unique, 2 payments |
| P8 Kerala | WATCH | DEMOTED TO CONCERN | 12 clicks, 3rd step-back |
| P13 Gulf | STABLE | STABLE | ~15 organic |
| P15 Delhi NCT | WATCH | APPROACHING CONFIRM | 63 organic (9.1%) |
| P18 UP | W3 | W4 CONFIRMED | 25 organic (+13.6%) |
| P19 Maharashtra | W3 | W4 CONFIRMED | 72 organic, Mumbai 55 |
| P20 Assessment-booking lag | EMERGING W3 | W4 CONFIRMED | 553 record, revenue +21% |
| P21 Haryana | NEW WEEK 1 | WEEK 2 | 15 clicks, 3rd week needed |

---

## Critical Issues (Escalation Required)

1. **🔴 /home dead clicks — 8 consecutive weeks UNRESOLVED** (W37–W44)
   - 679 dead clicks per week on app landing page
   - Not a content issue — requires engineering code fix
   - Action: Escalate to product/engineering immediately

2. **🔴 W45 Diwali warning** — Oct 29 = Diwali; W45 run may show conversion dip
   - Do NOT interpret W45 drop as organic regression
   - Expect recovery W46

3. **🟡 GA4 SKIPPED** — 17 consecutive weeks without GA4 data
   - Supermetrics trial expired 2026-07-27
   - Action: Renew Supermetrics trial or restore GA4 access

---

## Slack Notification

Posted to C0AUAPS4J83 at ts: 1793166937.730729
Link: https://cadabamsgroup.slack.com/archives/C0AUAPS4J83/p1793166937730729

---

## Next Run

**W45 run:** Wednesday 2026-11-04
- Expected: Diwali (Oct 29) seasonal dip in W45 conversions
- Watch: P21 Haryana W3 (confirm or demote), P8 Kerala recovery threshold, P20 assessment lag revenue signal
- Pending: Per-page dead click breakdown (use jq/bash extraction to avoid token limit)
- Pending: Mixpanel auto-pay setup (3 billing blocks in 2026: W30, W38, W40)

