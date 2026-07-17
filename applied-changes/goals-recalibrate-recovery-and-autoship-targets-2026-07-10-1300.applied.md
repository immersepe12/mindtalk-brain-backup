# Proposal: Recalibrate refresh-recovery + auto-ship success targets against 4 weeks of evidence
**Proposed:** 2026-07-10T13:00:00+05:30
**Source:** Kushal-directed workflow-hardening session (Cowork, 2026-07-10) — not a Meta-Learner run, but filed through the standard 7-day preview so Kushal can veto/amend
**Apply on:** 2026-07-17T20:00:00+05:30 (Strategist Step 10 apply-pass)
**Status:** preview

## Issue detected

Two GOALS.md targets are miscalibrated against the system's own accumulated evidence:

1. **"14-day recovery rate on refresh sprints: >70%" (Q3) and "Refresh recovery rate (14-day) ≥70%" (adaptive learning table).** Actual measured: Sprint A 1/6 = 17% (Learner close 2026-06-28); monthly rollup June = 17%. AP9 codified WHY: reviewer-signal-only refreshes cannot recover top-20 YMYL pages — content depth is required. A single blended 70% target ignores the confirmed page-depth split and permanently reads as "failing," which distorts Strategist axis-weighting.

2. **"Auto-ship success rate ≥85% of NEW briefs auto-ship cleanly."** T9's Verifier veto rate is structurally high BY DESIGN (word-count, cluster caps, YMYL gates) — e.g. week 06-22: 4/4 vetoed; 07-08: 1/2 vetoed on §5 wc + cluster cap. An 85% clean-ship target punishes the safety layer for working. The §5-pre-check at brief-gen (added 07-03) is the correct fix; the target should measure briefs that PASS pre-check.

## Proposed change
**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/brain/GOALS.md`
**Edit type:** line-edit (2 locations)

### Before
```
- 14-day recovery rate on refresh sprints: **>70%**
```
### After
```
- 14-day recovery rate on refresh sprints: **>60% for deep pages (pos >25, signal-fix playbook) / >40% for top-20 YMYL pages (depth+reviewer playbook, 42-day window)** — split per AP9/P12 evidence 2026-06-28
```

### Before
```
| Auto-ship success rate | ≥85% | NEW briefs cleanly convert to live pages |
```
### After
```
| Auto-ship success rate | ≥85% of briefs that pass §5 pre-check | Measures pipeline quality, not Verifier strictness. Verifier veto rate tracked separately; a veto of a §5-passing brief = pipeline defect, a veto of a §5-failing brief = T3/T5 defect. |
```

## Rationale
Targets should be falsifiable and fair. The system has 4 data points (W1-W6 closes + 3 weeks of T9 veto logs) showing these two numbers measure the wrong thing. Keeping them as-is trains the Strategist to chase impossible axes.

## Risk assessment
Low. Text-only KPI definition change; no behavior change to any gate or cap. Worst case: the split targets prove too lenient — Learner can propose tightening with new evidence.

## Rollback
Copy `brain/before-snapshots/GOALS.md-2026-07-17.bak` back.
