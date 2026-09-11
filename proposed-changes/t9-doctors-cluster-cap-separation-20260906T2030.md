# Proposal: T9 Auto-Ship — explicit /doctors/ cluster cap separation from /blogs/
**Proposed:** 2026-09-06T20:30:00+05:30
**Source:** task13-meta-learner-2026-09-06
**Apply on:** 2026-09-13T20:30:00+05:30
**Status:** preview

## Issue detected

T20 Auto-Remediation (2026-08-22) confirmed T9-DOCTORS-QUEUE-MISLABEL-01: T9's auto-ship log (`logs/auto-ship-2026-08-21.txt`) called all 49 queued candidates `/blogs/` and cap-blocked them. Only 11 were genuine `/blogs/` — 43 were `/doctors/` Tier A briefs (e.g., `NEW-online-psychiatry-brief.md` with `Suggested URL: /doctors/online-psychiatry` was listed by T9 as `/blogs/online-psychiatry`). T20's note: *"T9 parses path as /blogs/ by default when the Suggested File prefix does not match a tracked category."* The `/blogs/` cluster was at or near cap, so all 43 /doctors/ briefs were silently blocked week after week — this is the concrete root cause of DOCTOR-EXECUTOR-VELOCITY-01 (43 Tier A briefs unshipped as of 2026-08-25, confirmed by T10 Strategist).

Checking `cowork-tasks/task9-auto-ship-new-blogs.md`: Step §9 references `cluster cap: /blogs/` as a unified cap applying to all content by default. There is no explicit separation of `/doctors/` into its own cap bucket.

**Evidence:**
- `logs/auto-ship-2026-08-21.txt`: "calls all 49 queued candidates /blogs/ and cap-blocks them; only 11 are /blogs/ — 43 are /doctors/"
- `brain/BRAIN.md` 2026-08-25 T10: "T9-DOCTORS-QUEUE-MISLABEL-01 — live velocity bug. 43 Tier A /doctors/ briefs verified HTTP 404 by T20 2026-08-22 — genuinely unshipped. Largest single unexploited Q3 play."
- `brain/BACKLOG.md` active: "Largest single unexploited Q3 play" — 43 Tier A briefs blocked.
- `logs/auto-ship-2026-09-04.txt`: same cluster-cap block pattern still firing (CLUSTER_CAP:/blogs/:9/6).

## Proposed change
**File to edit:** `cowork-tasks/task9-auto-ship-new-blogs.md`
**Edit type:** sed-replace

Find the cluster-cap check section (referenced as `§9 cluster cap` in T9's skip-log format). Add explicit path-prefix separation rule immediately before the cap evaluation:

### Before
```
- {failure 3, e.g., §9 cluster cap: /blogs/ at 3/3 — wait until {date}}
```

### After
```
- {failure 3, e.g., §9 cluster cap: /blogs/ at 3/6 — wait until {date}}

**CLUSTER CAP RULE (path-prefix separated):**
Each URL prefix tracks its own 7-day publication cap, independently:
- `/blogs/` cap: 6 pages per 7-day rolling window (config.json max_new_content_per_week ÷ 3 paths, floor 6)
- `/doctors/` cap: 6 pages per 7-day rolling window (separate counter — NEVER shares with /blogs/)
- `/treatments/` cap: 3 pages per 7-day rolling window (YMYL — lower cap)
- `/illnesses/` cap: 3 pages per 7-day rolling window (YMYL — lower cap)

**Path resolution (mandatory before cap check):**
1. Read `Suggested File:` line from brief frontmatter. Extract the path prefix (first segment after `/`).
2. If `Suggested URL:` or `Suggested File:` starts with `/doctors/` → count against `/doctors/` cap only.
3. If no `Suggested File` line AND brief slug appears in `config.json tracked_specialty_listings` → treat as `/doctors/`.
4. If no `Suggested File` AND slug does NOT match tracked_specialty_listings → treat as `/blogs/`.
5. NEVER count a `/doctors/` brief against the `/blogs/` cap. Log the resolved prefix as `[CAP-BUCKET: /doctors/]` in the skip/approve line.
```

## Rationale

43 Tier A /doctors/ briefs have been blocked week over week under a /blogs/ cluster cap they should never have been subject to. The /doctors/ cluster is entirely separate from /blogs/ — it serves commercial intent (booking) queries vs. informational queries. Mixing them under one cap directly contradicts INTENT-PRIORITY.md §1 (Tier A content gets priority). Explicit path-prefix separation in the spec will unblock these briefs on the next T9 run. This is the highest-velocity unlock available in Q3.

## Risk assessment

Medium. If T9 reads this spec update and the cluster-cap logic is implemented in the task spec instructions (rather than a hard-coded script), up to 6 /doctors/ briefs could ship per 7-day window immediately. Risk: if doctor briefs have an underlying quality issue or AP3 conflict, they'll still be caught by the existing per-brief VETO checks (AP3, Verifier §5, etc.). The cap change doesn't bypass any individual brief quality gates — it only changes which cap bucket applies.

Note: if T9's cluster-cap logic is enforced *purely* inside `scripts/*.py` and NOT in the task spec instructions, this proposal is **human-review-only** (Strategist must mark it so when applying). The above edit to the spec's §9 skip-log template is safe regardless.

## Rollback

Before-snapshot: `cowork-tasks/task9-auto-ship-new-blogs.md` §9 cluster cap section as of 2026-09-06. To revert: remove the "CLUSTER CAP RULE" and "Path resolution" blocks added above, restore the single `/blogs/` cap reference.
