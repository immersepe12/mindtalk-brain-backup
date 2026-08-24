# Proposal: T17 — Add Chrome connection pre-check before AI citation queries (Step 5.5)
**Proposed:** 2026-08-16T20:30:00+05:30
**Source:** task13-meta-learner-2026-08-16
**Apply on:** 2026-08-23T20:00:00+05:30
**Status:** preview

## Issue detected

T17 (Competitive + AI Citation Monitor) has failed to complete its AI citation step 3 consecutive Thursdays (confirmed BACKLOG entries T17-18 on 2026-07-30, 2026-08-06, 2026-08-13, and T17-19 on 2026-08-13). Root cause: the Claude-in-Chrome extension enters a stale state after heavy batch jobs (T9 Auto-Ship at 3 PM IST + T11 Executor at 4:30 PM IST) run on the same Thursday afternoon before T17's 7 PM IST slot. The Chrome MCP tools time out silently, and T17 currently has no pre-check before diving into Step 6 AI queries — so the entire AI citation section is wasted (no data + no recovery attempt).

Impact: 3 consecutive weeks of stale AI citation trajectory. The Google AI OV "cbt therapy online india" commercial citation gain (T17 run 2026-07-16) and Perplexity Q3 "psychiatrist near me bangalore" gain (2026-08-06) cannot be tracked if the citation step keeps failing. BACKLOG T17-18 is currently flagged `flag_for_human` with no automated recovery path.

## Proposed change
**File to edit:** `cowork-tasks/task17-competitive-ai-monitor.md`
**Edit type:** sed-replace

### Before
```
#### Step 6 — Query each AI search engine via Claude in Chrome

For each query, use the `mcp__Claude_in_Chrome__*` toolkit to:
```

### After
```
#### Step 5.5 — Chrome connection pre-check (added 2026-08-23 — T17-18/T17-19 recurring stall fix)

Before starting AI citation queries, verify the Chrome extension is connected:

1. Call `mcp__claude-in-chrome__list_connected_browsers`.
   - If at least one browser is returned → proceed to Step 6 normally.
   - If the response is empty or returns an error:
     a. Call `mcp__computer-use__open_application` with `"Google Chrome"` to bring Chrome forward.
     b. Wait 5 seconds, then call `list_connected_browsers` again.
     c. If a browser is now returned → proceed to Step 6.
     d. If still not connected → **skip Step 6 entirely**. Post to `#seo-workflow-mindtalk`:
        ```
        ⚠️ *T17 Chrome stall — AI citation step skipped*
        Chrome extension not connected after restart attempt.
        All citation cells for this week carry over from last week's run.
        Action needed: reopen Chrome + reload extension before next Thursday.
        BACKLOG: CHROME-STALL-{YYYY-MM-DD}
        ```
        Then proceed directly to Step 7 (DataForSEO keyword tracking only).

Log the connection check result to `logs/competitive-{TODAY}.txt` as either `CHROME: CONNECTED` or `CHROME: STALL-SKIPPED`.

#### Step 6 — Query each AI search engine via Claude in Chrome

For each query, use the `mcp__Claude_in_Chrome__*` toolkit to:
```

## Rationale

3 consecutive data-loss Thursdays means the AI citation trajectory (the primary differentiator in T17 vs competitors) is now unreliable. The fix costs <30 seconds when Chrome is connected (one empty tool call), saves the entire citation step when Chrome is stalled, and gives Kushal actionable recovery instructions instead of a silent skip. The open-application + re-check pattern is the same used in other tasks that depend on external browser state.

## Risk assessment

Low. The pre-check is a no-op when Chrome is connected (expected 90% of cases). The fallback posts a Slack flag and continues — T17 still delivers the DataForSEO keyword ranking section. The only regression risk is if `open_application("Google Chrome")` has a side effect on another open tab — mitigated by the fact that T9/T11 have already completed their git pushes by 7 PM IST.

## Rollback

Before snapshot: `brain/proposed-changes/t17-chrome-precheck-20260816T2030.md` (this file, Before section).
To revert: delete Step 5.5 block and restore the original Step 6 header line.
