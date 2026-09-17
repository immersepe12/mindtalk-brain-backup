# ship_REFRESH_brief (defect fix) on /doctors/child-psychologists-in-bangalore — 2026-09-16

## What we did
Changed `filterAgeGroup: "Child"` → `filterAgeGroup: "Children"` in frontmatter of `src/content/doctors-listings/child-psychologists-in-bangalore.mdx`.

This is a one-word defect fix. The page was shipped 2026-09-15 (commit 0001be1) but rendered 0 clinicians because `src/lib/doctors.ts` does exact-match on `agePreferrence`, and the roster value is `"Children"` (32 profiles), not `"Child"` (0 profiles). Changing to `"Children"` with Bangalore + Psychologist filters matches 18 professionals.

## Commits
- Feature branch: `feat/exec-CHILD-PSYCH-BLR-EMPTY-01-2026-09-16`
- Commit on branch: `bfcdb0390799c5808eb6e9c46a3d50c1ab6ecac0`
- Merge commit to main: `a7a4c08aca22e4d392a378f4dfec93a2c3275a48`
- Method: GitHub Contents API (FUSE local checkout blocked — WEBSITE-CHECKOUT-CORRUPT-01)

## Verification
- GitHub tree confirmed: `filterAgeGroup: "Children"` on main ✓
- Vercel deploy triggered by Vercel's GitHub integration (auto-deploy on push to main)
- Live curl check: pending Vercel deploy (~3 min). Expected: "Showing 18 professionals" on the page.

## Expected outcome
Page goes from 0 → 18 clinicians shown. Tier A (1,200/mo keyword). 42-day observation window opens from today. Check 2026-10-28.

## Watch
CHILD-PSYCH-BLR-EMPTY-01 defect window: 2026-10-28 check (not a ranking watch, but indexation + clinician display check).

## Notes
Verifier sub-agent APPROVED. BACKLOG row marked COMPLETE 2026-09-16.
