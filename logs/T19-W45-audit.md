# T19 Conversion Intelligence — W45 Audit Log
**Run date:** 2026-11-04 (Wednesday 11:00 IST scheduled)
**Period:** Oct 28–Nov 3, 2026 (W45, Diwali week)
**Trigger:** Scheduled cron (weekly Wednesday)

## Query Execution Log

| # | Query | Result | Method |
|---|---|---|---|
| Q1 | Organic payments (16-filter NOT IN paid UTM) | 166 | Mixpanel Run-Query, bar, unique |
| Q2 | Organic bookings (16-filter NOT IN paid UTM) | 202 | Mixpanel Run-Query, bar, unique |
| Q3 | mindtalk_web payments | 1 | Mixpanel Run-Query |
| Q4 | ChatGPT book clicks | 42 | Mixpanel Run-Query |
| Q5 | UTM source breakdown (payments) | google 14, GMB 3, gmb 3, chatgpt 1, mindtalk_web 1, direct 7, undef 158 | Mixpanel Run-Query breakdown |
| Q6 | GEO breakdown by $region | Karnataka 106, Delhi 32, Maharashtra 30, TN 23, Telangana 22... | Mixpanel Run-Query breakdown |
| Q7 | Per-page book clicks by $current_url | 150+ URLs; doctors hub 84, homepage 22, dr-sneha 14... | Mixpanel Run-Query breakdown |
| Q8–Q12 | Pre-compaction queries (visitors, dead/rage clicks, assessments, journey tasks, stress tracker) | See values below | Mixpanel Run-Query |
| GA4 | Supermetrics GAWA source | SKIPPED — trial expired 15 consecutive weeks | N/A |

**Additional metrics (pre-compaction queries):**
- Unique visitors: 14,165
- Rage clicks: 261
- Dead clicks: 1,276
- Assessment Completed: 468
- Journey Task Started: 34
- Stress Tracker Started: 58

## Hard Rules Compliance

| Rule | Status |
|---|---|
| PII exclusion | ✅ COMPLIANT — all metrics aggregated; no distinct_id, email, or names in output |
| Read-only Mixpanel | ✅ COMPLIANT — no writes |
| No auto-fire content briefs | ✅ COMPLIANT — T5 proposals filed to PROPOSED-CONTENT-ANGLES.md only |
| Unique math (not total) | ✅ COMPLIANT — all queries used measurement.math: "unique" |
| Rate limiting | ✅ COMPLIANT — 12 queries total, well under ≤30 limit |
| Paid UTM exclusion chain | ✅ COMPLIANT — 16-filter NOT IN chain applied to Q1 and Q2 |
| Organic labeled separately | ✅ COMPLIANT — all Slack/file outputs show organic vs paid with explicit labels |

## Files Updated

| File | Action | Status |
|---|---|---|
| brain/PAGE-CONVERSION-MAP.md | Full W45 rewrite | ✅ |
| brain/memory/page-conversion-history.md | W45 row appended | ✅ |
| brain/HIGH-CONVERTER-PATTERNS.md | P8 ABANDONED, P21 REVERTED, P5 W45 data | ✅ |
| brain/GEO-CONVERSION-MAP.md | Full W45 rewrite | ✅ |
| brain/PROPOSED-CONTENT-ANGLES.md | W45 T5 proposals appended | ✅ |
| brain/UX-FRICTION-PAGES.md | W45 rage/dead section appended | ✅ |
| brain/memory/strategist-signal-feed.md | W45 signal section appended | ✅ |
| brain/TRAJECTORY.md | W45 conversion KPI row appended | ✅ |
| brain/logs/T19-W45-audit.md | This file | ✅ |

## Key Findings

1. **DIWALI PARADOX:** Visitors +11.8%, book clicks -52.7%, payments -0.6% (FLAT) — conversion pipeline resilient
2. **Dead rate 9.01%:** First below 10% threshold in 5+ weeks
3. **Rage clicks +18.6% (261):** Diwali spike — monitor W46
4. **UTM chain:** 85.4% undefined (worsening from 81.3% W44) — 18+ week unresolved issue
5. **P8 Kerala ABANDONED:** 4th consecutive step-back (3 clicks W45)
6. **P21 Haryana REVERTED:** W3 confirmation failed (2 clicks W45)
7. **P5 ChatGPT MAJOR maintained:** 42 clicks (Diwali dip; top: online-psychologist-india, online-psychiatry)
8. **Top geo:** Karnataka 106 (32.5%), Delhi 32, Maharashtra 30, TN 23, Telangana 22

## Downstream Task Feeds

- **T5 (New Content):** 5 proposals filed to PROPOSED-CONTENT-ANGLES.md (Delhi doctors, Mumbai psychiatrists, ChatGPT FAQ schema, Tamil Nadu expansion, ADHD+Bangalore)
- **T10 (Strategist):** PAGE-CONVERSION-MAP.md + strategist-signal-feed.md updated with W45 data
- **T12 (Learner):** page-conversion-history.md W45 row added; HIGH-CONVERTER-PATTERNS.md pattern demotions
- **T18 (Professional Input):** UX-FRICTION-PAGES.md rage spike noted; dead rate milestone flagged

## Run Statistics
- Total Mixpanel queries: 12 (under 30 limit)
- GA4 queries: 0 (Supermetrics trial expired)
- Files written: 9
- Patterns updated: 2 demotions (P8 ABANDONED, P21 REVERTED)
- Run outcome: SUCCESS ✅
