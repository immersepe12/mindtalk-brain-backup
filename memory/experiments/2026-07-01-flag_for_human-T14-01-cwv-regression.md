# flag_for_human on T14-01 CWV regression — 2026-07-01

## What we did

Posted a CRITICAL CWV regression alert to Slack (#seo-workflow-mindtalk) based on the 2026-07-01 technical health report from Task 14. Two new failures appeared between the 06-24 baseline and 07-01:

1. `/treatments/counselling-therapy` — LCP 1.65s → 9.26s (+460%). Perf 97 → 66. Also: "counselling" organic rank dropped from #9 to absent from top-20. Timing correlation between LCP regression and ranking drop is strong.

2. `/assessments` — TBT 179ms → 2923ms (+16×). Perf 96 → 68. Top free-tool page driving gad-7 #10 ranking — further JS bloat could drop that rank.

No autonomous fixes were attempted. The Slack flag asks dev to investigate git commits between 06-24 and 07-01 for: treatment page template changes, hero images, new embedded components, new analytics scripts, third-party embeds, or assessment-loader bundle additions.

## Expected outcome

Dev identifies and reverts the regression-causing commit(s) within the week. If LCP on counselling-therapy recovers to ~1.65s, the "counselling" ranking should recover from absent → back toward #9 (assuming the drop was performance-caused, not algorithmic). /assessments TBT fix protects the gad-7 #10 ranking.

## Watch

No new WATCH row opened — this is a dev/infra fix, not an SEO content action. Tech Health task (T14) will re-check on 07-08 (next weekly run).

If "counselling" rank hasn't recovered by 07-08, Strategist should add it to the confirmed-drops.json and schedule a content investigation.

## Notes

- Verifier APPROVE (all 10 checks pass — notification only, no blast radius)
- Slack message: https://cadabamsgroup.slack.com/archives/C0AUAPS4J83/p1782904888794339
- BACKLOG T14-01 row remains in BACKLOG (not closed) — stays open until dev confirms fix
- ALGO_WATCH still active (clears 07-02); treatment LCP fix is independent of ALGO_WATCH
- Prior TH batch (TH-1/TH-2/TH-3, 06-24) had three separate fixes flagged; homepage LCP was escalated but remains unresolved — this run adds two new regressions to the same dev queue
