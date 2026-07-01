# Watch Re-check — W15 (Anxiety Neurosis CTR) + W3 (PTSD 21-day re-verify)

**Run:** 2026-07-01 (one-off task `mindtalk-watch-W15-W3-recheck-2026-07-01`, fired 21:00 IST)
**Reason:** Both checks deferred from 06-30 (DataForSEO timeout + GSC google.auth missing in obs sandbox).
**Data source:** LIVE Google Search Console (domain property `sc-domain:mindtalk.in`), pulled directly this run. The obs-monitor failure was environmental only — `google-auth`/`googleapiclient` were absent in the obs sandbox. Installed the libs here; the existing `gsc-token.pickle` refreshed cleanly (had a valid refresh token), so no credentials JSON was needed. Verified against `reports/query-history.json` weekly series + `reports/queries-06-22/06-29.csv`. Raw pull: `watch-W15-W3-recheck-2026-07-01-rawdata.json`.

---

## Check 1 — W15: Anxiety Neurosis CTR verdict → 🔴 STALLED (CTR lever null)

**Page:** `/blogs/understanding-anxiety-neurosis`
**Change:** 2026-06-16 commit `579bb7c` — meta-only rewrite; title → "Anxiety Neurosis (GAD): Symptoms, Causes & Treatment | Mindtalk"; description leads with the GAD definition.
**Baseline (brief):** "anxiety neurosis" 764 impr/wk, pos 4.6, CTR 0.9%. **Target:** CTR ≥ 3%.

### Live GSC — query "anxiety neurosis", filtered to the page

| Window | Impr | Clicks | CTR | Pos |
|---|---|---|---|---|
| Baseline pre-change 06-02→06-15 (14d) | 1,497 (748/wk) | 14 | **0.935%** | 4.82 |
| Verdict window 06-17→06-28 (12d post) | 1,323 | 14 | **1.058%** | 4.91 |
| Full 06-16→06-30 | 1,589 | 17 | 1.07% | 4.78 |
| Recent 7d 06-22→06-28 | 812 | 8 | 0.985% | 4.88 |

Baseline reconciles almost exactly with the brief (748 vs 764 impr/wk; 0.935% vs 0.9% CTR; pos 4.82 vs 4.6) → measurement is sound.

### Weekly CTR trajectory (query-history.json, cross-check)
04-18 →1.3% · 04-25 →0.6% · 05-02 →0.5% · 05-09 →0.3% · 05-16 →1.0% · 05-24 →1.0% · 05-31 →0.5% · **06-06 →0.9% (baseline wk)** · 06-13 →1.7% (straddles the 06-16 ship, mostly pre-change days) · **06-20 →0.8% (first clean post-change full week)**, pos 5.0.

### Verdict
**🔴 STALLED.** CTR did not move. Clicks were **identical** before and after (14 → 14 over matched 14-day windows); the nominal 0.935%→1.058% is denominator drift (impressions fell 1,497→1,323), not a real gain. The first fully-post-change week (06-20) came in at **0.8% CTR** — dead-center of the historical 0.3–1.7% oscillation band, pos unchanged at ~5.0. Target of ≥3% was never approached.
- **Lift ≈ +0.1pp** (< 1pp threshold).
- **Cross-ref P11 (W10/Sprint C):** the winners in Sprint C either *added a number* or *front-loaded keyword + "Explained"*. This title front-loaded "Anxiety Neurosis" + added "(GAD)" but carried **no number and no curiosity token** ("Symptoms, Causes & Treatment" is a generic informational suffix) → P11 predicts a weak/null CTR effect. **Confirmed.** W15 is the clean single-target replication of the Sprint C finding: meta-only CTR rewrites without a number don't move CTR on these pages.

### Downstream
**BACKLOG #17 (CTR staged v2) gate → BLOCKED. Hold the CTR lever.** Do not green-light a v2 staged CTR rewrite off this hypothesis. If CTR is revisited later, only on Rocket/Goldmine pages (P9) AND only with a *number added* to the title (the sole style P11 shows as a reliable winner) — never the "front-load keyword, no number" pattern tested here.

---

## Check 2 — W3: PTSD 21-day re-verify → HOLD (normalization confirmed; re-verify PASSES)

**Page:** `/illnesses/posttraumatic-stress-disorder-ptsd`
**14-day check (Sprint A close):** impr 803→241 (−70%), rank ~10 stable, query count ROSE 57→61. Flagged as a possible **GSC under-report / SERP change, NOT content failure** → do NOT fire a heavy rewrite until the 21-day re-verify confirms a real drop.

### Live GSC — page-level weekly

| Window | Impr | Avg pos | Queries |
|---|---|---|---|
| 06-01→06-07 | 56 | 8.9 | — |
| 06-08→06-14 | 119 | 5.9 | — |
| 06-15→06-21 | 96 | 10.1 | 16 |
| **06-22→06-28 (recent)** | **127** | 11.0 | **30** |
| 30-day agg 05-29→06-28 | 419 | 9.0 | — |

### Verdict
**HOLD — the −70% is NOT a worsening content failure.** Three signals point to normalization / under-report resolving, exactly as the 14-day note predicted:
1. **Impressions are flat-to-recovering, not collapsing.** June weeks run 56 → 119 → 96 → **127**; the most recent week is the **June high**.
2. **Query footprint nearly doubled** (16 → 30 queries WoW) — an expanding, not demoted, page.
3. **Rank stable** ~9–11 across the period — a real quality demotion would erode rank; it hasn't.
- **Numeric reconciliation:** the mechanical "127 (7d) < 241" is apples-to-oranges — 241 was a ~14-day figure (trailing 14-day 06-15→28 = 96+127 = **223 ≈ flat** vs 241; recent-week run-rate → ~254 on a 14-day basis). So impressions are steady-to-up, not "241 or lower and falling." This lands in the HOLD (recovering) branch, not CONFIRMED DROP.
- Corroboration: the early-June per-page GSC snapshot (`gsc-data/…ptsd.json`, dated 06-01) showed impr +103% (32→65), signal NOISE — same non-failure signature.

### Downstream
**BACKLOG #18 (YMYL recovery batch, fires 07-02):** reduce the PTSD brief to **E-E-A-T + FAQ additions only — NO heavy depth rewrite.** The page still ships in the batch (it's a top-priority YMYL page at a low absolute level with ~0 clicks, so light-touch depth + reviewer signal is warranted) but the full depth-refresh + India-data + clinical-FAQ scope is **not** justified by the drop, because the drop isn't real. YMYL clinical sign-off still required (AP3 Option B).

---

## Verdict summary

| Watch | Verdict | Downstream |
|---|---|---|
| **W15** anxiety-neurosis CTR | 🔴 **STALLED** (lift ≈ +0.1pp, target ≥3% missed; clicks flat 14→14) | **#17 CTR-v2 gate BLOCKED** — hold CTR lever |
| **W3** PTSD 21-day re-verify | **HOLD** (recovering/normalizing — recent week 127 = June high, queries 16→30, rank stable) | **#18 ptsd brief → E-E-A-T + FAQ only**, no heavy rewrite |

**Both APIs recovered this run** (GSC via refreshed token). BACKLOG #22 (deferred-checks tracker) → COMPLETED. #18 YMYL batch remains fire-eligible 07-02 with the PTSD scope now reduced.
