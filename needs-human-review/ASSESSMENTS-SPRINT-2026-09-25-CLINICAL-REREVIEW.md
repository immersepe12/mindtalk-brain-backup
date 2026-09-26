> ✅ **CLOSED 2026-09-25** — Kushal: all clinicians have signed off in-app. Best-suited senior reviewers assigned (commit on branch `assessments-reviewers-2026-09-25`): wender-utah, asrs → Dr Krishna K R · ham-d, phq-9 → Dr Rangapriya Raghavan · ham-a, y-bocs, body-dysmorphia → Dr Vishal Kasal · stai, ders-16, am-i-borderline-test, bsl-23, npi, emotion-regulation → Ms Sufia Nusrat · pcl-5, autism-test, anger, big-5, rses, personality-and-identity → Ms Smicky Priya Das · ace-test, emotional-intelligence, imposter, perfectionism, stress-tolerance, emotions-and-reactions, eat-26, bes, eating-disorders-body-image → Ms Suhita Saha · personality-disorders → Dr Arun Kumar. The 3-yr reviewer (anuja-jain) removed from all 15 assessment pages. **Still open (product, not clinical):** confirm app matches page on HAM-D max score, Wender-Utah cut-off, EI report grouping, THI/SHI item counts, new-test time estimates.

# Assessments sprint 2026-09-25 — clinical re-review list

Shipped live in commit c9b9b731 under Kushal's standing instruction (assume validated; clinical sign-off is Kushal's responsibility). These are the changes that altered a clinical number or claim on a previously signed-off page — route to the named reviewer for confirmation.

| Page | Change | Reviewer to confirm |
|---|---|---|
| wender-utah | Cut-off 36+ → 46+ (Ward et al. 1993 validation) | page reviewer |
| pcl-5 | Bands now 0–30 / 31–33 / 34–80 (Bovin 2016); removed "validated in India" (Patel 2022 says not) | page reviewer |
| ham-d | Range 0–53 → 0–52 (17-item sum). Confirm what the app reports | page reviewer + app team |
| ham-a | Bands aligned to Matza 2010 | page reviewer |
| stai | Unverified 20-40/40-60/60-80 bands replaced with published 39-40 cut point (54-55 older adults) | page reviewer |
| y-bocs | Treatment response 25% → ≥35% (Mataix-Cols 2016 consensus) | page reviewer |
| ace-test | Study size 17,000/10 cats → 9,508/7 (Felitti 1998) | page reviewer |
| asrs / autism-test / body-dysmorphia-test | Corrected sample sizes + accuracy figures | page reviewer |
| phq-9 | Publication year 1999→2001; removed incorrect STAR*D claim | page reviewer |
| ders-16 | Subscale item counts from scoring key (full paper not accessible) | page reviewer |
| emotional-intelligence-test | BEIS-10 is 5 factors; page says app report groups into 4 areas — **product to confirm app grouping** | product |
| panic-disorder-test, stress-tolerance-test | Result-profile tables describe app output — **product to confirm** | product |
| tinnitus-handicap-inventory, sleep-hygiene-index | question_count 25 / 13 (published lengths) — **confirm app uses full versions** | product |
| 6 new self-test pages | time_minutes estimated (5 / 7) — shows in CTA label | product |
| bsl-23, bes (gated, left) | Still carry unverified India-validation + NIMHANS/AIIMS claims — needs clinical/safe-messaging pass | clinical |
| Many pages | Unverified India-validation / prevalence claims REMOVED or softened (see changelogs) | FYI |

Full per-page changelogs: outputs/stage/changelog/*.json (copied to reports/assessments-sprint-2026-09-25-changelogs/).
