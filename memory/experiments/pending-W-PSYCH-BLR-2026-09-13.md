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
