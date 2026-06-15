# BRAIN — Mindtalk SEO Growth Engine

**Last updated:** 2026-06-15 (autonomous loop initialized)
**Read by:** Strategist (Task 10), Executor (Task 11), Learner (Task 12)
**Written by:** Strategist + Learner (in their respective scheduled runs)

This is the **living state** of the autonomous SEO growth engine for mindtalk.in.
Every scheduled task that affects the site reads this file before acting and writes back what it learned.

---

## Operating principle

Grow `mindtalk.in` autonomously by:
1. **Aligning** with GOALS.md (Strategist reads this first)
2. **Detecting** site signals (rank, GSC, observation, weekly reports)
3. **Deciding** the highest-impact next action toward the weakest goal axis
4. **Executing** safely with hard caps (Executor + Auto-Ship)
5. **Observing** outcomes through scheduled watch windows
6. **Learning** patterns and updating strategy (Learner)
7. **Tracking** progress in TRAJECTORY.md weekly
8. **Self-improving** the workflow itself (Meta-Learner)
9. **Looping** without manual intervention except for YMYL clinical sign-off

The goal hierarchy:
```
GOALS.md (north star + quarterly milestones)
  ↓
Strategist reads + identifies WEAKEST axis
  ↓
BACKLOG.md (next 3-5 actions targeting that axis)
  ↓
Executor + Auto-Ship + Meta-Learner act
  ↓
WATCH.md (observe outcomes)
  ↓
Learner evaluates → TRAJECTORY.md updated weekly
  ↓
Strategist reads TRAJECTORY next morning → adjusts BACKLOG
```

---

## Current strategic state

### Site posture
- **Phase:** Growth + Recovery (post May 2026 Core Update remediation)
- **Pages live:** 691 (sitemap: 661)
- **Brief queue cap:** 20 NEW + 20 REFRESH per week
- **Auto-ship cap:** 5 NEW blogs per run (3 first-run), 20 per week
- **Tracking-db:** 51 BRIEF_CREATED, 11 PUBLISHED, 8 observation states

### Active hypotheses (under test)

1. **YMYL reviewer + JSON-LD `reviewedBy` fix** (shipped 2026-06-09, commit `270cf0c`)
   - Expected: 15-25% impression recovery on dementia/alzheimers/PTSD/drug-addiction clusters by 2026-06-23
   - Status: 14-day watch open
   - Scheduled check: `mindtalk-ymyl-reviewer-sprint-14d-check` fires 2026-06-23 9:00 IST

2. **AI Overview defense** (Sprint B shipped 2026-06-09, commits `aa5e3b9`, `5dfe080`, `c1e0d67`)
   - Expected: 30-50% impression recovery on dominant-personality / 20-quotes / emotional-distress
   - Status: 14-day watch open
   - Scheduled check: needs Task 10 to add to watch list

3. **CTR meta-rewrite top 20** (Sprint C shipped 2026-06-09, commit `7c3c2c4`)
   - Expected: +2,180 clicks/wk from CTR uplift on existing impressions
   - Status: needs 14-day watch
   - Scheduled check: needs Task 10 to add to watch list

4. **Homepage app-first redesign** (shipped 2026-06-12, merge `c35193f`)
   - Expected: app CTA click-through becomes #1 hero conversion path
   - Status: Mixpanel-tracked; 7-day check pending

### Open structural gaps

- 185 inventory items (assessments + journeys + worksheets) have no dedicated SEO page (16% → 95% coverage opportunity)
- Refresh briefs in algo_watch HOLD until Core Update settles (~7-14 days)
- 2 recovery-followup briefs need strategic angle decision (ERP + life-coach round-2)

### Anti-patterns to avoid (hard rules)

These are non-negotiable. Strategist must NEVER queue an action that violates these:

- ❌ Auto-ship YMYL pages (illness/treatment) — always needs clinical sign-off
- ❌ Bulk-rewrite ranking content without 14-day safety pause after major refresh
- ❌ Ship more than 20 NEW + 20 REFRESH briefs per week (config cap)
- ❌ Modify content on a page within 14 days of its last refresh (let it settle)
- ❌ Auto-ship anything tagged `algo_watch HOLD` or `do not publish`
- ❌ Override reviewer assignment from a pre-vetted brief
- ❌ Touch /assessments/suicide-safety until `ENABLE_SUICIDE_SAFETY=true`
- ❌ Push to main without `npm run build` verifying clean
- ❌ Take any action without Slack notification to `#seo-workflow-mindtalk`

