# Proposal: T11 investigate_regression — add MDX file existence pre-check before running diagnostic
**Proposed:** 2026-08-09T20:30:00+05:30
**Source:** task13-meta-learner-2026-08-09
**Apply on:** 2026-08-16T20:00:00+05:30
**Status:** preview

## Issue detected

**Category 1b: Wasted work — full diagnostic run on non-existent page**

Incident: **STRESS-COPE-01**, 2026-07-24 (BRAIN.md stamp, pm-T11):

> *"STRESS-COPE-01 CLOSED as FALSE SIGNAL — MDX file `10-ways-to-cope-with-stress-proven-methods-that-work.mdx` does NOT exist in repo; the Strategist's URL was inferred ('likely'), not confirmed. Cannot refresh a non-existent page. Lesson: investigate_regression entries must confirm the MDX file exists before queuing."*

T11 Step 4c (`investigate_regression`) currently begins by identifying the target, then immediately runs a full diagnostic suite:
- `decline-diagnostic.py`
- Read `gsc-data/{slug}.json`
- Read `reports/cluster-history.json`
- Read recent git log

All of this work is wasted if the MDX file doesn't exist in the repo. In the STRESS-COPE-01 case, the Strategist (T10) inferred a "likely" URL from GSC data that had no corresponding MDX. T11 ran the full diagnostic before discovering the file was absent.

The fix is a single filesystem check added as step 0 in T11 Step 4c, before any diagnostic work begins.

## Proposed change

**File to edit:** `cowork-tasks/task11-executor.md`
**Edit type:** line-edit

### Before
```
#### 4c. `investigate_regression`

1. Identify target from BACKLOG row (cluster slug, URL, or query)
2. Run focused diagnostic:
   - `python3 scripts/decline-diagnostic.py --target {target}` if applicable
   - Read `gsc-data/{slug}.json` for query-level breakdown
   - Read `reports/cluster-history.json` for trend
   - Read recent git log for that page/file
3. Write findings to `brain/memory/experiments/investigation-{target}-{TODAY}.md`:
   - What's the actual signal? (rank drop, impression drop, CTR drop, deindex)
   - What's the likely root cause? (algo, technical, content, SERP feature)
   - What's the recommended action? (refresh, structural change, hold, investigate further)
4. Update BACKLOG: replace the `investigate` row with the recommended action row
5. Slack notification with summary + link to full investigation log
```

### After
```
#### 4c. `investigate_regression`

0. **MDX file existence pre-check (added 2026-08-16 — STRESS-COPE-01 lesson)**

   Before running any diagnostic, confirm the target MDX file exists in the repo:
   ```bash
   # Derive slug from BACKLOG row URL (e.g. /blogs/some-slug → some-slug)
   slug={slug-from-backlog}
   # Check all 3 possible content dirs
   found=""
   for dir in blogs treatments illnesses; do
     f="/Users/agent/Documents/GitHub/mindtalk/src/content/${dir}/${slug}.mdx"
     [ -f "$f" ] && found="$f" && break
   done
   echo "${found:-NOT_FOUND}"
   ```
   - **If NOT_FOUND:** close the BACKLOG row as `FALSE_SIGNAL` with note: "MDX file does not exist in repo — URL was inferred, not confirmed. Cannot investigate a non-existent page." Post Slack flag. STOP — do not proceed to step 1.
   - **If found:** note the confirmed path, proceed to step 1.

1. Identify target from BACKLOG row (cluster slug, URL, or query)
2. Run focused diagnostic:
   - `python3 scripts/decline-diagnostic.py --target {target}` if applicable
   - Read `gsc-data/{slug}.json` for query-level breakdown
   - Read `reports/cluster-history.json` for trend
   - Read recent git log for that page/file
3. Write findings to `brain/memory/experiments/investigation-{target}-{TODAY}.md`:
   - What's the actual signal? (rank drop, impression drop, CTR drop, deindex)
   - What's the likely root cause? (algo, technical, content, SERP feature)
   - What's the recommended action? (refresh, structural change, hold, investigate further)
4. Update BACKLOG: replace the `investigate` row with the recommended action row
5. Slack notification with summary + link to full investigation log
```

## Rationale

One FALSE_SIGNAL incident (STRESS-COPE-01) consumed a full T11 action slot on a file that doesn't exist. The pre-check adds ~5 seconds of bash execution and zero tokens of real diagnostic work if the file is absent. If the file IS present, the check adds negligible overhead. This is a pure win: a 2-line bash check saves the entire T11 action budget when the BACKLOG entry is wrong.

## Risk assessment

Low. The pre-check is read-only (filesystem stat). It can only produce false negatives (file exists but check fails to find it), which is self-correcting — Slack flag notifies, human can re-queue. No production code or site changes involved.

## Rollback

Snapshot: the exact "Before" block above is the pre-change text. Revert by re-applying Before→After in reverse.
