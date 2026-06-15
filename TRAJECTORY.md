# TRAJECTORY — Weekly Progress vs GOALS.md

**Read by:** Strategist (T10) every day, Learner (T12) Sunday before weekly digest.
**Written by:** Learner only — Sunday 6 PM weekly run.
**Purpose:** Single rolling view of how the system is performing relative to its targets.

---

## Headline metrics — weekly

| Week | Clicks | Δ | Impr | Δ | CTR | Pos | Pages | Inv % | YTD path to 12mo goal |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|
| 2026-06-08 to 06-14 | 1,785 | -13.2% | 289K | -32% | 0.6% | 13.6 | 691 | 27% | Baseline |
| 2026-06-15 to 06-21 | TBD | — | — | — | — | — | — | — | — |

(Learner fills new row every Sunday)

---

## Production velocity — weekly

| Week | NEW shipped | Refresh shipped | YMYL refresh | Sprints fired | Stubs | Investigations | Total |
|---|---:|---:|---:|---:|---:|---:|---:|
| 2026-06-08 to 06-14 | 6 (manual sprint) | 3 | 0 | 4 (A, B×3, C) | 0 | 1 | 14 |
| 2026-06-15 to 06-21 | TBD | TBD | TBD | TBD | TBD | TBD | TBD |

---

## Quality KPI tracking

| KPI | Last week | 4-week avg | Q3 target | Status |
|---|---:|---:|---:|---|
| Avg CTR | 0.6% | 0.55% | 0.85% | 🔴 below |
| Avg position | 13.6 | 14.1 | (no specific target) | 🟡 holding |
| % pages with reviewer | 100% (YMYL) | 100% | 100% | 🟢 met |
| % pages with Quick Answer | ~35% | — | 100% (Q4) | 🟠 in progress |
| % pages with FAQ schema | ~40% | — | 100% (Q4) | 🟠 in progress |
| Top-3 ranking queries | 5,706 | — | 7,500 (Q3) | 🟡 baseline |
| Pages live | 691 | — | 800 (Q3) | 🟡 baseline |
| Inventory coverage | 27% | 27% | 45% (Q3) | 🟡 baseline |

---

## Adaptive learning — monthly rollup

| Month | Principles added | Anti-patterns added | Watches opened | Watches closed | Recovery rate | Notes |
|---|---:|---:|---:|---:|---:|---|
| 2026-06 (in progress) | 7 | 7 | 11 | 0 | TBD | Loop initialized; first watches close 2026-06-23 |

---

## Action distribution — last 4 weeks

| Action class | Count | Avg outcome | Confidence going forward |
|---|---:|---|---|
| YMYL reviewer fix | 55 pages (Sprint A) | Pending 14d check | High (logged P1) |
| AI Overview defense | 3 pages (Sprint B) | Pending 14d check | Medium (novel) |
| CTR meta-rewrite | 20 pages (Sprint C) | Pending 14d check | High (logged P4) |
| Homepage redesign | 1 page | 7d check pending | High (logged P9 future) |
| NEW blog ships | 6 pages | Indexation in progress | High |
| Refresh ships | 3 pages | 14d watches open | Medium |
| Manual investigations | 1 (Reduce Stress cluster) | False positive identified | High (logged AP5) |

---

## Risk caps — current usage

| Cap | This week usage | Limit | Status |
|---|---|---|---|
| NEW blogs auto-shipped | 6 | 20 | 30% — healthy headroom |
| Refresh auto-shipped | 3 | 10 | 30% — healthy headroom |
| % pages refreshed (rolling 30d) | ~5% | 20% | 25% of cap — fine |
| % pages auto-modified (rolling 7d) | ~1% | 5% | 20% of cap — fine |
| Build failures | 0 | 0 | 🟢 |
| Watches simultaneously open | 11 | 50 | 22% of cap — fine |

---

## Variance flags (where actual diverges materially from target)

| Metric | Target | Actual | Variance | Recommended action |
|---|---|---|---|---|
| Weekly clicks | 2,800 (Q3) | 1,785 | -36% | Need 5 weeks of consistent growth — bottleneck is shipping velocity. Auto-ship pipeline goes live this week, should close gap. |
| Avg CTR | 0.85% (Q3) | 0.6% | -29% | Sprint C (CTR meta-rewrite) shipped 2026-06-09 — 14d check 2026-06-23 will tell if playbook is working at scale |
| Inventory coverage | 45% (Q3) | 27% | -18pp | Need stub-page sprint (185-page gap). Drafted prompt pending Kushal approval. |

---

## Trajectory verdict (Learner's weekly write-up)

**Most recent week (Learner fills weekly):**

> System initialised this week. Architecture complete: 5 autonomous agents + brain memory + 7-day self-modification preview window. Inaugural Auto-Ship run fires 2026-06-15 15:15 IST shipping 3 NEW blogs. Sprints A/B/C shipped 2026-06-09 with 14d checks on 2026-06-23 — those results will be the first real signal of whether the recovery playbook works. Until then, system is in observation mode with seeded BACKLOG. Quality bars are met for all YMYL pages. Production velocity will scale once Task 9 + Task 11 stabilise their patterns.

---

## How TRAJECTORY.md gets updated

Every Sunday 6 PM, Learner:

1. Reads `reports/weekly-summary-{YESTERDAY}.txt` for headline metrics
2. Reads `logs/auto-ship-*.txt` and Executor logs from the past week
3. Counts watches opened/closed/recovered from `brain/WATCH.md` + closed experiments
4. Computes 4-week rolling averages
5. Compares actual vs Q3 targets in GOALS.md
6. Adds row to "Headline metrics — weekly" table
7. Adds row to "Production velocity — weekly" table
8. Updates "Quality KPI tracking" status emojis
9. Recomputes "Variance flags" — if any metric is >30% off target, propose adjustment
10. Writes "Most recent week" verdict in 2-3 sentences
11. Includes TRAJECTORY snapshot in Sunday Slack digest

Strategist reads this every day before deciding actions — knows where the gaps are.
