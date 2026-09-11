# Stub-Pilot + Hyperactive-ADHD — Day-42 Final Batch

Batch evaluated: 2026-09-05 by T4 (formally documented by T12 2026-09-06)
Ships: 2026-07-24 (W24-W28 mindful-minutes, commit `f8a7429`) + 2026-07-24 (hyperactive-ADHD, commit `713e3ce8`)
Note: Day-42 check date was 2026-09-04; deferred 1 day due to DataForSEO 402. T4 used GSC-only data on 09-05.
Data constraint: DataForSEO blind (402 day 2), Core Update confound (ALGO_WATCH active). GSC-only reads.

---

## URL-by-URL verdicts

### 1. /blogs/hyperactive-vs-inattentive-adhd
Watch context: Day-14 midpoint was not formally tracked (opened alongside stub-pilot batch).
Baseline (Day-14 GSC, Jul 24–Aug 8): pos ~35.9 (T4 observation-2026-08-14.txt)
Day-42 current (T4 09-05, GSC-only): pos ~41.0, impressions declining
Delta: pos −5.1 (further from target), no page-1 establishment
**Verdict: ⚫ WORSE**
Root cause: "hyperactive vs inattentive adhd" is a comparison/definition query. High-DA psychology sites (Healthline, Verywell, ADDitude) dominate. No India-specific angle creates competitive moat. This is a Tier C vocabulary page hitting a globally-competitive SERP.

---

### 2. /mindful-minutes/4-7-8-breathing (W26)
Day-14 baseline (closed 2026-08-09): 🟢 RECOVERED (EXCEPTIONAL) — pos 9.7 avg, "4 7 8 breathing" pos 2.5 (top-3)
Day-42 current (T4 09-05, GSC-only): pos ~36.2
Delta: pos −26.7 (catastrophic regression from Day-14 peak)
**Verdict: ⚫ WORSE**
Root cause: QDF (Query Deserves Freshness) boosted the page during the first 14 days. Boost expired + August Core Update (08-26) accelerated the regression. Global meditation/breathing sites reclaimed positions. Initial Day-14 🟢 EXCEPTIONAL was a QDF false positive — not a durable signal for stub-pilot content class.
Note: T4 flagged as NEEDS_REFRESH on 09-05.

---

### 3. /mindful-minutes/loving-kindness-meditation (W27)
Day-14 baseline (closed 2026-08-09): ⚫ WORSE — 0 impr, global brand lockout (Headspace/Calm/GGSC/Tara Brach DA 80-95+)
Day-42 current (T4 09-05): 0 impressions — no change
**Verdict: ⚫ WORSE (confirmed dark page)**
Root cause: Globally-competitive meditation term. No India-specific angle, no Mindtalk brand authority in this space. AP8 (pos-100 sentinel = noise) applies — this page never achieved even impression-level visibility. Dark page pattern confirmed (2nd data point after anger-management Day-14 close).

---

### 4. /mindful-minutes/morning-energy-activation (W28)
Day-14 baseline (closed 2026-08-09): 🟡 PARTIAL — 71 impr / pos 11.5, near-zero India search volume for exact phrase
Day-42 current (T4 09-05): near-zero impressions, effectively 0 traffic
**Verdict: ⚫ WORSE**
Root cause: "Morning energy activation" is not a search query — it's a content label from the app catalog. Near-zero India volume. P12 exception class E3 analog: content resonates when found (high CTR on adjacency queries) but market is too thin to generate meaningful impressions at any position. Stub-pilot pre-flight gate should include minimum volume threshold check.

---

### 5. /mindful-minutes/panic-attack-grounding (W24)
Day-14 baseline (closed 2026-08-09): 🟢 RECOVERED — 1,297 impr / pos 8.1, "5-4-3-2-1 grounding technique anxiety" pos 3.0
Day-42 current (T4 09-05): 136 impr / 0 clicks / pos ~13
Delta: impr −89.5%, pos +4.9 (regression), CTR 0% (AI Overview absorption)
**Verdict: 🔴 STALLED**
Root cause: "Panic attack grounding" / "5-4-3-2-1 grounding technique" queries now served by AI Overview — zero CTR despite visible ranking. T4 flagged: url_locked=true, B16 (SCHEMA_OPTIMIZATION_NEEDED for AI Overview compatibility) queued post-09-10. This is a new failure mode: rank exists, traffic doesn't, because AI synthesizes the technique directly.

