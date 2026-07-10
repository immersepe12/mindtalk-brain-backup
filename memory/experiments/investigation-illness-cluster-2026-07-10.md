# investigate_regression on illness-cluster — 2026-07-10

## What we did

Investigated the ILLNESS-CLUSTER-01 signal: illness_page_viewed −27% WoW (Mixpanel T19 W28: 161→118) combined with DataForSEO weekly summary (Jun 27–Jul 3) showing psychosis −34.2 positions (12.7→46.9). Ran during active June Core Update (Jun 30–Jul 17, 2026).

## Data sources consulted

| Source | Coverage window | Key finding |
|---|---|---|
| Mixpanel T19 W28 (BRAIN.md) | W28 (Jul 1–8) | illness_page_viewed −27% WoW (161→118) |
| weekly-summary-2026-07-06.txt | Jun 27–Jul 3 | psychosis −34.2 pos (12.7→46.9); Addiction Treatment +25.7% |
| gsc-data/illnesses_psychosis.json | Jun 20–27 (stale) | avg_pos 29.2, 73 impr — predates the drop window |
| rank-history.json (07-10 pull) | 2026-07-10 | psychosis pos=9; anxiety pos=9; depression pos=9; schizophrenia pos=12; stress-disorder pos=11; drug-addiction pos=100 (AP8 sentinel) |
| confirmed-drops.json | current | `{}` — zero confirmed drops |
| WATCH.md | current | No open watch on psychosis or illness cluster |
| BRAIN.md Strategist 07-09 | 07-09 | "0 CRITICAL/MAJOR rank drops. 2 MODERATEs = NOISE (ACT+rTMS — GSC IMPROVING)" |

## What's the actual signal?

**Psychosis drop:** DataForSEO Jun 27–Jul 3 reported −34.2 pos (12.7→46.9). Today's DataForSEO pull (07-10) shows psychosis back at pos=9. Pattern matches a QDF (Query Deserves Freshness) fluctuation or brief Core Update volatility that self-corrected within ~7 days. The prior WATCH.md note "Psychosis HIGH → NOISE (GSC impr +25.9% IMPROVING)" from late June is consistent with a chronically volatile query, not a structural ranking loss.

**illness_page_viewed −27%:** Real Mixpanel event signal (161→118 events). However:
- Overall site page views W28 stable (no broad traffic crash)
- Addiction Treatment cluster IMPROVING +25.7% (contradicts broad illness cluster drop)
- Most DataForSEO drops in Jun 27–Jul 3 were /treatments/ pages (psychotherapy −14.7, music therapy −14.7, eclectic therapy −10.2), NOT /illnesses/*
- illness_page_viewed drop likely reflects fewer illness-page entry points from search, not a ranking collapse
- Could also reflect seasonality or shift in traffic to assessment/doctor pages

**ALGO_WATCH threshold:** Requires ≥2 /illnesses/* URLs with GSC-confirmed drops. Current state: confirmed-drops.json = `{}`. Only psychosis flagged from /illnesses/* (DataForSEO only, not GSC-validated), and today's DataForSEO shows it recovered to pos=9. Threshold NOT met.

## Likely root cause

**Core Update volatility (transient).** Psychosis query is historically noisy (multiple prior "HIGH → NOISE" resolutions in WATCH.md). The Jun 27–Jul 3 drop window overlaps directly with Core Update activation (Jun 30). DataForSEO position oscillated and recovered within 7 days. This is consistent with Core Update flux, not a structural content quality demotion.

The illness_page_viewed Mixpanel −27% is a secondary signal — worth monitoring but does not change the root cause assessment. It may resolve as Core Update volatility settles post-07-17.

## Recommended action

**DO NOT trigger ALGO_WATCH.** Conditions not met:
- confirmed-drops.json = {} (no GSC-validated drops)
- psychosis recovered to pos=9 by 07-10
- < 2 illness URLs with confirmed drops
- Addiction Treatment improving contradicts cluster-level hypothesis

**MONITOR through Core Update end (07-17).** If Strategist W29 data (next run) shows:
- 2+ illness URLs with GSC impressions declining WoW → trigger GSC deep pull
- illness_page_viewed continues below 118 for 2nd consecutive week → escalate as SOFT_SIGNAL

**No YMYL refresh holds needed.** Current YMYL queue (#18 batch) can proceed per Strategist's 07-02 ALGO_WATCH clearance — this investigation does NOT re-trigger the hold.

**Add psychosis to next DataForSEO monitoring pass** to confirm sustained recovery (not just 1-day spike back to pos=9).

## Watch

No new watch opened. Monitoring to be picked up by Strategist W29 (next run ~07-14). If fresh signal emerges → Strategist will create new BACKLOG row.

## Notes

- AP5 correctly applied: spike treated as noise until GSC validates
- AP9 not applicable (no YMYL refresh action recommended)
- ALGO_WATCH threshold documented for future reference: ≥2 /illnesses/* with GSC-confirmed drops + ≥2 consecutive weeks of illness_page_viewed decline
- June Core Update window closes 07-17 — Strategist W29 should explicitly note Core Update resolution in W29 trajectory review