---

## Decision-making framework (used by Strategist)

When deciding "what should we do today?", score candidate actions by:

1. **Impact** — projected clicks/week or impressions/week recovered
2. **Confidence** — based on past similar actions (read MEMORY/patterns/)
3. **Effort** — Claude Code time + DataForSEO cost
4. **Risk** — could it harm a ranking page?
5. **Time-to-validate** — when will we know if it worked?

Score = `(Impact × Confidence) ÷ (Effort × Risk)`, prefer faster time-to-validate.

Top-3 actions go into BACKLOG.md ranked. Executor picks from top.

---

## Action categories the engine can take

| Category | Auto-fired? | Constraints |
|---|---|---|
| Auto-ship NEW blog | ✅ Yes (Task 9) | ≤5/run, ≤20/week, safety filters |
| Ship REFRESH brief | ⚠ With caveats | Only if NOT algo_watch HOLD AND page last touched >14 days ago |
| Draft new SPRINT prompt | ✅ Strategist drafts | Executor fires after 24h preview window |
| Investigate cluster regression | ✅ Yes | Spawns diagnostic worker |
| Schedule recovery check | ✅ Yes | Auto-creates Cowork one-off task |
| Edit code (components, lib, etc.) | ❌ Manual only | Too high-risk to autonomously modify code |
| Modify config | ❌ Manual only | Strategy parameters need human review |
| Touch YMYL pages | ❌ Manual only | Clinical sign-off required |

---

## Slack reporting cadence

- **Daily 8:30 PM IST** — Strategist summary: today's signals + tomorrow's plan
- **Per-execution** — Executor / Auto-ship per-run notifications
- **Sunday 6:30 PM IST** — Learner weekly digest: what we did, what worked, what's next

If Kushal ever wants to PAUSE the loop: disable any of `mindtalk-strategist`, `mindtalk-executor`, `mindtalk-auto-ship-new-blogs` in Cowork sidebar. The crons can be re-enabled at any time without code changes.

---

## Self-modification capability (added 2026-06-15)

The loop can now modify ITSELF — task specs, configs, cron prompts — not just content.

| Role | Can modify | Safety gate |
|---|---|---|
| **Meta-Learner (T13)** Sun 8 PM | brain/*.md, cowork-tasks/*.md, config.json, Cowork SKILL.md prompts | Proposes only — 7-day preview |
| **Strategist (T10)** daily 8 PM Step 10 | Applies proposals after preview | Snapshot to `brain/before-snapshots/` first |
| **NEVER auto-modified** | scripts/*.py, src/**, GitHub repo code | Always `human-review-only` flag |

Proposal lifecycle: Meta-Learner detects issue → writes proposal to `brain/proposed-changes/{id}.md` → Slack post with diff → 7 days pass → Strategist applies (or skips if `.vetoed.md` exists) → moves to `brain/applied-changes/`.

## See also

- `GOALS.md` — north star + quarterly milestones + risk caps + anti-goals (Kushal-owned, Strategist reads)
- `TRAJECTORY.md` — weekly progress vs GOALS, updated by Learner Sunday 6 PM
- `BACKLOG.md` — what's queued (top 3-5 actions for next 72h)
- `WATCH.md` — active observations with check dates
- `PRINCIPLES.md` — distilled lessons from past actions (3+ evidence rule)
- `ANTI-PATTERNS.md` — what NOT to do (mistakes the loop has learned)
- `proposed-changes/` — Meta-Learner system-improvement proposals awaiting 7-day preview
- `applied-changes/` — historical log of applied system-improvements
- `before-snapshots/` — backups taken before any auto-apply (rollback safety)
- `memory/experiments/` — per-experiment outcomes
- `memory/patterns/` — recurring patterns we've observed
- `memory/decisions/` — Strategist decision log with reasoning
- `memory/applied-history.md` — audit trail of every auto-applied change
