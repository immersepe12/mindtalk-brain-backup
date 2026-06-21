# Proposal: Fix stale "X/10" weekly-cap reference in Task 3 output template

**Proposed:** 2026-06-21T20:04:41+05:30
**Source:** task13-meta-learner-2026-06-21
**Apply on:** 2026-06-28T20:04:41+05:30
**Status:** preview

## Issue detected

`config.json` sets `max_urls_per_week: 20` and `max_new_content_per_week: 20`. Task 3's spec was migrated to the 20-cap everywhere EXCEPT its closing Output template, which still prints "X/10":

- `cowork-tasks/task3-serp-analysis-briefs.md:240` → `- Total briefs created this week vs weekly limit (X/10)`
- But the same file already says 20 at lines 35 (`Maximum 20 per week total`), 37 (`Cap: 20 refresh briefs per week (config.json max_urls_per_week=20)`), 218 (`Weekly total: [N]/20`), 228 (`Weekly limit reached (20/20)`).

Downstream effect — the agent following this stale instruction emits a 10-denominator across the whole brief log:
- `logs/briefs-2026-06-15.txt:25` → `Weekly limit at run time: 0/10 used`
- `logs/briefs-2026-06-15.txt:80,142,179` → `RUNNING WEEKLY TOTAL ... 1/10 ... 2/10`
- `logs/briefs-2026-06-15.txt:154` → `Task 3 REFRESH briefs (counts against 10/week cap): 2/10`
- Same `/10` pattern in `logs/briefs-2026-06-08.txt:51,96,134`.

A "/10" denominator on a 20 cap makes the queue look ~twice as full as it is, and risks the agent self-throttling brief creation at 10 when 20 are allowed (P4: shipping, not brief-gen, is the bottleneck — artificially halving the brief budget is the wrong direction).

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task3-serp-analysis-briefs.md`
**Edit type:** line-edit (line 240)

### Before
```
- Total briefs created this week vs weekly limit (X/10)
```

### After
```
- Total briefs created this week vs weekly limit (X/20, per config.json max_urls_per_week)
```

## Rationale

Single-source-of-truth alignment: the cap lives in `config.json` (20). Every human-facing number Task 3 emits should reflect that. This is the last stale "10" in the Task 3 spec; fixing it removes the wrong denominator from the brief log header the agent generates each run, and references config.json so the number stays correct if the cap changes again. Matches the first-run note in `task13-meta-learner.md` (issue #1).

## Risk assessment

Near-zero. This edits an output-format instruction in a task spec, not logic or a cap value. Worst case is a cosmetic wording difference in the log. No behavioural code path, no production file, no cap change. Note: the `/10` literals inside `scripts/publish-mdx-update.py` (forbidden path) are NOT touched by this proposal — if any residual "/10" persists in logs after this applies, a separate `human-review-only` proposal for that script will be filed.

## Rollback

Strategist snapshots the file to `brain/before-snapshots/task3-serp-analysis-briefs.md-{TIMESTAMP}.bak` before applying. To revert: copy that snapshot back over `cowork-tasks/task3-serp-analysis-briefs.md`.

## Veto instructions

To veto: rename this file to `cap-mismatch-task3-log-template-2026-06-21-2004.vetoed.md` and add a `## Veto reason` section.
To approve early: rename to `cap-mismatch-task3-log-template-2026-06-21-2004.approved.md`.
