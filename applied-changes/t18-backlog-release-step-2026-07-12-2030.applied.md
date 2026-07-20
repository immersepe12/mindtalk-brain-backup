# Proposal: T18 — Add Step 0 to release expired "Awaiting professional input" BACKLOG entries
**Proposed:** 2026-07-12T20:30:00+05:30
**Source:** task13-meta-learner-2026-07-12
**Apply on:** 2026-07-19T20:00:00+05:30
**Status:** preview

## Issue detected

T18's Step 5 states: _"If 21 days pass with no recording, the page is released back to the standard refresh queue and flagged in next week's professional-input run for re-pick consideration."_

However, no step in T18 (or any other task) **actually removes** expired entries from BACKLOG.md's `## Awaiting professional input` section. T18 only ADDS entries (Step 5); it never REMOVES them. The result:

- Pages accumulate on the exclusion list indefinitely.
- T11 Executor reads BACKLOG and skips these pages — correctly during the 21-day window, but incorrectly AFTER the deadline passes with no recording.
- The pages become permanently invisible to the refresh pipeline until someone manually edits BACKLOG.

**Evidence (current BACKLOG state, 2026-07-12):**

- W26 entries (6 pages): "don't refresh until: recording received or **2026-07-13**" — expires TOMORROW. No automated cleanup will run.
- W27 entries (6 pages): expiry 2026-07-20.
- W28 entries (6 pages): expiry 2026-07-27.
- Total: **18 pages** accumulating on the exclusion list with no purge mechanism.

When T18 runs next Monday (07-14), it calls Step 1 which reads `professional-input-history.md` (to enforce the 60-day re-pick ban) and WATCH.md (to skip observed pages). It does NOT read BACKLOG "Awaiting professional input" to remove expired rows.

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task18-professional-input-briefs.md`
**Edit type:** line-edit (insert new Step 0 before existing Step 1)

### Before

```
### Step 1 — Load eligibility pool

Read these sources:
```

### After

```
### Step 0 — Release expired professional-input holds from BACKLOG

Before scoring this week's picks, clean up stale entries in BACKLOG.md.

Read the `## Awaiting professional input` section of `brain/BACKLOG.md`.

For each row in that table:

1. Parse the "Don't refresh until" date (format: `recording received or YYYY-MM-DD`).
2. If **today's date > parsed date** (i.e., the 21-day window has passed) AND the row does NOT contain "recording received":
   - **Remove the row** from the `## Awaiting professional input` table in BACKLOG.md.
   - Append a release log entry to `logs/professional-input-{TODAY}.md`:
     ```
     RELEASED — {page-path} — 21-day window expired {YYYY-MM-DD}, no recording received. Page returns to standard refresh queue.
     ```
   - Post a brief Slack note to `#seo-workflow-mindtalk` if 2+ pages release in the same run (batched, not per-page):
     `ℹ️ T18: Released {N} professional-input holds from BACKLOG (21-day window expired, no recording). Pages back in standard refresh queue.`

3. If the row contains "recording received" AND the date has passed → also remove it (the recording arrived and the refresh should have already been done; the hold is complete).

Do NOT remove rows whose deadline is still in the future.

---

### Step 1 — Load eligibility pool

Read these sources:
```

## Rationale

T18's Step 5 promises an automatic release mechanism after 21 days. That mechanism was never implemented. With 18 pages currently blocked and W26 entries expiring tomorrow, the exclusion list is growing without bound. T11 Executor will continue skipping these pages indefinitely unless BACKLOG is manually edited.

Adding this as Step 0 (before Step 1's eligibility scoring) ensures the cleanup runs every Monday BEFORE the new picks are added — so released pages are immediately eligible for this week's selection if they score highly.

## Risk assessment

Low. The only change is removing rows from BACKLOG's "Awaiting professional input" table when their dates have passed. No content is modified. No brief is auto-shipped. The worst case: a row is accidentally removed one day early due to timezone handling — the page becomes eligible for refresh one day early, which is harmless (T11 won't rush to refresh it immediately).

One edge case: if a reviewer says "recording coming tomorrow" in a Slack thread but the BACKLOG row has no "recording received" marker, Step 0 would release the hold on the expiry date anyway. Mitigation: reviewers should update BACKLOG to "recording received" when they submit; Step 0 respects that marker.

## Rollback

Snapshot: `brain/before-snapshots/task18-professional-input-briefs.md-{TIMESTAMP}.bak`

To revert: copy snapshot back. Any rows already released from BACKLOG would need to be manually re-added if the rollback is needed urgently — but since those rows were already past their 21-day window, manually re-adding them is only necessary if a recording actually arrived after the Step 0 cleanup ran.

## Veto instructions

To veto: rename this file to `t18-backlog-release-step-2026-07-12-2030.vetoed.md` and add a `## Veto reason` section.
To approve early: rename to `t18-backlog-release-step-2026-07-12-2030.approved.md`.
