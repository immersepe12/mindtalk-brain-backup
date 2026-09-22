# Proposal: task5 — remove dead /doctors-listings/ route claim
**Proposed:** 2026-09-13T20:30:00+05:30
**Source:** task13-meta-learner-2026-09-13
**Apply on:** 2026-09-20T20:30:00+05:30
**Status:** preview

## Issue detected

`task5-new-content-discovery.md` line 43 states: *"200+ doctor listing pages → /doctors-listings/ (local SEO hubs)"*. This is a dead route. T20 Auto-Remediation (2026-09-12) archived 14 `/doctors-listings/` briefs that T5 had generated for this prefix, noting: *"task5 spec line 43 names a dead route — T13 item."* The actual live URL prefix for doctor listing hubs is `/doctors/` (e.g. `/doctors/psychiatrists-in-bangalore`).

Because T5 still names `/doctors-listings/` as a valid content target, every future discovery run may generate briefs for this dead path. T9 then has to skip them (or they sit in queue consuming brief capacity), introducing recurring waste. The 14 archived briefs represent weeks of dead queue capacity.

**Evidence:**
- `brain/BRAIN.md` 2026-09-12 T20: *"14 redundant /doctors-listings/ briefs archived (task5 spec line 43 names a dead route — T13)."*
- `cowork-tasks/task5-new-content-discovery.md:43`: `200+ doctor listing pages → /doctors-listings/ (local SEO hubs)`
- `config.json` tracked_specialty_listings: all entries use `/doctors/` prefix (e.g. `"doctors/psychiatrists-in-bangalore"`), zero `/doctors-listings/` entries.
- `cowork-tasks/task6-weekly-report.md:42`: `dead_prefixes = ['/doctors-listings/']` — T6 itself classifies this as dead.

## Proposed change
**File to edit:** `cowork-tasks/task5-new-content-discovery.md`
**Edit type:** line-edit

### Before
```
- 200+ doctor listing pages → /doctors-listings/ (local SEO hubs)
```

### After
```
- 200+ doctor listing pages → /doctors/ (local SEO hubs — e.g. /doctors/psychiatrists-in-bangalore; /doctors-listings/ is a dead route, do NOT generate briefs for that prefix)
```

## Rationale

Correcting the URL prefix prevents T5 from generating dead-route briefs in future runs. The added parenthetical explicitly marks `/doctors-listings/` as forbidden so any future model reading the spec is unambiguous. Zero production code touched.

## Risk assessment

Low. This is a documentation correction in a task spec file. The only downstream effect is that T5 will stop targeting the dead prefix — exactly the intended behaviour. No existing live pages are affected.

## Rollback

Before-state is the current line 43 content: `- 200+ doctor listing pages → /doctors-listings/ (local SEO hubs)`. Revert by restoring that line. No snapshot file required — git history of `cowork-tasks/task5-new-content-discovery.md` preserves the original.
