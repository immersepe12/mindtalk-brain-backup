# Watch W-BLR-THERAPISTS-0918 — QDF_BLOCKED (extended to 2026-12-11)

URL: /doctors/therapists-in-bangalore
Action that opened watch: Meta CTR update (same batch as Delhi therapists, 2026-09-18)
Opened: 2026-09-18 | Day-42 check: 2026-10-30 | T4 pre-recorded: 2026-10-30 | Evaluated: 2026-11-01

---

Baseline metrics (2026-09-11 → 2026-09-18):
  Avg Position: 16.2 | Clicks: ~9/wk | Impressions: ~1,500

Day-14 metrics: pos 20.0 (worsening noted in T4)
url_locked from 2026-09-18 → 2026-10-30 (AP12: no edits during observation window)

Day-42 current metrics (CW 2026-10-19 → 2026-10-26):
  Clicks: 7 | Impressions: 1,238 | Avg Position: 26.3

Previous window (2026-10-12 → 2026-10-19):
  Clicks: 9 | Impressions: 1,639 | Avg Position: 21.3

Delta from baseline to Day-42:
  Position: 16.2 → 26.3 (worsening, -10.1 pos)
  Clicks: -22% (9 → 7)
  Impressions: -18% (1,500 → 1,238)

External confound check:
- ALGO_WATCH: CLEARED 2026-10-15. No active Core Update.
- QDF guard: Does NOT apply here — the position worsened from Day-1 (not a positive QDF spike that normalized).
- T4 classification (2026-10-30): QDF_BLOCKED. T4 may be applying "QDF_BLOCKED" in the sense of
  "uncertain — possible algorithm interference, extended evaluation window needed" rather than the strict
  QDF definition. T10 Strategist confirmed: "therapists-in-bangalore QDF_BLOCKED to 2026-12-11 (no edits, AP12)"

T12 assessment: The position trend is genuinely worsening (16.2 → 20.0 Day-14 → 26.3 Day-42).
However, per AP12: the url_locked observation window prevents editing during this period.
T4 has extended the watch to 2026-12-11 (Day-84 equivalent) to distinguish algorithm noise from true signal.

Verdict: QDF_BLOCKED (NOT closed) — watch extended to 2026-12-11
AP12 constraint: No edits to this page until 2026-12-11.
Next evaluation: T12 2026-12-07 or 2026-12-14 (whichever T12 run falls near the close date).

Note for pattern extraction:
The contrast with therapists-in-delhi (same meta update batch, same date) is striking:
  - Delhi: baseline CTR 0.04%, meta rewrite → 3.3% CTR, massive click lift ✅
  - Bangalore: same meta rewrite strategy, position worsening throughout window ❌
Possible hypothesis: Meta CTR update works when baseline position is strong enough (pos <10);
at pos 16.2, the update may not compensate for competitive query dynamics.
This is 1 data point — not enough for an anti-pattern. Flag for future P11/AP consideration.
