# Watch W-COUN-BLR-20260821 — PENDING_EVALUATION (data error)

URL: /doctors/counsellors-in-bangalore
Action that opened watch: COUNSELLORS-BANGALORE-THIN-01 (T11 — commit 7163c6793b3c)
Opened: 2026-08-21 | Deferred check: 2026-09-10 (post ALGO_WATCH clear) | Evaluation attempted: 2026-09-13
Regression at watch open: "counselling bangalore" at pos 51

Baseline metrics: pos 51 on "counselling bangalore" (thin content diagnosis).
Current metrics: UNAVAILABLE — GSC file `gsc-data/doctors_counsellors-in-bangalore.json` stale (pulled 2026-08-14, 0 impr). Disk full prevents fresh pull. Weekly summary shows no specific counselling bangalore query mention.
Delta: CANNOT COMPUTE

Verdict: PENDING_EVALUATION (data error — disk full + very stale GSC file, 30 days old)
Notes:
- Per weekly summary 08-28 (T17): "counselling" at pos 9→4 (90.5K/mo) — strongest WoW positions in site history. This may be the /doctors/counsellors-in-bangalore page or a blog page. If correct, this would be a major recovery (pos 51→4 range).
- T17 data is KW-dimension across all pages; cannot confirm this is the counsellors-in-bangalore page specifically.
- GSC-INFRA-01 disk full is the blocking issue.
- CRITICAL: This watch has the most stale data (GSC pulled 2026-08-14, now 30 days old — approaching the 30-day staleness threshold for GSC data reliability).
- Re-evaluate urgently after disk space freed.


---
## T20 ADDENDUM — 2026-09-13 23:20 IST (fresh data; verdict still T12's)
The zero was pull-side (stale/mis-formatted file + sandbox `/sessions` disk full). GSC is reachable with
`HOME=/tmp XDG_CACHE_HOME=/tmp TMPDIR=/tmp PYTHONPATH=.pip-packages python3 scripts/gsc-pull.py --url /doctors/counsellors-in-bangalore` — file refreshed 2026-09-13 23:01 IST.
Page dimension (canonical host, no -L):
- pre  2026-07-24→2026-08-20: {'clicks': 20, 'impressions': 2841, 'position': 15.7} (101.5 impr/day)
- post 2026-08-22→2026-09-11: {'clicks': 14, 'impressions': 2203, 'position': 14.1} (104.9 impr/day)
Target query "counselling bangalore" at dimensions=[query] (property-level, rule f): pre {'clicks': 2, 'impressions': 82, 'position': 26.5} → post {'clicks': 2, 'impressions': 79, 'position': 30.7}
Pages holding the query in the post window (path, impr, clicks, pos): [['/centers/indiranagar?utm_source=GMB&utm_medium=Organic', 27, 1, 5.7], ['/treatments/counselling-therapy', 18, 1, 10.5], ['/', 2, 0, 1], ['/blogs/affordable-therapy-bangalore', 1, 0, 2], ['/blogs/therapy-cost-in-india', 1, 0, 2], ['/centers/indiranagar', 11, 0, 21.1], ['/centers/kalyan-nagar', 11, 0, 60.3], ['/centers/kalyan-nagar?utm_source=GMB&utm_medium=Organic', 1, 0, 6], ['/doctors/clinical-psychologists-in-bangalore', 8, 0, 86], ['/doctors/counsellors-in-bangalore', 8, 0, 48.6]]
Daily tail (date, impr, clicks): [['2026-09-07', 114, 0], ['2026-09-08', 128, 1], ['2026-09-09', 100, 0], ['2026-09-10', 132, 2], ['2026-09-11', 96, 0]]
Negative control (garbage path): 0 impressions. Full JSON: logs/t20-gsc-watch-verify-2026-09-13.json. See WATCH.md T20 correction block 2026-09-13.
