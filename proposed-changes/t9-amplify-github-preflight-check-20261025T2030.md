# Proposal: Add Amplify/GitHub pre-flight access check to Task 9 before blog authoring

**Proposed:** 2026-10-25T20:30 IST
**Source:** T13 Meta-Learner run 2026-10-25
**Apply on:** 2026-11-01T20:00 IST
**Status:** preview

## Issue detected

On 2026-10-21 the system migrated from Vercel to AWS Amplify + GitHub PR mode (EXARFit/mindtalk-website). Task 9 override notes document this (lines 2–10), but the spec has **no pre-flight check** to verify GitHub repo access before committing N hours of brief authoring. Evidence: Task 9 currently spends 2–4 hours producing MDX and then tries to push via `gh_ship.py` — if the GitHub token is expired or the repo is private/locked, all authoring work is wasted and the run ends in a silent error. The Vercel connector check that used to serve this purpose (`from mcp_vercel import get_project`) has been superseded and the replacement t9-vercel-preflight proposal (20261018T2030) was vetoed by T13 on 2026-10-25 because it referenced Vercel.

**Evidence:**
- `brain/BRAIN.md` 2026-10-21: "REPO MOVE — system moved from Vercel to Amplify"
- `brain/BRAIN.md` 2026-10-24: "Ship path works in PR mode"
- `brain/proposed-changes/t9-vercel-preflight-build-block-20261018T2030.vetoed-by-T13-2026-10-25.md`: prior attempt vetoed

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task9-auto-ship-new-blogs.md`
**Edit type:** line-edit (insert before existing Step 1 heading)

### Before

```
## Step-by-step execution

### Step 1 — Identify unshipped NEW blog briefs
```

### After

```
## Step-by-step execution

### Step 0 — Pre-flight: verify GitHub / Amplify access

Before spending any time on brief authoring, confirm the ship path is open:

```bash
# 1. Verify GitHub CLI is authenticated and repo is accessible
gh auth status 2>&1 | grep -q "Logged in" || { echo "❌ PREFLIGHT FAIL: gh not authenticated"; exit 1; }
gh repo view EXARFit/mindtalk-website --json name 2>&1 | grep -q "mindtalk-website" \
  || { echo "❌ PREFLIGHT FAIL: cannot read EXARFit/mindtalk-website — token may be expired or repo access revoked"; exit 1; }

# 2. Confirm gh_ship.py exists and is importable (dry-run check)
python3 -c "import ast; ast.parse(open('scripts/gh_ship.py').read())" 2>&1 \
  || { echo "❌ PREFLIGHT FAIL: scripts/gh_ship.py not parseable"; exit 1; }

echo "✅ PREFLIGHT PASS: GitHub access confirmed, ship path ready"
```

If PREFLIGHT FAIL: **stop immediately.** Post to Slack `#seo-workflow-mindtalk`:
```
🚨 T9 ABORTED — pre-flight failed
Reason: [paste error line above]
No briefs were authored. Fix GitHub access and re-run.
```
Do NOT proceed to Step 1 until PREFLIGHT PASS.

### Step 1 — Identify unshipped NEW blog briefs
```

## Rationale

The pre-flight gate prevents wasting 2–4 hours of compute and API calls when the ship path is broken. The check is idempotent, takes < 5 seconds, and uses the same `gh` CLI that `gh_ship.py` relies on — so a pass here means the ship will succeed (barring a mid-run outage). This is the Amplify/GitHub equivalent of the Vercel connector check that used to serve this purpose.

## Risk assessment

Low. The check only reads (no write, no PR creation). If `gh auth status` fails, it means the token really is expired and the run would have failed later anyway. The only new failure mode is a false-positive abort if the `mindtalk-website` repo is temporarily private-mode during a maintenance window — unlikely, and a re-run resolves it.

## Rollback

Strategist snapshots the file before apply. To revert:
`cp brain/before-snapshots/task9-auto-ship-new-blogs-{TIMESTAMP}.bak cowork-tasks/task9-auto-ship-new-blogs.md`
The Step 0 block can also be deleted manually in < 30 seconds.

## Veto instructions

To veto: rename this file to `t9-amplify-github-preflight-check-20261025T2030.vetoed.md` and add a `## Veto reason` section.
To approve early: rename to `t9-amplify-github-preflight-check-20261025T2030.approved.md`.
