# Proposal: T9 — Add tracking-db cross-check to audit-unshipped-briefs (Step 1 guard)

**Proposed:** 2026-11-08T14:41:00+05:30
**Source:** META-LEARNER T13 weekly run 2026-11-08T1441 (issue: T9-PULL-COMPLETENESS-01)
**Apply on:** 2026-11-15T14:41:00+05:30
**Status:** preview
**Target file:** `cowork-tasks/task9-auto-ship-new-blogs.md`
**Human-review-only:** ❌ (task-spec only; `scripts/audit-unshipped-briefs.py` marked human-review-only separately)

---

## Issue detected

**BACKLOG entry T9-PULL-COMPLETENESS-01 (verbatim):**
> This run's first `gh_ship.py pull src/content` timed out at 170s and left a partial local mirror; a naive unshipped-briefs comparison against it incorrectly flagged 5 already-merged slugs (from PR #52/#53, merged to main earlier today) as unshipped. Caught and corrected before anything was built, by re-pulling and cross-checking directly against the GitHub Pulls API. Recommend T13/T20 add a completeness check (e.g. compare local file count per content-type dir against the GitHub Contents API count) to `scripts/audit-unshipped-briefs.py` / `gh_ship.py pull`, so a future run under time pressure can't silently re-ship an already-merged page.

**Root cause:** T9 Step 1's `audit-unshipped-briefs.py` compares brief slugs against the local `src/content` file tree only. If the initial `gh_ship.py pull` times out or is partial, slugs already merged to `main` (and therefore present in `tracking-db.json` with status `PUBLISHED` or `AUTHORED_PENDING_VERIFY`) appear absent from the local tree and are incorrectly treated as unshipped candidates.

**Risk:** Without this guard, a time-pressure run following a partial pull could ship a duplicate page (re-opening a PR for a slug already in production), creating duplicate-content issues and wasted T9 budget.

---

## Proposed change

**Target:** `cowork-tasks/task9-auto-ship-new-blogs.md` — Step 1, Safety-filter block

### Edit 1 — Add tracking-db cross-check instruction to Step 1 safety filters

**Before (Step 1 safety filter list, item 7):**
```
7. Skip any brief whose slug already exists in `src/content/[type]/` tree.
```

**After:**
```
7. Skip any brief whose slug already exists in `src/content/[type]/` tree.
8. COMPLETENESS-GUARD: Before treating a brief slug as an unshipped candidate,
   cross-check `tracking-db.json` for that slug's status. If found with status
   `PUBLISHED` or `AUTHORED_PENDING_VERIFY`, skip it and log:
     COMPLETENESS-GUARD: skip [slug] (tracking-db status=PUBLISHED)
   This prevents a partial `gh_ship.py pull` (timeout, interrupted sync) from
   silently re-shipping an already-merged page. The script-level implementation
   of this check is marked human-review-only (see scripts/audit-unshipped-briefs.py).
```

**Note:** The corresponding script-level code change in `scripts/audit-unshipped-briefs.py` is `human-review-only` and must be implemented by a human developer after this task-spec proposal is applied.

---

## Why this is safe

- Read-only change to task spec; no production code altered.
- Adds a defensive skip, never removes candidates — worst case is a false-positive skip on a genuinely unshipped brief whose tracking-db entry was incorrectly set to PUBLISHED (recoverable: human can clear the tracking-db entry and re-run T9).
- The 5-slug incident on 2026-11-08 is real evidence; this guard would have caught it at the task-spec level even before the script fix.

---

## Rollback path

If the COMPLETENESS-GUARD causes false-positive skips:
1. Remove filter item 8 from T9 Step 1 (single-line revert to this proposal file).
2. Strategist applies rollback at next 8 PM run.
3. Human developer audits tracking-db.json for incorrect PUBLISHED entries.

---

## Diff summary

```diff
 cowork-tasks/task9-auto-ship-new-blogs.md
 Step 1 safety filters:
 
-  7. Skip any brief whose slug already exists in `src/content/[type]/` tree.
+  7. Skip any brief whose slug already exists in `src/content/[type]/` tree.
+  8. COMPLETENESS-GUARD: cross-check tracking-db.json for slug status;
+     skip if PUBLISHED or AUTHORED_PENDING_VERIFY; log the skip.
```
