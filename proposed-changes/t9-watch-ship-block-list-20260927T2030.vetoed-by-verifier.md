# Proposal: t9-watch-ship-block-list

**Proposal-ID:** t9-watch-ship-block-list-20260927T2030
**Raised-by:** T13-Meta-Learner
**Issue-category:** Missing gate / thin-content risk
**Raised-on:** 2026-09-27
**Apply-on:** 2026-10-04T20:00:00+05:30
**Affects-task:** T9 (auto-ship-new-blogs)
**Priority:** MEDIUM
**Rollback:** Remove the "Watch block-list check" paragraph appended to Step 2 Rule 7 in task9-auto-ship-new-blogs.md. Delete `brain/ship-block-list.json`.

---

## Issue

T20 tagged `WATCH-CANNOT-REACH-SHIP-GATE-01` on 2026-09-25: "T9 listing viability gate (Step 2 Rule 7) runs profile-count check but never reads WATCH.md. No machine-readable block mechanism exists. WATCH rows are human-readable prose — T9 cannot parse them."

When T20 or any task identifies a listing family as thin or risky (e.g. `W-PUNJABI-BLR-THIN-0925` — 1 professional, shipped before full WATCH review), the only safeguard is a human reading WATCH.md before T9 fires. T9 has no automated path to honor WATCH entries for `/doctors/` listing slugs. This creates a gap where thin listings can be re-shipped in subsequent runs.

---

## Proposed Change

**Files:**
1. `cowork-tasks/task9-auto-ship-new-blogs.md` — append to Step 2 Rule 7
2. `brain/ship-block-list.json` — CREATE new file (initial entry for punjabi-speaking block)

### Change 1: task9-auto-ship-new-blogs.md

**Action:** Append watch-block-list paragraph to Step 2 Rule 7, immediately after the existing Rule 7 text.

#### Before (end of Rule 7):

```
7. **Listing viability gate (`/doctors/` only, added 2026-09-20):** before writing a `src/content/doctors-listings/*.mdx`, resolve the brief's filter against `src/content/doctors/*.mdx` frontmatter and require **≥1 matching live profile** (`/doctors/<profile-slug>` 200, no -L). 0 matches → SKIP. Cities without open centre must use online-only phrasing. Cap bucket: `/doctors/` = 6 per 7-day window (its own counter, never shared with `/blogs/`).
```

#### After (same text + block-list paragraph):

```
7. **Listing viability gate (`/doctors/` only, added 2026-09-20):** before writing a `src/content/doctors-listings/*.mdx`, resolve the brief's filter against `src/content/doctors/*.mdx` frontmatter and require **≥1 matching live profile** (`/doctors/<profile-slug>` 200, no -L). 0 matches → SKIP. Cities without open centre must use online-only phrasing. Cap bucket: `/doctors/` = 6 per 7-day window (its own counter, never shared with `/blogs/`).

   **Watch block-list check (added 2026-09-27):** after the profile-count check, read `brain/ship-block-list.json` (JSON array of `{"slug_prefix": "…", "block_until": "YYYY-MM-DD", "reason": "…"}` objects). If any entry's `slug_prefix` is a prefix of this brief's target slug AND `block_until` >= today → SKIP and log `"WATCH-BLOCKED: {target_slug} matches block entry {slug_prefix} until {block_until} ({reason})"`. Any task or T20 can write entries here to block thin/problematic listing families without touching task specs. Strategist's daily run removes entries whose `block_until` has passed.
```

### Change 2: brain/ship-block-list.json (CREATE)

```json
[
  {
    "slug_prefix": "doctors/punjabi-speaking",
    "block_until": "2026-10-25",
    "reason": "W-PUNJABI-BLR-THIN-0925: thin listing (1 professional) shipped before WATCH checkpoint; block all punjabi-speaking until review 2026-10-25"
  }
]
```

---

## Filters

- **Forbidden-path check:** PASS — `cowork-tasks/task9-auto-ship-new-blogs.md` and `brain/ship-block-list.json` are allowed paths
- **Anti-pattern check:** PASS — no AP conflicts; this adds a gate that prevents thin content (consistent with AP11 spirit)
- **Duplicate check:** PASS — the Step 2 Rule 7 listing viability gate was applied 2026-09-20; this proposal extends it with a separate block-list mechanism. Different mechanism, no 30-day duplicate conflict.
- **INTENT-PRIORITY.md protection:** PASS — not related to intent classification or Tier gates

## Rollback Path

1. Remove the "Watch block-list check" paragraph from `cowork-tasks/task9-auto-ship-new-blogs.md` Step 2 Rule 7.
2. Delete `brain/ship-block-list.json`.
No tracking-db or content changes required.
