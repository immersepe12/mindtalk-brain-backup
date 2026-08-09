# Proposal: Fix T9 stale per-run cap in Constraints + add cluster window boundary cross-reference
**Proposed:** 2026-08-09T20:30:00+05:30
**Source:** task13-meta-learner-2026-08-09
**Apply on:** 2026-08-16T20:00:00+05:30
**Status:** preview

## Issue detected

**Two related issues in `cowork-tasks/task9-auto-ship-new-blogs.md`:**

**Issue A — Stale per-run cap in Constraints (category 1a: cross-task inconsistency)**

The per-run cap was raised from 5 → 7 on 2026-07-03 (see line 26, Step 2 Rule 6). But the Constraints section at the bottom of the file was never updated:
- Line 475: `**5 per run, 20 per week cap.** Hard limit.` ← still says 5
- Line 497: `≤ 5 pages per run` ← still says 5

If an agent reads the Constraints section as authoritative (which it should), it will self-throttle at 5 instead of the actual limit of 7. This costs ~2 pages per run × 3 runs/week = ~6 potential pages/week lost to a stale number.

**Issue B — No cross-reference to VERIFIER.md §9 boundary disambiguation (category 1b: wasted work)**

`brain/VERIFIER.md §9` has a disambiguation note (added 2026-07-24) that explicitly specifies: use `published_at > window_start` (strict `>`, NOT `>=`) when counting cluster pages in the 7-day rolling window. Using `>=` inflates the count by 1 on the rolloff day.

Despite this note existing in VERIFIER.md, T9 runs have produced the `>=` boundary error **3 times** (2026-07-23, 2026-07-24, 2026-07-28). The BRAIN.md 2026-07-28 stamp explicitly flagged this: *"3rd occurrence of this recurring T9 `>=` error; suggest Meta-Learner proposal to fix T9 formula."*

Root cause: T9 agents write the cluster window check Python code on-the-fly and do not consistently read VERIFIER.md §9 before doing so. Adding a boundary reminder directly in T9 Step 2 (where the cap check happens) will surface the correct formula at the moment of action.

## Proposed change

**File to edit:** `cowork-tasks/task9-auto-ship-new-blogs.md`
**Edit type:** line-edit (3 separate locations)

---

### Edit 1 of 3 — Step 2 Rule 5: add cluster window boundary note

### Before
```
5. **Cap check** — count this week's Task 9 shipments (read `logs/auto-ship-week-{WEEK-START}.txt` if exists). If ≥ 20, stop processing and log "Weekly auto-ship cap reached (20/20)".

6. **Per-run cap** — limit to **7 pages per single Task 9 run** (raised from 5 on 2026-07-03 to hit 20/week target). If more candidates remain, leave them for the next run.
```

### After
```
5. **Cap check** — count this week's Task 9 shipments (read `logs/auto-ship-week-{WEEK-START}.txt` if exists). If ≥ 20, stop processing and log "Weekly auto-ship cap reached (20/20)".

   **⚠ Cluster cap boundary (VERIFIER §9):** When counting pages per cluster from `tracking-db.json` for the 7-day rolling window, use strict `>` NOT `>=`: count entries where `published_at > window_start`, where `window_start = TODAY - 7 days`. A page published exactly 7 days ago has rolled OFF the window and must NOT be counted. Using `>=` inflates the count by 1 on the rolloff day — 3rd confirmed recurrence 2026-07-28. See `brain/VERIFIER.md §9` disambiguation note.

6. **Per-run cap** — limit to **7 pages per single Task 9 run** (raised from 5 on 2026-07-03 to hit 20/week target). If more candidates remain, leave them for the next run.
```

---

### Edit 2 of 3 — Constraints: fix stale "5 per run" cap

### Before
```
- **5 per run, 20 per week cap.** Hard limit.
```

### After
```
- **7 per run, 20 per week cap.** Hard limit. (Raised from 5 on 2026-07-03 — matches Step 2 Rule 6.)
```

---

### Edit 3 of 3 — Expected throughput: fix stale "≤ 5 pages per run"

### Before
```
- ≤ 5 pages per run
```

### After
```
- ≤ 7 pages per run
```

---

## Rationale

Issue A: The Constraints section is the most likely place an agent reads to confirm hard limits. A stale "5 per run" here creates a silent throttle — T9 silently caps at 5 thinking it's following the spec. The correct number (7) already exists in the body (line 26, Step 2 Rule 6) but inconsistency means one section always loses.

Issue B: The disambiguation note in VERIFIER.md is correct but agents don't naturally read VERIFIER.md §9 before writing ad-hoc Python cap-check code. Embedding the boundary rule directly in Step 2 (at the point of action) puts it where it's needed. Three recurrences of the same off-by-one error justify hardening the spec text rather than expecting agents to discover a disambiguation section in a different file.

## Risk assessment

Low. These are spec text fixes — no production code, no logic change. If the Strategist applies the wrong "Before" anchor, the apply step will MISMATCH-SKIP and no change will be made (safe failure mode).

## Rollback

Snapshot: this proposal file contains the exact "Before" text for all 3 edits. Revert by re-applying Before→After in reverse (After→Before).
