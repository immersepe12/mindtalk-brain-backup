# Proposal: T6 Step 2.5 — Dead-URL prefix guard before category bucketing
**Proposed:** 2026-07-26T20:30:00+05:30
**Source:** task13-meta-learner-2026-07-26
**Apply on:** 2026-08-02T20:00:00+05:30
**Status:** preview

## Issue detected

**Log evidence:**
1. `brain/BACKLOG.md` entry "DOCTORS-LISTING-DROP-02" (closed 2026-07-20): T6 weekly-report (2026-07-13) reported "Doctors-Listings category dropped −44.9% WoW". This figure was fabricated. Root cause: 12 doctor pages were keyed in `keyword-map.json` and `rank-history.json` under the dead URL prefix `/doctors-listings/{slug}` (these 404 on production) instead of the correct live prefix `/doctors/{slug}`. `rank-history.json` showed these 12 pages pinned at `position: 100` (not-ranking sentinel) for weeks. T6's `cluster-report.py` bucketed these phantom "position 100" signals into the "Doctors-Listings" category, generating the false −44.9% WoW figure.
2. The BACKLOG entry explicitly states: "task6-weekly-report.md Step 4 has no defined methodology" — meaning T6 has no verification step to catch dead URL prefixes before they pollute category totals.
3. This false signal consumed **4 consecutive days** of BACKLOG priority cycles (07-17→07-20) on a full T11 investigation before being confirmed as a tracking data artifact. This is a measurable wasted-work pattern.
4. A one-time data fix was applied 2026-07-20 (renaming 12 dead URL keys). But T6's spec still has no guard — the same error will recur if any future rank-tracking step introduces a URL under a dead prefix.

**Known dead URL prefixes:**
- `/doctors-listings/` — all these 404 in production; the live URLs are `/doctors/` (routing handled by `src/app/doctors/[slug]/page.tsx`). Confirmed via direct `curl` on 2026-07-20.

## Proposed change
**File to edit:** `cowork-tasks/task6-weekly-report.md`
**Edit type:** line-edit (insert new Step 2.5 between Step 2 and Step 3)

### Before
```
### Step 3 — Read both reports
```

### After
```
### Step 2.5 — Dead-URL prefix guard (added 2026-07-26)

Before reading the cluster report output, run a dead-URL prefix check on `keyword-map.json`:

```bash
cd ~/Seo-workflow-mindtalk/mindtalk-setup

# Check for any tracked URLs under known-dead prefixes
python3 -c "
import json
dead_prefixes = ['/doctors-listings/']
km = json.load(open('keyword-map.json'))
dead_entries = [url for url in km if any(url.startswith(p) for p in dead_prefixes)]
if dead_entries:
    print('DEAD_URL_ENTRIES_FOUND:', len(dead_entries))
    for url in dead_entries[:10]:
        print(' -', url)
else:
    print('OK — no dead-prefix entries')
"
```

- If `OK` → proceed to Step 3 normally.
- If `DEAD_URL_ENTRIES_FOUND` → **STOP before generating cluster report.** Log `⚠ DEAD_URL_DETECTED` to the run log and post Slack:
  ```
  ⚠️ T6 DEAD URL GUARD — {N} entries in keyword-map.json use dead URL prefix(es): {prefixes}.
  These will produce false DROP signals in today's cluster report.
  Data fix required before T6 can run cleanly.
  Known fix: rename affected entries from /doctors-listings/{slug} → /doctors/{slug} in keyword-map.json AND rank-history.json.
  Full list: run keyword-map.json grep for the prefix above.
  ```
  Do NOT run `cluster-report.py` or write a weekly summary until the data is corrected.
  Note: the one-time fix was applied 2026-07-20. This guard fires if the error is re-introduced.

> **Why this matters:** Dead-prefix entries sit at `position: 100` (not-ranking sentinel) in rank-history.json indefinitely. When cluster-report.py buckets them, it sees a sustained 100-position reading that registers as a dramatic category drop. The false signal costs T11 investigation cycles and crowds out real drops from the BACKLOG queue.

### Step 3 — Read both reports
```

## Rationale

The 2026-07-20 data fix was surgical (renamed 12 specific keys). But the underlying process gap — T6 not verifying URL prefixes before cluster bucketing — remains. The next time a task introduces a URL under a dead prefix (which has happened at least once: initial setup routed doctor pages under `/doctors-listings/` by mistake), T6 will generate another false category-drop signal. The guard takes ~5 seconds to run, adds no false positives, and clearly instructs the corrective action. It also documents the known dead-prefix pattern so future tasks know to avoid it.

## Risk assessment

**Very low.** The guard only adds a 5-line Python check to Step 2.5. On the happy path (no dead entries), it's a no-op that adds ~5s to the T6 run. If it fires (dead entries found), the correct response is to delay the cluster report until data is fixed — which is exactly what should have happened on 2026-07-13 but wasn't possible because the guard didn't exist. The only failure mode is a false positive (guard fires when there's no real problem), which can't happen if `dead_prefixes` only contains confirmed-dead prefixes.

## Rollback

Delete the Step 2.5 block from `cowork-tasks/task6-weekly-report.md` (from `### Step 2.5 —` through the closing line before `### Step 3`). Rollback snapshot: `brain/proposed-changes/t6-dead-url-prefix-guard-2026-07-26-2030.md` (this file).

## Veto instructions
To veto: rename this file to `t6-dead-url-prefix-guard-2026-07-26-2030.vetoed.md` and add a `## Veto reason` section.
To approve early: rename to `t6-dead-url-prefix-guard-2026-07-26-2030.approved.md`.
If neither, auto-applies 2026-08-02.
