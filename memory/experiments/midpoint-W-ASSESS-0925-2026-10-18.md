# W-ASSESS-0925 — Day-21 Midpoint Evaluation (NOT CLOSED)

**Evaluation date:** 2026-10-18
**Watch group:** W-ASSESS-*-0925 (Assessments Sprint, opened 2026-09-25)
**Day-42 close date:** 2026-11-06
**Status:** MIDPOINT ONLY — do not close, do not write principles yet

**Data source:** gsc-data/*.json files, pulled 2026-10-16 (Windows: current Oct 6-13, previous Sep 29–Oct 6)
**Proxy method:** 14d actual = current_window + previous_window (2× 7d). Normalized 90d baseline = baseline_metric / 90 × 14.
**Constraint:** AP12 — url_locked until 2026-11-06. No content changes to any assessment page.

---

## Summary Table

| Watch ID | URL | Baseline clicks/impr (90d) | 14d Norm Baseline | 14d Actual | Position | Verdict |
|---|---|---|---|---|---|---|
| W-ASSESS-GAD7-0925 | /assessments/gad-7 | 922 / 39,059 | 143 / 6,076 | 326 / 11,671 | 9.0→7.4 | 🟢 ON_TRACK |
| W-ASSESS-YBOCS-0925 | /assessments/y-bocs | 574 / 42,683 | 89 / 6,638 | 261 / 11,562 | 6.9→3.6* | 🟢 ON_TRACK |
| W-ASSESS-LLQ-0925 | /assessments/love-language-quiz | 314 / 38,716 | 49 / 6,024 | 276 / 28,259 | 9.2→8.2 | 🟢 EXCEPTIONAL |
| W-ASSESS-BPD-0925 | /assessments/am-i-borderline-test | 522 / 15,447 | 81 / 2,403 | 285 / 5,504 | 9.1→6.1 | 🟢 ON_TRACK |
| W-ASSESS-ACE-0925 | /assessments/ace-test | 91 / 11,594 | 14 / 1,804 | 27 / 2,803 | 10.7→9.2 | 🟢 ON_TRACK |
| W-ASSESS-DASS-0925 | /assessments/dass-21 | 76 / 2,925 | 12 / 455 | 44 / 2,010 | 9.0→6.9 | 🟢 EXCEPTIONAL |
| W-ASSESS-EI-0925 | /assessments/emotional-intelligence-test | 48 / 2,575 | 7.5 / 401 | 40 / 1,083 | 10.7→4.7 | 🟢 EXCEPTIONAL |
| W-ASSESS-AUTISM-0925 | /assessments/autism-test | 96 / 6,330 | 15 / 984 | 60 / 2,404 | 16.6→11.6 WoW reg. | 🟡 WATCH |
| W-ASSESS-CSSRS-0925 | /assessments/c-ssrs | 71 / 16,623 | 11 / 2,585 | 6 / 1,563 | 9.2→8.9 | 🔴 STALLED |
| W-ASSESS-EAT26-0925 | /assessments/eat-26 | 6 / 1,330 | 0.9 / 207 | 2 / 396 | 13.0→25.2 COLLAPSE | 🔴 STALLED |
| W-ASSESS-CUBE-0925 | /assessments/cube-test | 0 (NEW) | — | 26 / 1,208 | pos 6.3 page-1 ✓ | 🟢 EXCEPTIONAL |
| W-ASSESS-HUBS-0925 | /assessments hubs | grouped | — | DATA_LIMITED | — | DATA_LIMITED |
| W-ASSESS-NEW8-0925 | 8 NEW pages | grouped | — | DATA_LIMITED | — | DATA_LIMITED |
| W-ASSESS-BYLINE-0925 | section CTR | section aggregate | — | DATA_LIMITED | — | DATA_LIMITED |
| W-ASSESS-INDEX-0925 | psychometric cluster | cluster | — | DATA_LIMITED | — | DATA_LIMITED |
| W-ASSESS-308-0925 | 33 orphan 404s | crawl check | — | DATA_LIMITED | — | DATA_LIMITED |

*W-ASSESS-YBOCS: HIGH_PRIORITY_DROP signal (WoW impr -20.5%, clicks -13.6%) — overall 14d vs norm positive but momentum declining. Monitor at Day-42.

**Evaluable watches with data (11):**
- 🟢 ON_TRACK / EXCEPTIONAL: 9 (82%)
- 🟡 WATCH: 1 (9%)
- 🔴 STALLED: 2 (18%)
- ⚫ WORSE: 0

Stalled/Worse rate 18% — below 50% threshold. No LEARNER FLAG.

---

## Individual Watch Notes

### W-ASSESS-GAD7-0925 — 🟢 ON_TRACK
- 14d actual: 326 clicks / 11,671 impr | norm baseline: 143 / 6,076
- Delta: +128% clicks, +92% impr, pos improved 9.0→7.4
- Strong lift. Position trending toward page-1 top. Day-42 to confirm CTR target.

### W-ASSESS-YBOCS-0925 — 🟢 ON_TRACK (WoW pullback flagged)
- 14d actual: 261 / 11,562 | norm baseline: 89 / 6,638
- Delta: +193% clicks, +74% impr, pos exceptional 6.9→3.6
- HIGH_PRIORITY_DROP: WoW impr -20.5%, clicks -13.6%. Position at 3.6 is still excellent but declining WoW. May be QDF normalization. AP12 lock; no action. Monitor at Day-42.

### W-ASSESS-LLQ-0925 — 🟢 EXCEPTIONAL
- 14d actual: 276 / 28,259 | norm baseline: 49 / 6,024
- Delta: +466% clicks, +369% impr, pos stable 9.2→8.2
- Near-5× click multiplier. "love language quiz" query cluster expanded massively. Strong candidate for P-ASSESS principles at Day-42.

### W-ASSESS-BPD-0925 — 🟢 ON_TRACK
- 14d actual: 285 / 5,504 | norm baseline: 81 / 2,403
- Delta: +252% clicks, +129% impr, pos improved 9.1→6.1
- Position approaching target ≤6. Near-3× vs baseline. Day-42 to confirm.

### W-ASSESS-ACE-0925 — 🟢 ON_TRACK
- 14d actual: 27 / 2,803 | norm baseline: 14 / 1,804
- Delta: +93% clicks, +55% impr, pos improved 10.7→9.2
- Solid but moderate. Low query volume family. Expected steady-state by Day-42.

### W-ASSESS-DASS-0925 — 🟢 EXCEPTIONAL
- 14d actual: 44 / 2,010 | norm baseline: 12 / 455
- Delta: +267% clicks, +342% impr, pos improved 9.0→6.9
- Target was ≤15 — already page 1 at 6.9. Nearly 3.7× click lift from low base.

### W-ASSESS-EI-0925 — 🟢 EXCEPTIONAL
- 14d actual: 40 / 1,083 | norm baseline: 7.5 / 401
- Delta: +433% clicks, +170% impr, pos dramatic 10.7→4.7 (top 5)
- Click volume growing WoW (11→29). Candidate for plain-English retarget principle at Day-42.

### W-ASSESS-AUTISM-0925 — 🟡 WATCH
- 14d actual: 60 / 2,404 | norm baseline: 15 / 984
- Delta: +300% clicks, +144% impr, BUT pos REGRESSING WoW 8.4→11.6
- Click count vs norm is excellent but position moving wrong direction. May be query mix shift or new competitor. AP12 lock; no action until 2026-11-06. Flag for T10 at Day-42.

### W-ASSESS-CSSRS-0925 — 🔴 STALLED
- 14d actual: 6 / 1,563 | norm baseline: 11 / 2,585
- Delta: -45% clicks, -40% impr vs normalized baseline
- CTR: 0.38% — below 0.43% pre-sprint baseline, far below 1%+ target
- C-SSRS is a specialized clinical instrument with limited organic volume (clinicians/researchers not patients). Plain-English retarget may not apply here. Action review at Day-42; may need "suicide risk assessment" clinical-query repositioning.

### W-ASSESS-EAT26-0925 — 🔴 STALLED
- 14d actual: 2 / 396 | norm baseline: 0.9 / 207
- Position COLLAPSED 12.2→25.2 WoW (from page 2 to page 3+)
- Possible cause: EAT-26 has strict copyright restrictions on item content — check if AP15 was applied correctly; inadvertent item reproduction could trigger quality penalty. Flag for T10 at Day-42. AP12 lock applies.

### W-ASSESS-CUBE-0925 — 🟢 EXCEPTIONAL (P12 midpoint confirmation)
- 14d actual: 26 / 1,208 | baseline: 0 (NEW page)
- Position: 6.3 current (page 1) — target was page-1 by Day-42 → ACHIEVED before Day-21
- WoW: impr growing 431→777 (+80%), clicks growing 8→18 (+125%)
- P12 confirmed at midpoint for this assessment URL. NOT stub-pilot class; QDF_RISK_INTERIM does NOT apply. Standard Day-42 evaluation.

### DATA_LIMITED watches (5)
- W-ASSESS-HUBS-0925: hub pages — need hub-level GSC pull
- W-ASSESS-NEW8-0925: 8 NEW assessment pages — need individual gsc-data files
- W-ASSESS-BYLINE-0925: section-level CTR — requires section-aggregate pull
- W-ASSESS-INDEX-0925: cluster psychometric indexation — aggregate metric
- W-ASSESS-308-0925: 33 orphan 404s — requires crawl/HTTP check
All deferred to Day-42 (2026-11-06).

---

## Candidate Principles Status

**(a) Clinician byline + evidence section lifts CTR on YMYL tool pages**
Status: SEEDED. GAD-7, BPD, EI showing CTR/position improvement. C-SSRS showing decline despite byline. Cannot write principle at Day-21. CHECK AT 2026-11-06.

**(b) Plain-English "X test" retarget beats acronym titles**
Status: SEEDED. EI (+433%), LLQ (+466%), BPD (+252%) support the hypothesis. C-SSRS (clinical acronym retained, stalling) also supports it. Cannot write principle at Day-21. CHECK AT 2026-11-06.

**(c) P12 holds for NEW assessment pages**
Status: CONFIRMED at midpoint for W-ASSESS-CUBE-0925. Will confirm definitively at Day-42 when W-ASSESS-NEW8-0925 data available.

---

## Next Evaluation

**All W-ASSESS-*-0925 → Day-42 close: 2026-11-06**
Action required: Run gsc-pull.py with page-dimension (AP13/AP14) for all assessment URLs + hub pages. Compare against 90d baselines using normalized window formula.
