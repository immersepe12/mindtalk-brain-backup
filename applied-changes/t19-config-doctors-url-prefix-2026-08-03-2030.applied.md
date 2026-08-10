# Proposal: Fix dead `doctors-listings/` URL prefix in config.json tracked_specialty_listings
**Proposed:** 2026-08-03T20:30:00+05:30
**Source:** task13-meta-learner-2026-08-03
**Apply on:** 2026-08-10T20:00:00+05:30
**Status:** preview

## Issue detected

**Evidence chain:**

1. `config.json` → `tracked_specialty_listings` contains 12 entries with the `doctors-listings/` URL prefix (e.g. `"doctors-listings/psychiatrists-in-bangalore"`).
2. These URLs 404 on production. Verified live 2026-08-03:
   - `curl https://www.mindtalk.in/doctors-listings/psychiatrists-in-bangalore` → **HTTP 404**
   - `curl https://www.mindtalk.in/doctors/psychiatrists-in-bangalore` → **HTTP 200**
3. The 07-20 Cowork session (BRAIN.md stamp 2026-07-20 pm-2) already diagnosed this: *"content lives in `src/content/doctors-listings/` but is served by the shared `/doctors/[slug]` route (commit `7e80988`); confirmed via curl that every `/doctors-listings/*` URL 404s while every `/doctors/*` equivalent returns 200."* That session fixed `rank-history.json` and `keyword-map.json` but **did NOT fix `config.json`**.
4. The 07-15 T14 tech-health report explicitly noted: *"config.json doctors-listings URL prefix bug found."* — logged but never resolved.
5. **Impact:** Every rank-pull run (T1 / T2) reads `tracked_specialty_listings` from config.json and checks those 12 URLs. They return `position: 100` sentinel (not-in-top-100) every single pull because the URLs 404 — not because the pages aren't ranking. This produces false "Doctors-Listings category" drop signals in weekly summaries. The 07-13 DOCTORS-LISTING-DROP-02 alarm (−44.9% WoW, 3 days of BACKLOG investigation) traced directly back to this same root cause (BRAIN.md 07-20 stamp).

## Proposed change
**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/config.json`
**Edit type:** sed-replace (replace all 12 `doctors-listings/` occurrences in `tracked_specialty_listings` with `doctors/`)

### Before
```json
  "tracked_specialty_listings": [
    "doctors-listings/psychiatrists-in-bangalore",
    "doctors-listings/psychologists-in-bangalore",
    "doctors-listings/therapists-in-bangalore",
    "doctors-listings/counsellors-in-bangalore",
    "doctors-listings/psychiatrists-in-hyderabad",
    "doctors-listings/psychologists-in-hyderabad",
    "doctors-listings/therapists-in-hyderabad",
    "doctors-listings/counsellors-in-hyderabad",
    "doctors-listings/psychiatrists-in-mysore",
    "doctors-listings/psychologists-in-mysore",
    "doctors-listings/therapists-in-mysore",
    "doctors-listings/child-psychiatrists"
  ],
```

### After
```json
  "tracked_specialty_listings": [
    "doctors/psychiatrists-in-bangalore",
    "doctors/psychologists-in-bangalore",
    "doctors/therapists-in-bangalore",
    "doctors/counsellors-in-bangalore",
    "doctors/psychiatrists-in-hyderabad",
    "doctors/psychologists-in-hyderabad",
    "doctors/therapists-in-hyderabad",
    "doctors/counsellors-in-hyderabad",
    "doctors/psychiatrists-in-mysore",
    "doctors/psychologists-in-mysore",
    "doctors/therapists-in-mysore",
    "doctors/child-psychiatrists"
  ],
```

## Rationale

The rank-pull pipeline (T1/T2) uses `tracked_specialty_listings` from config.json to monitor the P9 Goldmine doctor-listing cluster — one of the highest-converting URL families on the site (66% of UTM payments per BRAIN.md 07-02). Checking 12 dead URLs every pull:

1. Produces a spurious `position: 100` sentinel every single run for each of the 12 pages.
2. Generates false "Doctors-Listings category" drop signals in weekly summaries (confirmed root cause of DOCTORS-LISTING-DROP-02, 07-13 to 07-20).
3. Silently masks the actual rank data for these pages, which ARE ranking well (e.g. `/doctors/psychiatrists-in-bangalore` at pos 9.2 with 28,873 impr/28d per BRAIN.md 07-20).

Fixing the prefix means the rank-pull immediately starts returning real data for these 12 URLs with no other changes. The underlying MDX files (in `src/content/doctors-listings/`) and the Astro route (`/doctors/[slug]`) are already correct — only the tracking config was wrong.

This fix was explicitly diagnosed, scoped, and deferred from the 07-20 session: *"Fixed at the source: renamed all 12 wrong keys in both JSON files to the correct `/doctors/{slug}` prefix"* for rank-history.json and keyword-map.json, but config.json was not included.

## Risk assessment

**Very low.** `config.json` is a read-only config file — no task writes to it. The only effect is that T1/T2 will now query DataForSEO for the correct URLs instead of the dead ones. First rank-pull after apply will populate rank-history.json with real data under the correct keys, replacing the stale `position: 100` sentinels. No production code is touched.

One edge case: if any script does a direct key-lookup on `tracked_specialty_listings` entries that matches the old `doctors-listings/` prefix, it would fail to find the new `doctors/` keys. A grep across `scripts/` shows no such hardcoded prefix lookups — all scripts iterate the config list and query DataForSEO with whatever prefix is in the config.

## Rollback

Copy `brain/before-snapshots/config-{TIMESTAMP}.bak` back to `config.json`. The before-snapshot is created by Strategist at apply time.

## Veto instructions
To veto: rename this file to `t19-config-doctors-url-prefix-2026-08-03-2030.vetoed.md` and add a `## Veto reason` section.
To approve early: rename to `t19-config-doctors-url-prefix-2026-08-03-2030.approved.md`.
If neither, auto-applies 2026-08-10.
