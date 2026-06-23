# BRAIN — Mindtalk SEO Growth Engine

**Last updated:** 2026-06-23 (Strategist daily — **Sprint B/C 14d checks LANDED. Sprint A PENDING.** Sprint B: **P2 CONFIRMED** — all 3 AIO-defense pages reclaimed citation (W7 🟢 5× cited, impr 96→1,152; W8 🟢 3× cited, impr 64→549; W9 🟡 5× cited, impr partial). Sprint C: **DISCONFIRMED (bulk)** → P11 codified: style decides CTR — add number to list/steps titles WIN (+0.17–0.31pp CTR); remove existing number or swap to geo-commercial LOSE (-0.13–0.40pp). New playbook: **2-page staged P11 sample before any bulk**. **Sprint A W1-W6 still `pending_evaluation`** — check task due today, results not yet in WATCH.md (W7-W10 written, W1-W6 still `open`). Sprint A verdict gates the post-07-02 held-YMYL-refresh queue — highest urgency open item. Daily rank pull: **0 CRITICAL/MAJOR, 3 MODERATE all NOISE** (GSC: social-media-trap +31% impr IMPROVING; toxic-friends +83% impr NOISE; chronic-insomnia +63% impr NOISE). Sleep cluster from 06-22 = **NOISE CONFIRMED** (12 of 14 flags removed; all GSC impr flat-to-UP). **NEW confirmed drop:** /blogs/how-to-manage-ocd-thoughts — clicks −50%, impr −67.3%, GSC avgpos 16.1→21.8 — YMYL/mental-health → W17 added, ALGO_WATCH HELD. confirmed-drops `{}` (all 3 confirmed YMYL held). flagged-drops 22→8. **ALGO_WATCH ACTIVE** (May core update complete 06-02, clears ≈2026-07-02 — 9 days). Caps: NEW 4/20, refresh 0. **Step 10 NO-OP** (3 proposals `Apply on: 2026-06-28`, still 5 days future). **Posture: ACTION PHASE BEGINS** — Sprint B confirms AIO defense playbook; P11 unlocks targeted CTR v2; #8R fire-gate cleared; online-therapy hub draft done (Kushal path decision unblocks fire); held-refresh queue targets 07-02. No `⚠ STRATEGIST FLAG`.)
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
   - Status: Mixpanel-tracked; 7-day check pending (2026-06-19) — ✅ Mixpanel unified into 4011856 (2026-06-17) — Wed 06-24 T19 will provide first conversion read for W11

5. **Sleep/insomnia cluster coordinated weakness** (detected 2026-06-15) — ✅ **REFUTED 2026-06-16**
   - Hypothesis was: simultaneous sibling drops to *exactly* position 100 = technical deindex.
   - Result: GSC 06-16 re-pull found all 3 siblings indexed, positions *improved* WoW, signal=NOISE. CBT-i had its best week of the series inside the alleged-drop window. Root cause: DataForSEO single-keyword tracker "100" is a "not-in-top-100-this-pull" sentinel, **not** a Google index signal. No content action taken. Log: `memory/experiments/investigation-sleep-cluster-2026-06-16.md`.
   - **Carry-forward learning:** the *same* exact-100 pattern recurred 06-16 (10 URLs). The data-quality gate now auto-quarantines ≥4 uniform pos-100 drops. W16 reconciles them against the 06-18 pull. Treat exact-100 as DataForSEO noise by default (AP5).
   - **W16 CLOSED 2026-06-18 — noise confirmed a 3rd time.** The 06-16 ten recovered (none in the 06-18 pos-100 set) and the 06-18 pull produced a *different* 15-URL pos-100 set. The exact-100 set rotates run-to-run → conclusively a DataForSEO API/parsing artefact, not deindex. The auto-quarantine gate works as designed; keep treating exact-100 as noise and only escalate if the *same* URLs report 100 across two consecutive pulls.

6. **Conversion layer reframes growth strategy** (T19 inaugural 2026-06-17, Mixpanel 4011856)
   - Signal: the strongest converters are /doctors (🟢 Goldmine, 321% intent), /experts/expert-therapists (62%), and /doctors/telugu- & tamil-speaking-doctors (🟡 Rockets, 91-95%). High-traffic discovery blogs (dry-begging, hamilton-anxiety-scale, dominant-personality, etc.) convert **~0 booking intent**. Geo: Bengaluru = 65% of all booking intent; Mumbai/Chennai/Delhi = high-intent low-volume (expansion); Hyderabad/Telangana = leak (11% intent).
   - Hypothesis: the autonomous loop has been optimizing a **vanity axis** (clicks on blogs) while the real booking engine (doctor/expert pages) sits mostly outside the SEO tracked set (config tracks illnesses/treatments/blogs + doctors-LISTINGS, but the converting pages are /doctors, /experts/, /doctors/{lang}-speaking-doctors). The highest-leverage SEO move is to route blog link-equity into doctor Goldmines and to build language/metro doctor pages — NOT to keep harvesting CTR on discovery blogs.
   - Status: LIMITED_BASELINE (week 1 of data). Patterns need ≥3 weeks before T5 fires (D9). Acting cautiously: draft internal-link reorientation sprint now (BACKLOG #8, draft-only/staged), defer new doctor-page content (D9) until pattern confirmed. P9 scoring modifiers now active.
   - ~~Open dependency: cross-domain revenue validation BLOCKED (consult project 3986277 absent)~~ — **✅ RESOLVED 2026-06-17**: project 3986277 deprecated; all data (marketing + consult web app + Mindtalk app) unified into project 4011856. UTM attribution shipped both codebases (mindtalk.in PR #6 sends `utm_source=mindtalk_web` + page-type/slug/CTA-position; consult.cadabams.com captures + stamps onto every Mixpanel event). 14h post-deploy verification (2026-06-18 03:00 IST): 65 Referral Captured, 56 Doctor Booking Page Viewed with utm_source=mindtalk_web, 1 Payment Successful tagged mindtalk_web. T19 spec updated 2026-06-17 to use Revenue > Engagement > Intent precedence + new 🔵 Engagement Engine tier + UX friction detection. **Next T19 run 2026-06-24 (Wed 11:06 IST) = first revenue-truth conversion classification.**

### Open structural gaps

- ~290 inventory items missing SEO pages (verified 2026-06-22 by file system audit; "185" was a conservative curation guess that's been carried forward). Live: 21 assessments / 9 journeys / 18 worksheets / 5 mindful-minutes / 5 journals. App inventory: 99 assessments + 18 journeys + ~50 worksheets + 155+ audios + 26 journals. **Pilot 20 plan drafted 2026-06-22** at `dev-specs/2026-06-22-stub-page-pilot-20.md` (5/type × 4-week batched rollout, existing 5-reviewer pool, earliest fire 06-30). Validates the playbook before committing to remaining ~270.
- Refresh briefs in algo_watch HOLD until Core Update settles (~7-14 days)
- 2 recovery-followup briefs need strategic angle decision (ERP + life-coach round-2)

### Operational notes (2026-06-15)

- **Auto-Ship push path — ✅ RESOLVED 2026-06-17.** The 3 inaugural NEW blogs shipped via `549dac3` (Task 9 manual completion); 32/32 NEW briefs now live, 254 blogs total. The Vercel attribution block (`user.email` mismatch → Venkat-P7) was fixed 06-16 (`89e293a`); the deploy pipeline is unblocked for T9/T11/T16. Auto-ship 06-17 ran clean ("nothing to ship — all shipped"). Indexation watches W12-W14 opened.
- **May 2026 core update is receding:** /treatments/psychotherapy impressions rebounded +109% (89→186) on 06-15 GSC and dropped off the flagged queue as noise. This is the first concrete "update settling" signal. Hold YMYL refreshes one more cycle; plan to **resume the held refresh queue after ~06-23** if the trend holds. Don't refresh mid-rebound (muddies attribution).
- **Monitoring gap (2026-06-19) — Jun-9 NEW_CONTENT cohort silently un-monitored.** Obs-monitor flagged that 6 NEW pages (anger-management-therapy, codependency-signs-causes-treatment, dbt-skills-modules, people-pleasing-how-to-stop, relationship-problems-signs-causes-solutions, what-is-somatic-therapy) carry `status=PUBLISHED` but have **no `url_locked` flag**, so the Step-1 filter (requires `url_locked==true`) skips them — their day-21 midpoint (~06-30) will be silently missed. This is the *missing-flag* sibling of the 06-16 *status-dimension* filter fix. Tracking-db edits are outside Strategist write scope → escalated to Kushal as BACKLOG #13 (set `url_locked=true` before 06-30). Recurrence of this class → Meta-Learner should propose hardening the Obs-monitor filter to lock-on-publish.
- **pos-100 noise — now confirmed 5×.** The DataForSEO exact-position-100 quarantine set rotates run-to-run (06-16 → 06-18 → 06-19 → 06-22 sets share zero URLs pairwise). Established rule (AP5/P5/AP8): treat exact-100 as API/parsing noise by default; only escalate to a deindex investigation if the *same* ≥4 URLs report 100 across two consecutive pulls. The auto-quarantine gate is working as designed. 06-22 added a clean cross-check: sleep-disorder-tests was reported at "pos 100" by the tracker while GSC showed it +32% impr the same week — the two sources disagree, confirming the tracker value is the artefact.
- **Broad cluster GSC slide (2026-06-22 weekly report) — under read-only investigation, NOT refresh.** The Monday weekly report flagged 12 cluster avg-position drops (5 sleep: circadian-rhythm −16.7, delayed-sleep-phase −11.3, sleep-talking −7.8, sleep-disorder listing −6.6 @474 impr, ocd-thoughts −14.7; plus top-10-stressors, migraine-stress, positive-psychology, anger-in-relationship, save-marriage, conduct-disorder, drug-addiction). This is the *broader* successor to the 06-16 sleep-cluster signal (which resolved as NOISE). It's GSC avg-position-sourced (more reliable than the DataForSEO tracker) but **all flags are `gsc_validation: PENDING`** → Task 2 adjudicates Tue 06-23. Hypothesis: partly composition (the "what is a life coach" 9,429-impr page-2 surge mechanically dragged site avg position 10.1→11.3), partly possible cannibalization across overlapping sleep blogs. Response (BACKLOG #14): read-only cannibalization/internal-link diagnostic, gated post-validation; **no refresh** — YMYL/health under ALGO_WATCH (P7), /illnesses/sleep-disorder + DBT in the pro-input skip-list, and don't perturb pre-06-23 Sprint attribution. Treat as validate-first; do not assume a real penalty cascade (AP5).
- **Real blog schema (confirmed by T9 against 251 live files):** quickAnswer + keyTakeaways + faqs live in **frontmatter** (not `<QuickAnswer>`/`<KeyTakeaways>` body components as some specs/briefs show); semantic `category` (e.g. relationship-issues/ocd/general) + `reviewer:` slug; FAQs render as FAQPage JSON-LD; body is plain GFM. Verifier quality-bar checks should match the frontmatter schema, not body components.

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
