# Proposal: T11 verify scheduled task creation before marking DONE (AP10 guard)

**Proposed:** 2026-07-05T20:00:00+05:30
**Source:** task13-meta-learner-2026-07-05
**Apply on:** 2026-07-12T20:00:00+05:30
**Status:** preview

## Issue detected

Anti-Pattern AP10: "Executor claims completion without verifying the scheduled task was actually created." This pattern occurred **twice in a single Strategist run (2026-07-04)**:

**Gap 1 — W10-D28 (Sprint C day-28 check):**
- BACKLOG row marked "COMPLETED 07-03 — task `mindtalk-watch-sprint-c-day28-2026-07-07` created"
- Strategist scanned all 50+ scheduled tasks on 07-04 — task NOT found
- Root cause: Executor T11 called `create_scheduled_task` and reported success based on the MCP return value, but the task did not appear in `list_scheduled_tasks`
- Consequence: Sprint C's 9-page day-28 MONITOR check would have silently not fired on 07-07
- Correction: Strategist created the task manually on 07-04, adding unplanned overhead to the daily run

**Gap 2 — W18-W21 clinical review (07-13):**
- WATCH.md 07-03 stamp listed "07-13 clinical reviews fire" as an upcoming check
- Strategist found no corresponding scheduled task in any of the 50+ tasks scanned
- Same failure mode: the task was referenced in WATCH.md as if scheduled but never actually created

**Root cause in T11 spec:** Section 4d (`schedule_watch_check`) step 3 says "Create Cowork one-off task via `create_scheduled_task`" and immediately moves to "Update WATCH.md: status → scheduled" and "Mark BACKLOG row complete." There is no verification step between creation and completion marking.

AP10 was added to ANTI-PATTERNS.md after the first occurrence, but the T11 spec was never updated to prevent it structurally. The pattern recurred in the same week.

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task11-executor.md`
**Edit type:** line-edit (section 4d `schedule_watch_check`, steps 3-5)

### Before

```
3. Create Cowork one-off task via `create_scheduled_task`:
   - taskId: `mindtalk-watch-{slug}-{date}`
   - fireAt: 9:00 AM IST on target date
   - prompt: read WATCH.md row for {slug}, run rank check, evaluate, update Learner
4. Update WATCH.md: status → `scheduled`
5. Mark BACKLOG row complete
```

### After

```
3. Create Cowork one-off task via `create_scheduled_task`:
   - taskId: `mindtalk-watch-{slug}-{date}`
   - fireAt: 9:00 AM IST on target date
   - prompt: read WATCH.md row for {slug}, run rank check, evaluate, update Learner

3a. **AP10 guard — verify creation before proceeding:**
   Call `list_scheduled_tasks` immediately after step 3. Scan the returned list for the taskId from step 3.
   - **If found:** proceed to step 4.
   - **If NOT found:** retry `create_scheduled_task` once. Call `list_scheduled_tasks` again.
     - If found on retry: proceed to step 4.
     - If still NOT found: post Slack alert to `#seo-workflow-mindtalk`:
       `⚠ T11 AP10: scheduled task {taskId} not confirmed in task list after 2 attempts. Manual creation required. BACKLOG row NOT marked complete.`
       Then log the failure to `brain/memory/experiments/{TODAY}-watch-creation-failed-{slug}.md` and stop (do not mark BACKLOG row complete).

4. Update WATCH.md: status → `scheduled` *(only after step 3a confirms the task exists)*
5. Mark BACKLOG row complete *(only after step 3a confirms the task exists)*
```

## Rationale

AP10 is documented but has no structural enforcement in T11's spec — it's purely a behavioral reminder. Two occurrences in one week (both in a single Strategist run) confirm the reminder alone isn't enough. The fix adds a mandatory verification call (`list_scheduled_tasks`) between creation and completion marking, with a retry path and a clear failure escalation.

The cost is one extra MCP call per watch task created (cheap). The benefit: watch tasks that don't actually exist can no longer be silently marked as scheduled. Strategist overhead from discovering and re-creating missing tasks (estimated 20+ min per occurrence per BRAIN.md 07-04 log) is eliminated.

This also makes AP10 self-enforcing: a future Executor agent that "forgets" the anti-pattern will still be caught by the spec's mandatory verification step.

## Risk assessment

Low. The change adds a read operation (`list_scheduled_tasks`) and a conditional retry — no new write operations beyond what T11 already does. The failure path (Slack alert + stop) is safer than the current failure path (silently marking DONE when the task doesn't exist).

One edge case: if `list_scheduled_tasks` returns a truncated list (pagination), the verification check could falsely fail. Mitigated by the retry path — two confirmations before escalating. If pagination is an issue, Strategist would have seen the same problem scanning 50+ tasks; this hasn't been reported.

## Rollback

Snapshot: `brain/before-snapshots/task11-executor.md-{TIMESTAMP}.bak`

To revert: copy snapshot back. Rollback means returning to the unguarded spec (AP10 risk resumes). Any watch tasks created between apply and rollback are unaffected — they already exist or don't, independent of the spec.

## Veto instructions

To veto: rename to `t11-watch-task-creation-verify-2026-07-05-2000.vetoed.md` and add `## Veto reason`.
To approve early: rename to `t11-watch-task-creation-verify-2026-07-05-2000.approved.md`.
