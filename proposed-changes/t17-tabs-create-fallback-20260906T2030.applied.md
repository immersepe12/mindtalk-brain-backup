# Proposal: T17 Competitive — fallback to existing-tab navigate when tabs_create_mcp stalls
**Proposed:** 2026-09-06T20:30:00+05:30
**Source:** task13-meta-learner-2026-09-06
**Apply on:** 2026-09-13T20:30:00+05:30
**Status:** preview

> ### 🔧 T20 auto-remediation 2026-09-20 — target filename corrected (was MISMATCH-SKIP ×5)
> This proposal had `File to edit: cowork-tasks/task17-competitive.md`, **which does not exist**. The
> real file is `cowork-tasks/task17-competitive-ai-monitor.md`. T10's apply-pass skipped it on 09-13,
> 09-15, 09-17, 09-19 and 09-20 (MISMATCH-SKIP #1–#5) purely on that filename; the proposal's substance
> was never rejected. Corrected below so the next apply-pass can act on it. Stale threshold 2026-09-27.
>
> **Verified against the real file (2026-09-20):** `#### Step 5.5 — Chrome connection pre-check` exists
> at **line 115**; `Step 5.6` does **not** exist (0 matches). The proposal is still valid and un-applied.
>
> ⚠️ **Note for the applier:** the "### Before" block below is a *paraphrase* of Step 5.5, not its
> verbatim text — the real Step 5.5 is a prose sentence plus a numbered list. Do **not** attempt a
> literal string replace. **Append the new Step 5.6 block immediately after the existing Step 5.5
> section** and leave Step 5.5 itself unchanged, except to redirect its "proceed to Step 6" branch on
> the *connected* path to "proceed to Step 5.6".

## Issue detected

T17 has stalled on AI citation queries for **6 consecutive Thursdays** (07-31, 08-07, 08-14, 08-21, 08-28, 09-04). The 08-23 applied proposal `t17-chrome-precheck-20260816T2030` added Step 5.5: check Chrome connection before running AI citation queries. But the stall persists. Root cause (confirmed in `logs/competitive-2026-09-03.txt`): *"CHROME: STALL-SKIPPED | tabs_create_mcp timed out after list_connected_browsers confirmed 2 browsers connected | 6th consecutive Thursday stall"*

The precheck correctly detects that Chrome IS connected (2 browsers) — the failure is specifically in `tabs_create_mcp` (creating a new tab) timing out. Step 5.5 only detects the stall and skips; it does not attempt any recovery path. Since Chrome is connected but new-tab creation fails, the obvious fallback is to navigate within an existing tab rather than creating a new one.

**Evidence:**
- `logs/competitive-2026-09-03.txt` (most recent T17 run): "tabs_create_mcp timed out after list_connected_browsers confirmed 2 browsers connected | 6th consecutive Thursday stall | BACKLOG: CHROME-STALL-2026-09-03"
- `brain/BACKLOG.md` B10: "Chrome stall (T17 6+ weeks blind) + GSC OAuth expired (10+ weeks)" — 200+ AI citation data points missed.
- `brain/applied-changes/t17-chrome-precheck-20260816T2030.applied.md`: precheck applied 08-23 — confirmed still stalling post-apply.
- The precheck added Step 5.5 detect-and-skip, but no Step 5.6 recovery attempt.

## Proposed change
**File to edit:** `cowork-tasks/task17-competitive-ai-monitor.md` *(corrected by T20 2026-09-20; was `task17-competitive.md`, which does not exist)*
**Edit type:** append (add Step 5.6 immediately after the existing Step 5.5 block)

### Before
```
Step 5.5 (Chrome precheck): Before running any AI citation queries, call `list_connected_browsers`. If no browser connected → log "CHROME: OFFLINE — skipping AI citation queries this run" and proceed to Step 6 (DataForSEO-only run). If connected → proceed to citation queries.
```

### After
```
Step 5.5 (Chrome precheck): Before running any AI citation queries, call `list_connected_browsers`. If no browser connected → log "CHROME: OFFLINE — skipping AI citation queries this run" and proceed to Step 6 (DataForSEO-only run). If connected → proceed to Step 5.6.

Step 5.6 (Tab creation fallback): Attempt `tabs_create_mcp` with a 30-second timeout. If it succeeds → use the new tab for all citation queries (current behaviour). If `tabs_create_mcp` times out or fails:
   a. Do NOT skip immediately.
   b. Retrieve existing tab IDs from `list_connected_browsers` response.
   c. Attempt `mcp__claude-in-chrome__navigate` on the first existing tab (no new tab needed).
   d. If navigation succeeds → proceed with citation queries on the existing tab. Log: "CHROME: tabs_create_mcp stalled — using existing tab {tabId} via navigate fallback."
   e. If `navigate` also fails after 20 seconds → log "CHROME: STALL-SKIPPED (tabs_create_mcp + navigate both failed) | BACKLOG: CHROME-STALL-{TODAY}" and skip AI citation block. Proceed to Step 6 DataForSEO-only.
   f. Never let a tab-creation failure alone skip the entire AI citation block when Chrome is confirmed connected.
```

## Rationale

6 consecutive weeks of missed AI citation data (B10: "200+ data points missed") is a significant measurement gap — Mindtalk's first Google AI Overview commercial citation (`cbt therapy online india`) was detected in T17 W16, and the system has been blind to AI citation changes since 07-31. The root cause is specifically `tabs_create_mcp` failing, not Chrome being offline. Navigating an existing tab is a direct drop-in for creating a new one in this context. The fix is a 3-line spec addition with a clear fallback chain that maintains the existing skip-path if both methods fail.

## Risk assessment

Low. The fallback adds one additional navigation attempt before skipping. If the existing tab has stale content from a prior query, the `navigate` call to a fresh URL will replace it — no contamination risk. Worst case: the fallback also fails and T17 proceeds to the existing STALL-SKIPPED path (current behavior). No production code touched.

## Rollback

Before-snapshot: `cowork-tasks/task17-competitive.md` Step 5.5 as applied 2026-08-23 (see `brain/applied-changes/t17-chrome-precheck-20260816T2030.applied.md`). To revert: delete the Step 5.6 block added above. Step 5.5 remains as-is.
