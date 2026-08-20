# Proposal: T9 — Escalate stuck /doctors-listings/ briefs to BACKLOG when count > 5
**Proposed:** 2026-08-16T20:30:00+05:30
**Source:** task13-meta-learner-2026-08-16
**Apply on:** 2026-08-23T20:00:00+05:30
**Status:** preview

## Issue detected

T5 (New Content Discovery) correctly generates Tier A city doctor listing briefs per INTENT-PRIORITY.md. These land in `/doctors-listings/` paths. T9 (Auto-Ship) Step 1 Python regex explicitly matches only `(blogs|treatments|illnesses)` paths — so every `/doctors-listings/` brief is silently skipped every run with no escalation.

Result: a dead zone. T5's 2026-08-10 run created 13 STANDING_TIER_A_BACKLOG city doctor briefs (kolkata/pune/chennai/mumbai/delhi specialists) — ALL stuck. The queue has been growing without any alert: 13 stuck (08-05) → 15 (08-07) → 30 (08-12) → 30+ (08-14). T9 logs show "Nothing to ship today" even though 30+ high-Tier-A briefs exist. This is the root cause of SYSTEM-UNDERUTILISED flagged in BACKLOG (W33: 6 pages/week, W34: ~5 pages/week, both below the 8/week floor). BACKLOG entry `SYSTEM-UNDERUTILISED-W33-W34` explicitly delegated resolution to "T13 Meta-Learner 2026-08-16."

No task auto-ships or escalates /doctors-listings/ briefs. The fix is not to expand T9 scope (that requires a dev decision on whether to add a doctors-listings MDX pipeline in the mindtalk repo) — but to make T9 proactively surface the stuck queue so the decision can be made.

## Proposed change
**File to edit:** `cowork-tasks/task9-auto-ship-new-blogs.md`
**Edit type:** sed-replace

### Before
```
If 0 candidates, log "Nothing to ship today" to `logs/auto-ship-{TODAY}.txt`, post a brief "No queue today" to Slack `#seo-workflow-mindtalk`, and exit cleanly.
```

### After
```
**Before exiting on 0 candidates: check for stuck out-of-scope briefs (added 2026-08-23 — SYSTEM-UNDERUTILISED fix)**

Regardless of whether candidates were found, run this secondary check:

```python
import glob, re, datetime, pathlib

BRIEFS = pathlib.Path('briefs')
DOCTORS_RE = re.compile(r'\*\*Suggested File:\*\*\s+src/content/doctors-listings/[\w/-]+\.mdx')
stuck = [f for f in BRIEFS.glob('NEW-*-brief.md') if DOCTORS_RE.search(f.read_text())]

if len(stuck) > 5:
    backlog_path = pathlib.Path('brain/BACKLOG.md')
    if 'DOCTOR-LISTING-SHIP-NEEDED' not in backlog_path.read_text():
        entry = (
            f"| DOCTOR-LISTING-SHIP-NEEDED | flag_for_human | {datetime.date.today()} | "
            f"{len(stuck)} /doctors-listings/ briefs stuck — T9 regex scope excludes this path. "
            f"Decision needed: (A) extend T9 scope to doctors-listings once MDX pipeline confirmed, "
            f"or (B) create a separate doctor-listing ship task. All are Tier A (70-95% booking intent). | "
            f"T9 auto-ship secondary check |\n"
        )
        with open(backlog_path, 'a') as fh:
            fh.write(entry)
        # Post Slack flag
        print(f"DOCTOR-LISTING-BACKLOG: {len(stuck)} stuck /doctors-listings/ briefs — BACKLOG entry written")
```

Log the count to `logs/auto-ship-{TODAY}.txt` as `DOCTORS-LISTINGS-STUCK: N` (even if < 5, log the count for tracking).

If 0 candidates, log "Nothing to ship today" to `logs/auto-ship-{TODAY}.txt`, post a brief "No queue today" to Slack `#seo-workflow-mindtalk`, and exit cleanly.
```

## Rationale

The stuck queue is invisible to every task. T9 says "Nothing to ship" — technically true — but hides that 30+ Tier A briefs are waiting. Adding the secondary check costs one extra glob + read pass per T9 run (negligible). The BACKLOG entry is deduped (checks for `DOCTOR-LISTING-SHIP-NEEDED` before writing), so it fires once and stays until resolved. The 5-brief threshold prevents noise from transient single-brief lags. This directly addresses SYSTEM-UNDERUTILISED W33-W34, which was explicitly delegated to this Meta-Learner run.

## Risk assessment

Low. The check is read-only (glob + file read + conditional append to BACKLOG.md). It cannot affect the ship pipeline. The dedup check prevents BACKLOG.md from accumulating repeated entries. The only risk is if `DOCTOR-LISTING-SHIP-NEEDED` string appears in a different BACKLOG entry for an unrelated reason — mitigated by the specificity of the string.

## Rollback

Before snapshot: `brain/proposed-changes/t9-doctor-listing-backlog-escalation-20260816T2030.md` (this file, Before section).
To revert: remove the secondary check block and restore just the original "If 0 candidates" line.
