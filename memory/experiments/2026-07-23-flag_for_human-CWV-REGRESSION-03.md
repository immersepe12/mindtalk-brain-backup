# flag_for_human on CWV-REGRESSION-03 — 2026-07-23

## What we did
Posted Slack flag to #seo-workflow-mindtalk (ts: 1784795676.969119) with full LCP regression context for the dev team.

## Context
T14 Tech Health W4 (2026-07-22) confirmed: 5 hub pages still failing LCP threshold after 3 consecutive weeks.
- Homepage RECOVERED (10.55s→1.80s) — but the fix was NOT applied to the other hub pages.
- /assessments WORSENED (4.01s→7.34s) — regression between 07-15 and 07-22.
- Pattern: FCP fast (0.96–1.2s) on ALL pages; LCP slow only on hub pages = page-specific large lazy-loaded element.

## Pages flagged
| Page | LCP | 
|---|---|
| /treatments/counselling-therapy | 9.55s 🔴 |
| /app | 9.14s 🔴 |
| /journeys | 9.13s 🔴 |
| /worksheets | 9.15s 🔴 |
| /assessments | 7.34s 🔴 (WORSE from 4.01s) |

## Dev action items sent
1. Add `<link rel="preload">` for hero element on each hub page (same fix as homepage)
2. Check for `loading="lazy"` on above-fold components that should be eager
3. Identify what changed on /assessments between 07-15 and 07-22

## Expected outcome
Dev team identifies and fixes per-page LCP elements. Counselling-therapy ranking stabilises post-fix (prior correlation confirmed in June rank drop).

## Watch
No watch scheduled — T14 auto-checks again 2026-07-29.

## Notes
Verifier: APPROVE (blast radius = 0, path-safe, high goal-alignment).
Slack ts: 1784795676.969119 / link: https://cadabamsgroup.slack.com/archives/C0AUAPS4J83/p1784795676969119
