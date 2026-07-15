# Technical Health History

Appended weekly by Task 14 (mindtalk-technical-health-monitor). Used for trend analysis.

| Date | Score | Indexation % | CWV avg perf | Broken links | Schema issues | Notes |
|---|---|---|---|---|---|---|
| 2026-06-24 | 78/100 | 139% (949 indexed / 683 sitemap) | 96.6 (non-homepage) | 0 | 4 | BASELINE. Homepage LCP=10.95s CRITICAL. All other pages CWV healthy. |
| 2026-07-01 | 75/100 | ~138% (sitemap 688, +5) | 84.3 (non-homepage) | 0 | 4 | 🚨 TWO NEW CRITICAL pages: /treatments/counselling-therapy LCP 1.65s→9.26s (+460%); /assessments TBT 179ms→2923ms (+16×). Homepage LCP marginally improved 10.95s→10.22s. "counselling" organic rank dropped #9→absent. |
| 2026-07-08 | 85/100 | ~137% (sitemap 692, +4) | 95.6 (8 pages; 2 PSI timeouts) | 0 | 4 | ✅ MAJOR RECOVERY. All 3 CWV criticals resolved: homepage LCP 10.22s→2.55s (−74%); counselling-therapy LCP 9.26s→1.65s (full recovery); assessments TBT 2923ms→310ms (full recovery). "counselling" rank recovering (LCP driver fixed). Schema issues unchanged (4 pages). Best score since baseline. |
| 2026-07-15 | 60/100 | unknown (GSC OAuth expired) | 69 (8 pages; 2 PSI timeouts) | 0 | 4 | 🚨 CRITICAL REGRESSION. 7/8 pages LCP 9–11s (was green last week). Homepage 2.55s→10.55s (+315%); counselling-therapy 1.65s→11.06s (+570%); all page types affected. Only /assessments acceptable (4.01s, 85 perf). FCP fast (1.05s) + slow LCP = large element in global layout. Suspected: nav commit 1e007b8 + corporates feature fbc6235 (07-10 to 07-14 deploy window). flag_for_human added to BACKLOG. config.json doctors-listings URL bug found (wrong prefix). |
