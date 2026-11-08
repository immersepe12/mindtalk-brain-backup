# Proposal: T5 — Add tracking-db BRIEF_CREATED pre-filter to Step 2 (BRIEF-COLLISION-GATE-01 fix)

**Proposed:** 2026-11-01T20:30:00+05:30
**Source:** META-LEARNER T13 weekly run 2026-11-01T2030
**Apply on:** 2026-11-08T20:00:00+05:30
**Status:** preview

## Issue detected

`brain/BACKLOG.md` flag **BRIEF-COLLISION-GATE-01** (added 2026-10-28) documents that T5
is queuing URLs that already have briefs in `BRIEF_CREATED` status in `tracking-db.json`.
The Strategist explicitly flagged this as "Meta-Learner Sunday 11-01 candidate" on four
consecutive daily runs (Oct 28–31). AP7 covers the anti-pattern conceptually but T5's
Step 2 filter only checks `new-content-opportunities.json` status — it does not
cross-reference `tracking-db.json` directly.

**Root cause:** When `new-content-opportunities.json` is out of sync with `tracking-db.json`
(e.g., a brief was written by a human or a prior T5 run that partially failed to update
the opportunities file), the Step 2 filter sees the opportunity as `status == "OPPORTUNITY"`
and queues it again. The result: duplicate briefs for the same URL path, wasted T5 runtime,
and potentially two competing briefs reaching T9.

The COLLECTION + QUEUE COLLISION CHECK (Step 2 BRIEF COUNT GATE) does check the `briefs/`
directory for file collisions, but not tracking-db BRIEF_CREATED status — a different plane.

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task5-new-content-discovery.md`

**Edit type:** line-edit (append tracking-db cross-reference guard to the Step 2 filter sentence)

### Before

```
From the opportunities list, filter to only `status == "OPPORTUNITY"` (not already briefed or published).
```

### After

```
From the opportunities list, filter to only `status == "OPPORTUNITY"` (not already briefed or published). **Before adding any candidate to the shortlist, also cross-reference `tracking-db.json`: exclude any URL whose `url_path` already has a `tracking-db.json` entry with `status` of `BRIEF_CREATED`, `PUBLISHED`, `LIVE`, or `IN_PROGRESS` — even if its `new-content-opportunities.json` status is still `"OPPORTUNITY"`. Log each exclusion: `AP7-GUARD: skipping {url_path} — tracking-db status={status} (opportunities cache out of sync).` This prevents BRIEF-COLLISION-GATE-01 duplication when the two data sources diverge.**
```

## Rationale

This is a 1-line addition to an existing filter sentence. It makes the existing Step 2 filter
authoritative against the tracking-db (the ground-truth source of record for URL status) rather
than relying solely on the opportunities JSON which can drift. AP7 already names this as a hard
anti-pattern; this change enforces it at the filter step where it costs nothing (a dict lookup)
rather than catching it at Step 5.5 quality pre-check or worse, at T9 ship time.

The exclusion log makes the drift visible for debugging.

## Risk assessment

Very low. This adds a guard only — it can never incorrectly block a genuine new URL because
`tracking-db.json` only contains URLs that have been actively processed by the SEO workflow.
A false positive (blocking a valid opportunity) would require a URL to have been incorrectly
set to BRIEF_CREATED in tracking-db, which is a separate data-quality issue that should be
surfaced (the log line will do this). The change does not touch any data files — only the
spec for how T5 filters.

## Rollback

Remove the bold cross-reference guard sentence from the Step 2 filter line. T5 reverts to
filtering on `new-content-opportunities.json` status only — BRIEF-COLLISION-GATE-01 risk
returns but no data is corrupted.

## Veto instructions

To veto: rename to `t5-brief-created-precheck-20261101T2030.vetoed.md`.
To approve early: rename to `t5-brief-created-precheck-20261101T2030.approved.md`.
