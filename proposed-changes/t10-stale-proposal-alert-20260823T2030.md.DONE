# Proposal: T10 Strategist — alert when proposals sit >14 days past Apply-on date
**Proposed:** 2026-08-23T20:30:00+05:30
**Source:** task13-meta-learner-2026-08-23
**Apply on:** 2026-08-30T20:00:00+05:30
**Status:** preview

## Issue detected

Two proposals have been sitting in `brain/proposed-changes/` for **28 days** past their `Apply on:` dates with no alert and no resolution:

- `t16-read-pending-human-actions-2026-07-26-2030.md` — Apply on: 2026-08-02. Still `.md` (not `.applied`, not `.vetoed`).
- `t5-floor-miss-brain-flag-2026-07-26-2030.md` — Apply on: 2026-08-02. Still `.md` (not `.applied`, not `.vetoed`).

Both were almost certainly skipped by the mismatch gate (Before block changed since filing) and left in queue per the existing Step 10 rule. But the mismatch Slack alert fires ONCE, and there is no recurring escalation if the proposal sits unapplied for weeks. Kushal has no visibility that two system proposals are stale and unresolved.

## Proposed change
**File to edit:** `cowork-tasks/task10-strategist.md`
**Edit type:** line-edit (append a stale-detection block between the existing hard-rule and Step 11)

### Before
```
**Hard rule:** If you encounter ANY unexpected behaviour during apply (file not found, edit syntax doesn't match Before block, etc.), STOP, do not partially apply, post `⚠ APPLY FAILED` to Slack with full context, and leave the proposal in the queue for human resolution.

### Step 11 — Post Slack summary
```

### After
```
**Hard rule:** If you encounter ANY unexpected behaviour during apply (file not found, edit syntax doesn't match Before block, etc.), STOP, do not partially apply, post `⚠ APPLY FAILED` to Slack with full context, and leave the proposal in the queue for human resolution.

**Stale proposal scan (run after apply loop):** For every `.md` file in `brain/proposed-changes/` that is NOT `.applied.md` and NOT `.vetoed.md`, parse its `Apply on:` frontmatter field. If `Apply on:` is more than **14 days** in the past, post this alert to `#seo-workflow-mindtalk`:
```
⚠️ STALE PROPOSAL — {id}
Apply on: {apply_on_date} ({N} days overdue)
Still in queue: not applied, not vetoed.
Likely cause: Before-block mismatch gate skipped it and no human resolved the mismatch.
Action required: either (a) update the proposal's Before block to match current file state, or (b) rename to {id}.vetoed.md to abandon it.
```
Document in `brain/memory/applied-history.md`:
```
{TIMESTAMP} | STALE-ALERT | proposal: {id} | apply_on: {date} | overdue: {N} days
```

### Step 11 — Post Slack summary
```

## Rationale

The mismatch gate is correct — it prevents applying stale edits to changed files. But its one-time Slack alert gets buried. Without a recurring escalation, stale proposals silently accumulate (confirmed: 2 proposals, 28 days overdue, zero follow-up). The stale scan catches these every daily Strategist run until resolved.

## Risk assessment

Low. This is read-only scanning + Slack alerting — no file modifications. No risk of incorrect edits. The only false positive is alerting on a proposal that was intentionally left pending (rare; user can just veto it to silence future alerts).

## Rollback

Snapshot: `brain/before-snapshots/task10-strategist-{TIMESTAMP}.bak` (created at apply time)
To rollback: restore snapshot to `cowork-tasks/task10-strategist.md`.
