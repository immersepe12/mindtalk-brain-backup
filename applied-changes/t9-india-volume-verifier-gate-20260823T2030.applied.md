# Proposal: T9 Verifier — add P12-E3 India search volume gate
**Proposed:** 2026-08-23T20:30:00+05:30
**Source:** task13-meta-learner-2026-08-23
**Apply on:** 2026-08-30T20:00:00+05:30
**Status:** preview

## Issue detected

**P12 exception class E3** ("near-zero India search volume") was codified on 2026-08-03 after W13's failure (`/blogs/how-to-find-a-therapist-for-ocd` — target query returned 0 organic results from DataForSEO India API). The principle states: "Add a minimum India monthly volume gate (≥100/mo) to T5 brief approval."

However, T5 is only the primary brief-generation path. Briefs can also be manually added directly to `briefs/`. The T9 Verifier (Step 3 AP3 gate) is the last safety check before any brief ships — but it has no E3 volume gate. A brief with `india_monthly_volume: 45` would ship without any warning.

Evidence: The `t5-floor-miss-brain-flag-2026-07-26-2030.md` proposal (stale in queue, 28 days) and the W13 post-mortem both point to T5 as the responsible gate, but T9 has no backstop.

## Proposed change
**File to edit:** `cowork-tasks/task9-auto-ship-new-blogs.md`
**Edit type:** line-edit (append a new check 3b after the existing AP3 block)

### Before
```
   - If valid → proceed; this counts as "AP3 satisfied" in the Verifier audit log
   - **Non-YMYL paths skip this check entirely.** Briefs in `/blogs/*` (general content cluster) do not need clinical_reviewer_signed_off — they just need the regular `reviewer` assignment per step 4.
```

### After
```
   - If valid → proceed; this counts as "AP3 satisfied" in the Verifier audit log
   - **Non-YMYL paths skip this check entirely.** Briefs in `/blogs/*` (general content cluster) do not need clinical_reviewer_signed_off — they just need the regular `reviewer` assignment per step 4.

3b. **P12-E3 India search volume gate** — if the brief frontmatter contains `india_monthly_volume:` and its value is < 100, VETO:
   ```
   P12-E3 VETO: india_monthly_volume {N} < 100/mo minimum. Target query has near-zero India search demand. Escalate brief to T5 for re-targeting or archive it.
   ```
   - If `india_monthly_volume:` field is absent, skip this check (assume T5 validated volume during brief generation).
   - If value ≥ 100, proceed.
   - This gate fires on ALL content types (blogs, mindful-minutes, worksheets, journeys) — not YMYL-specific.
```

## Rationale

T9 Verifier is the last pre-ship checkpoint. P12 E3 is a known brief-quality failure that caused a wasted ship (W13). Adding a backstop at T9 means manually-added briefs or briefs that slipped T5's gate get caught before they reach production. The gate is conservative (only fires when field is explicitly set AND <100) — it won't block existing briefs that lack the field.

## Risk assessment

Low. If `india_monthly_volume` is not in the brief frontmatter, the gate doesn't fire. If it IS present and <100, the brief shouldn't ship anyway (P12 E3 explicitly says it fails 80% of the time). The only risk is a false veto if T5 accidentally sets a low value on a valid brief — reviewer can override by bumping the value or removing the field.

## Rollback

Snapshot: `brain/before-snapshots/task9-auto-ship-new-blogs-{TIMESTAMP}.bak` (created at apply time)
To rollback: restore snapshot to `cowork-tasks/task9-auto-ship-new-blogs.md`.
