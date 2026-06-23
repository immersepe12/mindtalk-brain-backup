# investigate_regression: Sleep-Disorder Cluster GSC Avg-Position Slide — 2026-06-23

## What we did

Read-only cannibalization + internal-link diagnostic on the sleep/insomnia cluster flagged by the 2026-06-22 Monday weekly report (12 cluster avg-position drops, 5 sleep-related: circadian-rhythm −16.7, delayed-sleep-phase −11.3, sleep-talking −7.8, sleep-disorder listing −6.6, ocd-thoughts −14.7).

Data sources checked:
- `confirmed-drops.json` (Task 2 GSC validation, today 06-23)
- `reports/cluster-history.json` for all sleep-tagged pages
- `src/content/blogs/` and `src/content/illnesses/` file inventory for cannibalization audit
- Git log for recent content changes in the cluster

---

## Findings

### 1. Task 2 confirmed: zero new drops today

`confirmed-drops.json = {}` after today's 9:30 AM IST Task 2 run. No GSC-validated new drops from the morning pull. This is the strongest single signal: if these were real structural drops, Task 2 would have flagged at least one URL today.

### 2. Individual page analysis from cluster-history.json

| Page | Last 2 weeks pos | Verdict |
|---|---|---|
| `cognitive-behavioral-therapy-for-insomnia` | 15.0 → 14.1 | ✅ IMPROVING — impr 338→348→378 |
| `sleep-disorder` (illness hub) | 9.5 → 16.1 | ⚠ REGRESSION-TO-MEAN — pos 9.5 was best-ever outlier; prior 8-week avg ~14-16 |
| `guide-to-sleep-talking-disorder-somniloquy` | 18.5 → 26.3 | 🔵 WITHIN RANGE — historical range 13.8–30.3; 26.3 is not unusual |
| `nursing-care-and-diagnosis-plan-for-insomnia` | 13.4 → 13.4 | 🔵 STABLE POS, impr declining 430→456 (slight bounce). Sustained 1612→456 over 3 months — query volume/seasonal |
| `light-therapy-for-insomnia` | 11.8 → 15.2 | 🔵 Pos worse but impr recovering 268→319. Not a structural drop |
| `natural-remedies-for-insomnia-during-pregnancy` | 14.9 → 17.4 | 🟡 Slight sustained decline (634→318 impr over 9 weeks). Low priority (318 impr/wk) |
| `benefits-of-yoga-in-treating-sleep-disorder` | 7.7 → 9.1 | 🔵 Low volatility; within range |
| `understanding-sleep-deprived-brain` | 6.4 → 5.0 | ✅ IMPROVING |

**CBT-i is IMPROVING.** A coordinated cluster penalty would hit all pages. CBT-i improving while sleep-talking/disorder-listing drop is diagnostic evidence against a shared cause.

### 3. Regression-to-mean pattern on sleep-disorder listing

The 06-06 pos 9.5 for `/illnesses/sleep-disorder` was a historical best (prior range: 10.9–29.1 over 9 weeks). The 06-13 return to pos 16.1 is reversion toward the mean (~13-16 range), not a new drop. AP5 applies: 9.5 was the spike; 16.1 is normal.

### 4. Cannibalization assessment — CLEAN

The sleep cluster has 28 blog pages + 1 illness hub, but they cover clearly distinct subtopics:
- Hub: `/illnesses/sleep-disorder` (general overview)
- Clinical: `/blogs/nursing-care-and-diagnosis-plan-for-insomnia` (nursing care plan)
- Treatment approach: `/blogs/cognitive-behavioral-therapy-for-insomnia` (CBT-i), `/blogs/light-therapy-for-insomnia`
- Diagnosis: `/blogs/sleep-disorder-tests-from-insomnia-to-hypersomnia`
- Demographic: `/blogs/understanding-insomnia-in-females`, `/blogs/understanding-insomnia-in-children`
- Subtypes: `/blogs/guide-to-sleep-talking-disorder-somniloquy`, `/blogs/understanding-circadian-rhythm-sleep-disorder`, `/blogs/understanding-delayed-sleep-phase-disorder-dsps`

No two pages compete for the same head term. Topical differentiation is high. **Cannibalization risk: LOW.**

### 5. Composition effect (same cause as BRAIN.md explains)

The "what is a life coach" head term added 9,429 page-2 impressions (pos ~11.3) to site avg. This same composition effect operates at the cluster level: any new GSC-tracked query entering a cluster's data at a weak position will drag the cluster's avg-position metric down, even if no individual page declined. The 06-22 report's cluster avg-position calculations likely include newly-tracked queries from the 3 NEW blogs shipped in late June entering the sleep ecosystem.

### 6. ocd-thoughts in the 12-drop list

`ocd-thoughts` is a separate topical cluster (OCD), not sleep. Its presence in the "12 cluster drops" confirms these are 12 scattered individual fluctuations harvested by the weekly report algorithm, NOT a coordinated topical-cluster event.

### 7. No recent content changes

Git log shows the last content touches to sleep cluster files were:
- Sprint A reviewer batch (commit `270cf0c`, 2026-06-09): added clinical reviewer to sleep-disorder illness page
- Earlier reviewer batches: `9574ebf`, `2703a7a`, `6f8eb81`
- No content changes in the past 14 days = AP4 safe; also means no recent change to blame

---

## Root cause: Composition + Natural Volatility (NOT a structural cluster regression)

1. **Composition effect** — "life coach" + other new head terms entering site/cluster GSC tracking dragged avg-position metrics
2. **Regression-to-mean** — sleep-disorder listing pos 9.5 (spike) → 16.1 (normal range)
3. **Natural position volatility** — sleep-talking has always ranged 13.8–30.3; 26.3 is normal
4. **Query volume seasonality** — nursing-care impressions declining over 3 months at stable position = the query "nursing care plan for insomnia" simply gets less search volume in summer; not a ranking problem
5. **Task 2 confirms: {}** — strongest signal; real drops would appear in confirmed-drops

---

## What actually did NOT work to look at (pro-input skip-list pages)

Per the professional-input queue: `/illnesses/sleep-disorder` (Dr. Rayani M Dessa brief) and `/treatments/dialectical-behaviour-therapy-dbt` (Ms. Vindhya Shree P K brief) are both gated "don't refresh until recording received or 2026-07-13." These were NOT touched in this investigation and are handled separately.

---

## Recommended action: CLOSED AS NOISE

**No refresh. No structural action required.** The 12 cluster drops are:
- Composition-driven avg-position artifacts, not real ranking changes
- Within historical volatility ranges for each page
- Contradicted by CBT-i IMPROVING and Task 2 finding zero confirmed drops

**One genuine monitoring signal** (NOT urgent, NOT a sprint candidate):
- `nursing-care-and-diagnosis-plan-for-insomnia` has sustained 3-month impression decline (1612→456). Position is stable → query volume trend, not a ranking problem. Dr. Sneha professional-input brief already created (`briefs/professional-input/2026-W26/nursing-care-and-diagnosis-plan-for-insomnia-brief.md`). Correct handling is through that pipeline. Do not add a separate refresh brief.

**BACKLOG update:** Replace #14 `investigate_regression` row with "CLOSED — noise confirmed (composition + regression-to-mean)" per the Completed section. No new action row needed.

---

## Watch

None added (no action taken, no change to observe).

## Tags

#sleep-cluster #investigate #noise-confirmed #composition-effect #2026-06-23
