# GEO Conversion Map — Updated 2026-06-17 (INAUGURAL RUN)

**Written by:** T19 Conversion Intelligence (Wed 11:00 IST) — overwritten weekly.
**Source:** Mixpanel 4011856, trailing 7d. Intent = `book_appointment_clicked` (total) ÷ unique visitors per geo.
**Site avg intent rate:** 42% (1,620 book clicks ÷ 3,812 unique visitors). ⚠️ LIMITED_BASELINE: true.

> Intent rate > 100% in some geos = multi-click users ÷ unique visitors (per spec). Read as relative intensity.

## Headline
- **Bengaluru alone = 65% of all booking intent. Karnataka = 67%.** The business is overwhelmingly a Bangalore play right now.
- Tier-1 metros (ex-Bangalore) convert well but contribute small absolute volume — **expansion opportunity**.
- **Hyderabad / Telangana is the standout leak**: high traffic, very low intent.

## By Indian State (top, by intent volume)
| State | Visitors/wk | Book clicks | State intent rate | vs site (42%) |
|---|---:|---:|---:|---|
| Karnataka | 1,427 | 1,078 | 76% | 🟢 +34 |
| Maharashtra | 206 | 116 | 56% | 🟢 +14 |
| Tamil Nadu | 98 | 53 | 54% | 🟢 +12 |
| Delhi (NCT) | 181 | 82 | 45% | 🟢 +3 |
| Andhra Pradesh | 34 | 38 | 112% | 🟢 hot, low vol |
| West Bengal | 46 | 15 | 33% | 🟡 -9 |
| Bihar | 31 | 12 | 39% | ⚪ ~avg |
| Gujarat | 25 | 9 | 36% | ⚪ ~avg |
| Kerala | 86 | 19 | 22% | 🔴 -20 |
| Telangana | 144 | 16 | 11% | 🔴 -31 (big leak) |

## By tier-1 city
| City | Visitors/wk | Book clicks | Intent rate | Read |
|---|---:|---:|---:|---|
| Bengaluru | 1,399 | 1,052 | 75% | 🟢 core engine (65% of all intent) |
| Chennai | 62 | 44 | 71% | 🟢 high intent, low volume → grow |
| Mumbai | 140 | 96 | 69% | 🟢 high intent → grow |
| Delhi | 137 | 75 | 55% | 🟢 solid |
| Pune | 39 | 15 | 38% | ⚪ ~avg |
| Kolkata | 39 | 13 | 33% | 🟡 below avg |
| Hyderabad | 142 | 16 | 11% | 🔴 leak — 3rd-highest city traffic, near-bottom intent |

## NRI / international (baseline only — not actioned)
Small real-intent volume from UK (Portsmouth, Tower Hamlets), US (California, Michigan, Illinois), UAE (Dubai, Abu Dhabi), Bangladesh (Dhaka 17 book clicks). Capture only.

## ⚠️ Bot / proxy noise — EXCLUDE from geo signal
High pageviews, ~0 intent → datacenter/proxy traffic, not real users:
- **Singapore: 213 visitors, 0 book clicks** (largest noise source)
- China: Nanjing 23, Beijing 11, Handan 9, Changzhou 6 — all ~0 intent

These inflate global "visitors"; the real engaged audience is India-concentrated.

## Actions seeded for Strategist
1. **Investigate Hyderabad/Telangana leak.** 142 city visitors, 11% intent vs Bangalore 75%. Paradox: Telugu-speaking-doctor pages are top Rockets (95% intent) yet Telangana geo converts worst — the Telugu intent likely comes from AP/Tirupati, not Hyderabad. Cross-check page×geo next run.
2. **Grow Mumbai + Chennai + Delhi.** High intent rate, low volume = under-served by SEO. Local landing pages likely high ROI.
3. **Don't chase Singapore/China traffic** — it's noise.