---

### 6. /mindful-minutes/pre-sleep-body-scan (W25)
Day-14 baseline (closed 2026-08-09): 🟡 PARTIAL — 141 impr / pos 8.2 / 0 clicks; competition lockout on primary "body scan for sleep" cluster
Day-42 current (T4 09-05): 3 impressions, effectively 0 traffic
**Verdict: ⚫ WORSE**
Root cause: "Body scan for sleep" dominated by high-DA global sleep meditation sites (Headspace, Calm, Sleep Foundation). 28-day trend: impressions collapsed from 141→3. No recovery path without significant DA growth or hyperlocal India angle pivot.

---

## Batch summary

| URL | Day-14 | Day-42 | Final verdict |
|---|---|---|---|
| hyperactive-vs-inattentive-adhd | not tracked | pos 41.0 | ⚫ WORSE |
| 4-7-8-breathing (W26) | 🟢 EXCEPTIONAL | pos 36.2 | ⚫ WORSE (QDF false positive) |
| loving-kindness-meditation (W27) | ⚫ WORSE | 0 impr | ⚫ WORSE (dark) |
| morning-energy-activation (W28) | 🟡 PARTIAL | ~0 impr | ⚫ WORSE |
| panic-attack-grounding (W24) | 🟢 RECOVERED | 136 impr/0 clicks | 🔴 STALLED (AI Overview trap) |
| pre-sleep-body-scan (W25) | 🟡 PARTIAL | 3 impr | ⚫ WORSE |

**Score: 0🟢 / 0🟡 / 1🔴 / 5⚫ — 100% stalled/worse**

---

## Pattern analysis

**Not yet at 3+ failures for a single root cause → no new ANTI-PATTERN written this run.**

However, two emerging patterns noted (candidates for future AP when 3rd data point arrives):

1. **QDF false positives on stub-pilot content**: 4-7-8-breathing peaked at pos 2.5 at Day-14 then crashed to pos 36.2 by Day-42. This is the same pattern as any new page getting a freshness boost that evaporates. Stub-pilot Day-14 evaluations should be treated as preliminary — Day-42 is the real verdict. (1st formal data point)

2. **AI Overview absorption on grounding techniques**: panic-attack-grounding ranked pos 13 but drove 0 clicks because AI Overview synthesizes the technique inline. Pure how-to content with step-by-step instructions is at highest risk. (1st formal data point — B16 action queued)

3. **Dark page pattern confirmed**: loving-kindness-meditation + anger-management (W34) = 2 confirmed dark pages. Both are globally-competitive meditation/psychology head terms with no India-specific angle. Pre-flight gate needed: check DA of top-3 SERP. If all DA>70, mark as dark_risk. (2nd data point)

---

## Watches to formally close

W24 (panic-attack-grounding): 🔴 STALLED — keep open for B16 schema optimization; url_locked=true
W25 (pre-sleep-body-scan): ⚫ WORSE — close, no action path
W26 (4-7-8-breathing): ⚫ WORSE — close; NEEDS_REFRESH flagged (T4 09-05)
W27 (loving-kindness-meditation): ⚫ WORSE — close (dark page confirmed)
W28 (morning-energy-activation): ⚫ WORSE — close (thin market confirmed)
Hyperactive-ADHD blog: ⚫ WORSE — no named watch; close inline

⚠ LEARNER FLAG: 5⚫ + 1🔴 out of 6 = 100% stalled/worse on stub-pilot Day-42 batch. This is the worst single-batch outcome in system history. The stub-pilot batch 2 pilot (10-item) must incorporate the pre-flight gates identified above before firing.
