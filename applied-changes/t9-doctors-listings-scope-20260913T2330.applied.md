# Proposal: T9 Auto-Ship — recognise `src/content/doctors-listings/` (renders at `/doctors/<slug>`) as a shippable content dir
**Proposed:** 2026-09-13T23:30:00+05:30
**Source:** task20-auto-remediation-2026-09-13 (companion to `t9-doctors-cluster-cap-separation-20260906T2030`; Verifier CORRECTION applied)
**Apply on:** 2026-09-20T20:30:00+05:30 (auto-apply by Strategist if not vetoed)
**Status:** preview

## Issue detected

B23 asked Kushal to confirm whether T9's cluster cap is enforced in spec text or in `scripts/*.py`. T20 verified it
2026-09-13 (Verifier APPROVE): **spec text** — `grep -rn -i "cluster.cap\|cluster_cap\|per_cluster" scripts/*.py` = 0 hits;
`cowork-tasks/task9-auto-ship-new-blogs.md:160` tells Claude to count `tracking-db.json` rows with `published_at > window_start`;
the cap table is `brain/VERIFIER.md §9` (lines 131–140). So the 09-06 cap-separation proposal is applicable.

**But the cap bucket is not what blocks the 14 Tier A `/doctors/` briefs.** All 14 carry
`Suggested File: src/content/doctors-listings/<slug>.mdx`. Ground truth from the website repo (GitHub tree, `main` @ d5b6443):
- `src/content/doctors-listings/` holds **281 listing MDX** files (e.g. `adhd-specialists-in-bangalore.mdx`); `src/content/doctors/` holds 62 doctor *profiles* and zero listings.
- `src/app/doctors/[slug]/page.tsx:38` — `generateStaticParams()` includes `getCollection("doctors-listings")`; line 89/132 `getFile("doctors-listings/${slug}")`. **A listing MDX renders at `/doctors/<slug>` with no code change.** `/doctors-listings/<slug>` as a URL is dead; as a content dir it is the live source.
- Listing frontmatter contract: `title`, `description`, `filterCity|filterRole|filterLanguage|filterCondition|filterTherapy|filterArea|filterAgeGroup` (null when unused), `uniqueIntro`, `seo.metaTitle`, `seo.metaDescription`, then markdown body with H2s + `## Frequently Asked Questions` H3s. `getDoctorsForListing(filter)` fills the grid from the 62 profiles — **a filter that matches 0 profiles renders an empty page** (Bhojpuri brief archived 2026-09-13 for exactly this).
- `src/content/doctors-listings/README.md` (truthfulness rule): Chennai · Coimbatore · Hyderabad · Visakhapatnam centres are NOT open → online-only framing; the same must hold for Kolkata / Mumbai / Delhi / Pune briefs (no centre) — never "visit our <city> centre".

T9 Step 1 (spec lines 74 and 85–86) only recognises `blogs|treatments|illnesses`, defaults everything else to `/blogs/`, and its
`existing` scan skips `doctors-listings/` → (i) every `/doctors/` brief is mislabelled `/blogs/` and cap-blocked
(`logs/auto-ship-2026-09-11.txt`: `NEW-anxiety-therapists-in-kolkata-brief.md → /blogs/`), (ii) an already-shipped listing brief would
look "unshipped" — double-publish risk. `scripts/audit-unshipped-briefs.py:21` (`CATEGORIES = ["blogs","illnesses","treatments"]`)
and `:61` (`expected /blogs/{slug}`) have the identical gap, and that script runs FIRST (the inline python is only the `||` fallback).
Also: task9 line 96 "secondary check for stuck out-of-scope briefs (added 2026-08-23)" has an empty body.

