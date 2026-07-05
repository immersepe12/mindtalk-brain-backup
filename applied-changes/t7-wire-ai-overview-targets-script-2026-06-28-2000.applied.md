# Proposal: Add ai-overview-targets.py to T7 monthly site audit

**Proposed:** 2026-06-28T20:00:00+05:30
**Source:** task13-meta-learner-2026-06-28
**Apply on:** 2026-07-05T20:00:00+05:30
**Status:** preview

## Issue detected

`scripts/ai-overview-targets.py` generates `reports/ai-overview-targets-{DATE}.md` — the signal file that feeds Sprint B (AI Overview defense), PRINCIPLE P2, and P10. The pending proposal `strategist-read-ai-overview-targets-2026-06-21-2004.md` (applying today, 2026-06-28) wires this report into Strategist's Step 2 input list. But that proposal noted: *"Caveat: the latest report on disk is dated 2026-05-18 (stale). Reading a stale file is harmless, but if `ai-overview-targets.py` is no longer on a cron, the data will age."*

The file **has not been updated since 2026-05-18** — 41 days ago at time of writing. No scheduled task in cowork-tasks/ (T1–T13) calls `ai-overview-targets.py`. It has been run ad-hoc only. Once Strategist starts reading this file (post today's apply), it will be consuming 6-week-old AI Overview cannibalisation signals with no automated refresh path.

Evidence:
- `reports/ai-overview-targets-2026-05-18.md` — most recent file, 41 days old
- Grep of all cowork-tasks/*.md for "ai-overview-targets": zero matches (no scheduled task calls it)
- T6 (weekly), T7 (monthly site audit), T8 (analyst HTML) all run scripts but none reference this one

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task7-site-audit.md`
**Edit type:** append — add a new step after the existing site-audit steps, before the Slack post step

The exact insertion point depends on T7's current step count (read T7 to find the final numbered step before Slack). Add after the last data-gathering step:

### Before (end of data-gathering section, before Slack/output step)

Find the last line of T7's data steps that ends with a script call or file read, then insert after it:

```
(end of existing T7 steps)
```

### After (new step added)

```
### Step N — Regenerate AI Overview targets report

Run the AI Overview cannibalisation detector to refresh which pages are losing impressions to AIO snippets:

```bash
cd /Users/agent/Seo-workflow-mindtalk/mindtalk-setup
python3 scripts/ai-overview-targets.py 2>/dev/null
```

If the script runs successfully, a new `reports/ai-overview-targets-{TODAY}.md` file will appear.
If it fails (API error, credentials missing), log the error and continue — do not abort the site audit.

This step ensures Strategist's Step 2 always reads a ≤30-day-old AI Overview signal when scoring AI-defense sprint candidates.
```

(Replace "Step N" with the correct sequential step number in T7's spec.)

## Rationale

Closes the production gap between "Strategist reads the report" (pending proposal applying today) and "the report is fresh". A 6-week-old AI Overview signal is not actionable — Sprint B target pages could have fully recovered or new pages could now be cannibalised. Monthly refresh in T7 aligns with the audit cadence (first Monday of the month) and keeps the signal ≤30 days old. The script run is cheap (DataForSEO SERP-advanced calls on the top ~20 at-risk URLs) and fits naturally in the monthly audit alongside the other SERP analysis steps.

## Risk assessment

Low. The script write is a new report file under `reports/`; it does not modify any existing file. If the script fails (auth or API issue), the site audit continues normally. The only risk is if the script has undocumented side effects — review T7 output after first run to confirm no unexpected writes outside `reports/`.

## Rollback

If the step causes T7 to fail or produces bad data: remove the added step from `cowork-tasks/task7-site-audit.md` (revert from `brain/before-snapshots/task7-site-audit.md-{TIMESTAMP}.bak`). The stale `reports/ai-overview-targets-2026-05-18.md` remains as the fallback Strategist reads.

## Veto instructions

To veto: rename this file to `t7-wire-ai-overview-targets-script-2026-06-28-2000.vetoed.md` and add a `## Veto reason` section.
To approve early: rename to `t7-wire-ai-overview-targets-script-2026-06-28-2000.approved.md`.
