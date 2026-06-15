# Proposed Changes Queue

This folder holds **Meta-Learner proposals** for workflow improvements that haven't yet been applied.

## File format

Each proposal is a single markdown file: `{proposal-id}-{TIMESTAMP}.md`

```markdown
# Proposal: {short description}
**Proposed:** {ISO-8601 timestamp}
**Source:** {which Meta-Learner run identified this}
**Apply on:** {timestamp + 7 days} (auto-apply by Strategist if not vetoed)
**Status:** preview | vetoed | applied | abandoned

## Issue detected
{What's wrong, with evidence + log references}

## Proposed change
**File to edit:** `{absolute path}`
**Edit type:** {sed-replace | line-edit | append | full-rewrite}

### Before
```
{exact content to be replaced}
```

### After
```
{exact replacement content}
```

## Rationale
{Why this change improves the system. Cite evidence.}

## Risk assessment
{What could go wrong if this is applied incorrectly?}

## Rollback
{How to revert if the change causes issues — usually: copy `brain/before-snapshots/{filename}-{TIMESTAMP}.bak` back}

## Veto instructions
To veto: rename this file from `{proposal-id}.md` to `{proposal-id}.vetoed.md` and add a `## Veto reason` section explaining why.

To approve early: rename to `{proposal-id}.approved.md` — Strategist's next 8 PM run will apply it.
```

## How the apply pass works (Strategist daily 8 PM)

Strategist's daily run includes Step 11:

1. List all `*.md` files in this folder
2. For each file:
   - Skip if filename ends with `.vetoed.md` → mark abandoned
   - Skip if filename ends with `.applied.md` → already done
   - If filename ends with `.approved.md` → apply immediately
   - If `Apply on:` timestamp is in the past AND no veto → apply
   - Otherwise → leave for next run

3. For each apply:
   - Snapshot the target file to `brain/before-snapshots/{filename}-{TIMESTAMP}.bak`
   - Apply the edit per spec
   - Rename proposal file to `{proposal-id}.applied.md`
   - Move applied file to `brain/applied-changes/`
   - Post Slack confirmation with link to before-snapshot for easy rollback

## Hard rules

- Strategist can ONLY apply proposals for files matching:
  - `brain/*.md`
  - `cowork-tasks/*.md`
  - `config.json`
  - `/Users/agent/Documents/Claude/Scheduled/*/SKILL.md` (Cowork cron prompts)
- Strategist CANNOT apply proposals for:
  - `scripts/*.py` (Python — too high-risk)
  - `src/**` (production code in mindtalk repo)
  - Anything outside the SEO workflow ecosystem

If Meta-Learner proposes an edit to a forbidden path, the proposal is auto-flagged for human review only (never auto-applied).