## Proposed change
**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task9-auto-ship-new-blogs.md`
**Edit type:** sed-replace (two hunks, Step 1 inline python)

### Before
```
for dir_name in ['blogs', 'treatments', 'illnesses']:
```
### After
```
for dir_name in ['blogs', 'treatments', 'illnesses', 'doctors-listings']:
```

### Before
```
    m = re.search(r'\*\*Suggested File:\*\*\s+src/content/(blogs|treatments|illnesses)/[\w-]+\.mdx', text)
    target_dir = m.group(1) if m else 'blogs'
```
### After
```
    m = re.search(r'\*\*Suggested File:\*\*\s+src/content/(blogs|treatments|illnesses|doctors-listings)/[\w-]+\.mdx', text)
    target_dir = m.group(1) if m else 'blogs'
    # doctors-listings MDX renders at /doctors/<slug> (src/app/doctors/[slug]/page.tsx) — label + cap-bucket it as /doctors/
    url_prefix = '/doctors/' if target_dir == 'doctors-listings' else f'/{target_dir}/'
```
(and in the print line use `{url_prefix}{slug}` instead of `/{target_dir}/{slug}`)

**Plus, Step 2 — a new hard gate for `doctors-listings` candidates (append after rule 6):**
```
7. **Listing viability gate (`/doctors/` only, added 2026-09-20):** before writing a `src/content/doctors-listings/*.mdx`,
   resolve the brief's filter (language / condition / role / therapy / city) against `src/content/doctors/*.mdx` frontmatter and
   require **≥1 matching live profile** (`/doctors/<profile-slug>` 200, no -L). 0 matches → SKIP, append a T9 rejection block
   ("§listing-viability: 0 profiles match filterLanguage=X"), do NOT ship. Cities without an open centre (README in that dir:
   Chennai, Coimbatore, Hyderabad, Visakhapatnam — and any city not in the OPEN table, e.g. Kolkata/Mumbai/Delhi/Pune) must use the
   online-only phrasing from the README; a brief that says "visit our <city> centre" fails Verifier §5.
   Cap bucket: `/doctors/` = 6 per 7-day window (its own counter, never shared with `/blogs/`) — add the row to VERIFIER.md §9.
```

## Companion items (NOT applied by this proposal — out of Strategist/T20 remit)
- **`scripts/audit-unshipped-briefs.py`** (code — dev / Strategist-Verifier): line 21 `CATEGORIES = ["blogs", "illnesses", "treatments", "doctors-listings"]`;
  line 61 print the resolved prefix (`/doctors/` for doctors-listings) instead of the hard-coded `/blogs/`. Until this lands, T9's
  primary path keeps mislabelling; the spec fix above only governs the fallback branch and the human-readable log.
- **`brain/VERIFIER.md §9`** table: add `| /doctors/* | 6 | Tier A listing pages; own counter, separate from /blogs/ (2026-09-20) |`.
- The 09-06 proposal's After-block must be applied with `/treatments/ 7` and `/illnesses/ 5` (VERIFIER §9), not 3/3, and its
  sed anchor (`/blogs/ at 3/3`, line 175) lands in the rejection *template* — put the CLUSTER CAP RULE under Step 2 rule 5 instead.

## Rationale
14 Tier A `/doctors/` briefs (all verified 404 on 2026-09-13, none has a listing MDX yet) are content-only ships worth
+200–500 clicks/wk by T10's estimate. Nothing about them needs Kushal: the cap question is answered, the render path is verified,
and the only human-adjacent item is a one-line script edit that the Strategist Verifier owns. Three Punjabi briefs ride on a
1-profile roster (thin but precedent-consistent — Odia/Urdu listings live at 1); the viability gate makes that explicit at ship time.

## Risk assessment
Low. The gate is additive; `/blogs/` behaviour is unchanged. Empty-listing risk is closed by rule 7. The truthfulness rule is
already the repo's own README. Rollback = revert the two hunks and delete rule 7.

## Rollback
Before-snapshot to be taken by T10 at apply time (`brain/before-snapshots/task9-auto-ship-new-blogs-<ts>.bak`).
