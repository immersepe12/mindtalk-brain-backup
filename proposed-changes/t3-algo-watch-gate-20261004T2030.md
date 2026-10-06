# Proposal: Add algo_watch gate to Task 3 before brief generation
**Proposed:** 2026-10-04T20:30:00+05:30
**Source:** task13-meta-learner-2026-10-04
**Apply on:** 2026-10-11T20:00:00+05:30
**Status:** preview

## Issue detected
Strategist run 2026-09-27 explicitly flagged: *"T3 SPEC CONCERN — P6 RISK: T3 created REFRESH-how-to-reduce-anxiety-immediately-brief.md on 09-25 while algo_watch=TRUE on that URL. T3's brief creation during an active algo_watch window may indicate a missing check in T3's gate logic — T13 candidate for next Meta-Learner cycle."*

Confirmed by inspecting `cowork-tasks/task3-serp-analysis-briefs.md` Step 2: it goes directly from receiving confirmed-drop URLs into SERP Analysis (Step 2a) with no check on `algo_watch` status in tracking-db. Principle P6 states: "NEVER override an algo_watch HOLD without evidence the update has settled." Creating a refresh brief during an algo_watch window is a P6 violation — it queues a content change that, if shipped, would confound an active observation and violate AP12.

Evidence: `brain/BRAIN.md` line ~1579 (Strategist 09-27 note), and `brain/BRAIN.md` BACKLOG entry for REFRESH-how-to-reduce-anxiety-immediately-brief.md showing `status: BRIEF_CREATED` with `algo_watch: true` on the parent URL.

## Proposed change
**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task3-serp-analysis-briefs.md`
**Edit type:** sed-replace

### Before
```
### Step 2 — For each confirmed drop URL (up to 20 total this week)

#### 2a. SERP Analysis
```

### After
```
### Step 2 — For each confirmed drop URL (up to 20 total this week)

#### 2a-PRE. algo_watch gate (run BEFORE Step 2a for every URL)
Before proceeding to SERP Analysis for any URL, check tracking-db.json:

```bash
cat ~/Seo-workflow-mindtalk/mindtalk-setup/tracking-db.json | python3 -c "
import json,sys
db=json.load(sys.stdin)
url='{url_path}'  # replace with current URL
entry=db.get(url,{})
print('algo_watch:', entry.get('algo_watch', False))
print('algo_watch_reason:', entry.get('algo_watch_reason',''))
print('algo_watch_until:', entry.get('algo_watch_until',''))
"
```

- If `algo_watch: true` → **SKIP this URL entirely**. Log: `ALGO_WATCH_HOLD: {url_path} — reason: {algo_watch_reason} — held until: {algo_watch_until}`. Do NOT proceed to 2a, 2b, 2c, or brief generation for this URL.
- If `algo_watch: false` or field absent → proceed to Step 2a normally.

This gate enforces Principle P6 ("NEVER override an algo_watch HOLD without evidence the update has settled") and prevents briefs that would violate AP12 (modifying a url_locked page during its open observation window).

#### 2a. SERP Analysis
```

## Rationale
P6 is a core safety principle preventing confounded experiments. If T3 creates a refresh brief for a URL under algo_watch, there is a downstream risk that T9 (Auto-Ship) or T11 (Executor) ships the brief before the algo_watch window closes — violating AP12 and destroying the experiment's signal. The fix is a one-line gate before the expensive SERP browser work (which saves unnecessary browser calls too). The Strategist explicitly requested this as a "T13 candidate" — this is the right cycle to fix it. Confirmed 1 violation instance (09-25).

## Risk assessment
Low risk. The gate only adds a SKIP for algo_watch=true URLs; all non-locked URLs continue through Step 2 unchanged. The only failure mode is a false positive (skipping a URL that has a stale algo_watch=true with an expired until date) — mitigated by logging the skip with the `algo_watch_until` date so Kushal can see which URLs were held and when they expire.

## Rollback
Copy `brain/before-snapshots/task3-serp-analysis-briefs.md-{TIMESTAMP}.bak` back to `cowork-tasks/task3-serp-analysis-briefs.md`.

## Veto instructions
To veto: rename this file from `t3-algo-watch-gate-20261004T2030.md` to `t3-algo-watch-gate-20261004T2030.vetoed.md` and add a `## Veto reason` section explaining why.

To approve early: rename to `t3-algo-watch-gate-20261004T2030.approved.md` — Strategist's next 8 PM run will apply it.
