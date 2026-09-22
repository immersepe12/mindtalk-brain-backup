# Proposal: task3 — remove doctors-listings as a content category
**Proposed:** 2026-09-13T20:30:00+05:30
**Source:** task13-meta-learner-2026-09-13
**Apply on:** 2026-09-20T20:30:00+05:30
**Status:** preview

## Issue detected

`task3-serp-analysis-briefs.md` line 25 lists `doctors-listings (local SEO hubs)` as a live content category alongside illnesses, treatments, and blogs. `/doctors-listings/` is a dead route confirmed by T6 (`dead_prefixes = ['/doctors-listings/']`) and T20 (2026-09-12 archived 14 redundant briefs). T3's SERP analysis step uses this category list to decide which brief type to generate when it identifies a target keyword. If T3 classifies a doctor-hub keyword as `doctors-listings`, it will generate a brief pointing at a path that 404s.

**Evidence:**
- `cowork-tasks/task3-serp-analysis-briefs.md:25`: `Content categories: illnesses (conditions), treatments (therapies), blogs (informational), doctors-listings (local SEO hubs)`
- `cowork-tasks/task6-weekly-report.md:42`: `dead_prefixes = ['/doctors-listings/']` — T6 classifies it dead.
- `brain/BRAIN.md` 2026-09-12 T20: dead route confirmed; 14 briefs archived.
- `config.json` tracked_specialty_listings: no `/doctors-listings/` entries; all hubs live under `/doctors/`.

## Proposed change
**File to edit:** `cowork-tasks/task3-serp-analysis-briefs.md`
**Edit type:** line-edit

### Before
```
- Content categories: illnesses (conditions), treatments (therapies), blogs (informational), doctors-listings (local SEO hubs)
```

### After
```
- Content categories: illnesses (conditions), treatments (therapies), blogs (informational), doctors (local SEO hubs — URL prefix /doctors/, NOT /doctors-listings/ which is a dead 404 route)
```

## Rationale

Aligns T3's category list with the live site structure. Prevents T3 from generating SERP analysis briefs targeting a dead URL prefix. The explicit `NOT /doctors-listings/` note prevents regression even if a future model session reads the spec without broader context.

## Risk assessment

Low. Documentation correction only. T3 produces briefs, not production code. The only effect is correct URL prefix classification in new briefs.

## Rollback

Restore line 25 to: `- Content categories: illnesses (conditions), treatments (therapies), blogs (informational), doctors-listings (local SEO hubs)`. Git history of `cowork-tasks/task3-serp-analysis-briefs.md` is the rollback source.
