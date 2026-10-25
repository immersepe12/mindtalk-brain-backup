# Proposal: T9 — Add Vercel project pre-flight check before MDX authoring

**Proposed:** 2026-10-18T20:30:00+05:30
**Source:** META-LEARNER T13 weekly run 2026-10-18T2030
**Apply on:** 2026-10-25T20:00:00+05:30
**Status:** preview

## Issue detected

PROD-ORIGIN-STALE-01 has been active since 2026-10-14 (5+ days). During this window
T9 ran on 2026-10-15 and 2026-10-16, authored MDX, pushed to feature branches, and
polled for Vercel previews — but the mindtalk project is returning 404 from the Vercel
connector. Strategist logged T9-BUILD-BLOCK-01 in BACKLOG both days. This means two
completed blog briefs are sitting on feature branches that never deployed to production.

T9 currently has NO pre-flight check. Step 0 moves directly into "identify unshipped
briefs → author MDX", so work is wasted on every blocked run. The run only discovers
the connector failure at Step 4 (build verification), after spending time writing MDX.

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task9-auto-ship-new-blogs.md`

**Edit type:** line-edit (insert new Step 0-PRE block before current Step 1)

### Before

```
## Step 1 — Identify unshipped briefs
```

### After

```
## Step 0-PRE — Vercel connector pre-flight check

Before authoring any MDX, verify the Vercel connector can reach the mindtalk project:

```python
from mcp_vercel import get_project
result = get_project(project_id_or_name="mindtalk")
if result.get("status") == 404 or "not found" in str(result).lower():
    # Connector is stale / project unreachable
    send_push_notification(
        "T9 ABORTED: Vercel connector 404 on mindtalk project. "
        "Check PROD-ORIGIN-STALE-01. No MDX authored this run."
    )
    post_slack(
        channel="#seo-workflow-mindtalk",
        message=(
            "🚫 *T9 auto-ship ABORTED* — Vercel connector returned 404 "
            "for `mindtalk` project. No MDX authored.\n"
            "Action needed: re-authenticate Vercel connector or verify project "
            "still exists.\n"
            "Brain entry: PROD-ORIGIN-STALE-01 active."
        )
    )
    raise SystemExit("T9 aborted: Vercel pre-flight failed")
```

If the pre-flight passes (HTTP 200, project found), continue to Step 1.

## Step 1 — Identify unshipped briefs
```

## Rationale

Evidence from brain/BRAIN.md (2026-10-18 T12 entry): PROD-ORIGIN-STALE-01 day 5.
Strategist decisions 2026-10-15 and 2026-10-16 both show T9 blocked on Vercel 404
AFTER authoring. Early abort saves 20-30 minutes per blocked run and prevents
half-deployed feature branches from cluttering the repo.

## Risk assessment

Low risk. Pre-flight is read-only (GET only). If pre-flight itself errors (transient
network), catch the exception and treat as a pass-through to not false-abort on a
transient glitch — log a warning instead. The check adds ~5 seconds to T9 happy path.

## Rollback

Remove the Step 0-PRE block from task9-auto-ship-new-blogs.md. T9 reverts to its
prior behavior (discovers Vercel failure at Step 4 instead of Step 0).

## Veto instructions

If you believe early-abort is too aggressive (e.g., transient 404 should not block),
rename this file to `t9-vercel-preflight-build-block-20261018T2030.vetoed-by-verifier.md`
and add a one-line reason. The Strategist will not apply it.
