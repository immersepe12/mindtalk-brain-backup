# Watch W-PSYCH-BLR-20260821 — PENDING_EVALUATION (data error)

URL: /doctors/psychologists-in-bangalore
Action that opened watch: PSYCHOLOGISTS-BANGALORE-REFRESH-01 (T11 — commit 7163c6793b3c, +900w, 4 new H2s, 2 new FAQs)
Opened: 2026-08-21 | Deferred check: 2026-09-10 (post ALGO_WATCH clear) | Evaluation attempted: 2026-09-13
Regression at watch open: "adult psychologist near me" dropped pos 5→8

Baseline metrics (at watch open): pos 8 on "adult psychologist near me", ALGO_WATCH active — deferring
Current metrics (proxy only): Weekly summary 08-31→09-06 shows "psychologist near me" pos 8.1, 3,208 impr — closely related query (not exact match to "adult psychologist near me"). Per-page GSC file `gsc-data/doctors_psychologists-in-bangalore.json` stale (pulled 2026-08-27, 0 impr — disk full prevents fresh pull).
Delta (proxy): "psychologist near me" pos ~8.1 vs baseline drop to pos 8 = roughly neutral (not recovered to pre-regression pos 5).

Verdict: PENDING_EVALUATION (data error — stale per-page GSC data; proxy suggests no recovery yet)
Notes:
- ALGO_WATCH cleared 2026-09-10. Evaluation is now valid.
- Proxy evidence (weekly summary "psychologist near me" pos 8.1) suggests position has not recovered to pre-regression pos 5. The refresh may have stabilized without fully recovering.
- Requires per-page dimension GSC pull with path format (/doctors/psychologists-in-bangalore) for definitive verdict.
- Re-evaluate next Learner run.


---
## T20 ADDENDUM — 2026-09-13 23:20 IST (fresh data; verdict still T12's)
The zero was pull-side (stale/mis-formatted file + sandbox `/sessions` disk full). GSC is reachable with
`HOME=/tmp XDG_CACHE_HOME=/tmp TMPDIR=/tmp PYTHONPATH=.pip-packages python3 scripts/gsc-pull.py --url /doctors/psychologists-in-bangalore` — file refreshed 2026-09-13 23:01 IST.
Page dimension (canonical host, no -L):
- pre  2026-07-24→2026-08-20: {'clicks': 88, 'impressions': 13755, 'position': 26.5} (491.2 impr/day)
- post 2026-08-22→2026-09-11: {'clicks': 67, 'impressions': 16597, 'position': 18.1} (790.3 impr/day)
Target query "adult psychologist near me" at dimensions=[query] (property-level, rule f): pre {'clicks': 0, 'impressions': 2, 'position': 5} → post {'clicks': 0, 'impressions': 2, 'position': 4}
Pages holding the query in the post window (path, impr, clicks, pos): [['/doctors/psychologists-in-bangalore', 2, 0, 4]]
Daily tail (date, impr, clicks): [['2026-09-07', 515, 0], ['2026-09-08', 2580, 4], ['2026-09-09', 426, 1], ['2026-09-10', 1210, 5], ['2026-09-11', 544, 1]]
Negative control (garbage path): 0 impressions. Full JSON: logs/t20-gsc-watch-verify-2026-09-13.json. See WATCH.md T20 correction block 2026-09-13.
