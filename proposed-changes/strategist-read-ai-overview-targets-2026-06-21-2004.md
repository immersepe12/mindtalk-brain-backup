# Proposal: Strategist Step 2 reads AI Overview targets report

**Proposed:** 2026-06-21T20:04:41+05:30
**Source:** task13-meta-learner-2026-06-21
**Apply on:** 2026-06-28T20:04:41+05:30
**Status:** preview

## Issue detected

The workflow generates AI Overview opportunity data — `scripts/ai-overview-targets.py` writes `reports/ai-overview-targets-*.md` (latest present: `reports/ai-overview-targets-2026-05-18.md`). This is exactly the signal that feeds Active Hypothesis #2 in BRAIN.md ("AI Overview defense", Sprint B) and PRINCIPLE P2 ("AI Overview cannibalisation can't be fixed by SEO refresh alone").

But the Strategist spec's Step 2 input list (`cowork-tasks/task10-strategist.md:42-50`) does NOT reference this file. Strategist reads rank, gsc-validation, observation, weekly-summary, analyst-report, flagged/confirmed-drops, tracking-db — but never the AI Overview targets report. A signal the system pays to produce is never consumed by the decision-maker. This is the classic "missing signal" Meta-Learner category and matches the first-run note in `task13-meta-learner.md` (issue #3).

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task10-strategist.md`
**Edit type:** line-edit (Step 2 input list) — add one bullet after the analyst-report line (line 48)

### Before
```
- `reports/analyst-report-W{LATEST}-{DATE}.html` — if exists, latest analyst HTML
- `flagged-drops.json` + `confirmed-drops.json` — current queue states
```

### After
```
- `reports/analyst-report-W{LATEST}-{DATE}.html` — if exists, latest analyst HTML
- `reports/ai-overview-targets-{LATEST}.md` — if exists, pages losing impressions to AI Overview snippets (feeds Hypothesis #2 / PRINCIPLE P2). Use the newest file by date suffix; prefer AI-Overview-defense actions for pages on this list whose position improved while impressions fell ≥50%.
- `flagged-drops.json` + `confirmed-drops.json` — current queue states
```

## Rationale

Closes the loop between a signal the system already produces and the decision-maker that should act on it. P2 says AI Overview cannibalisation needs interactive content + India-specific stats + schema, not a plain refresh — Strategist can only queue that class of action if it reads which pages are affected. Wiring the report into Step 2 lets Strategist route AI-Overview-defense sprints to the right pages instead of treating impression loss as a generic drop.

## Risk assessment

Low. Adds a read-only input to Strategist; it does not change scoring math, caps, or any write path. Caveat: the latest report on disk is dated 2026-05-18 (stale). Reading a stale file is harmless, but if `ai-overview-targets.py` is no longer on a cron, the data will age — flagged separately as a follow-up to confirm the generator is scheduled (does NOT block this proposal, which only ensures the input is consumed when fresh). No production code touched.

## Rollback

Strategist snapshots to `brain/before-snapshots/task10-strategist.md-{TIMESTAMP}.bak` before applying. To revert: copy that snapshot back over `cowork-tasks/task10-strategist.md`.

## Veto instructions

To veto: rename this file to `strategist-read-ai-overview-targets-2026-06-21-2004.vetoed.md` and add a `## Veto reason` section.
To approve early: rename to `strategist-read-ai-overview-targets-2026-06-21-2004.approved.md`.
