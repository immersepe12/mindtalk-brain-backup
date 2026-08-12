# flag_for_human on CWV-DOCTORS-PAGE-01 — 2026-08-12

## What we did
Detected new critical CWV failure on /doctors/psychiatrists-in-bangalore via T14 Tech Health run (2026-08-12). Flagged to dev team via Slack (#seo-workflow-mindtalk, ts: 1786533017.817679). Verifier sub-agent verdict: APPROVE (zero-risk operational notification).

**Slack message included:**
- LCP 8.95s, perf score 56 on /doctors/psychiatrists-in-bangalore
- Root cause: page.tsx fetches all 76 physician profiles dynamically before hydration → white screen → late LCP
- Precedent: same pattern as counselling-therapy (9.26s → recovered), /app (9.14s → recovered), /assessments (7.34s → recovered)
- All 12 /doctors/* specialty listing pages likely affected
- 3 fix options: (a) paginate 10 above fold + lazy-load 66; (b) preload hero element; (c) SSR above-fold profiles
- Deadline: 2026-08-26 Core Update (14 days)

## Expected outcome
Dev team investigates and fixes /doctors/psychiatrists-in-bangalore (and other /doctors/* pages) before Aug Core Update. Perf 56 → perf ≥75 = full CWV signal restore on Tier A ×1.5 commercial cluster ("psychiatrists in bangalore" 110K/mo, Perplexity FIRST citation).

## Watch
None opened (dev action required — T14 will detect the fix on next weekly run).

## Notes
- Homepage LCP RECOVERED this week (CWV-REGRESSION-04 fix: 11.0s → 2.78s)
- Doctors page is now the new critical CWV failure site-wide
- First time T14 sampled this page (7 prior runs, homepage-focused)
- Verifier: APPROVE — all §1–§10 checks pass or N/A for flag_for_human type
