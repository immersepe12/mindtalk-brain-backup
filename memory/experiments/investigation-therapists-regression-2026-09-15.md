# investigate_regression — therapists-in-bangalore + therapists-in-hyderabad — 2026-09-15

## BACKLOG source
B8 — RE-SCOPED by T20 2026-09-12 (Verifier reversed T20's own false-positive closure). Verified REAL regression at query level. Priority: IMMEDIATE.

## What we looked at

- `src/content/doctors-listings/therapists-in-bangalore.mdx` — confirmed path
- `src/content/doctors-listings/therapists-in-hyderabad.mdx` — confirmed path
- Git log for both files
- GSC cache files (stale — pulled 2026-06-30, using wrong /doctors-listings/ URL path)
- de29c86 batch commit (2026-08-31): 52 new doctor-listing pages including 10+ therapist variants
- BACKLOG B8 evidence from T20 2026-09-12 (query-level GSC pull)

## Actual signal (from T20 verified evidence)

Query: **"therapist near me"** (commercial Tier A, 60.5K/mo, INTENT-PRIORITY §5 pos 8–11 cliff)

| Page | Pos (baseline) | Pos (2026-09-09) | Impr trend | Clicks/wk |
|------|----------------|-------------------|------------|-----------|
| /doctors/therapists-in-bangalore | 9.3 | 16.2 | 856→1,167 impr (+36%) | 7→4 (-43%) |
| /doctors/therapists-in-hyderabad | 10.1 | 49.5 | 294→205 impr (-30%) | CRASH |

Secondary signals (90d, query-level):
- "counselling psychologist near me": 1,100 impr / pos 22.5
- "talk therapy": 1,363 impr / pos 28.4
- Property-level pos for "therapist near me": 11.9 → 27.0 (impr-weighted)

## Root causes

### 1. Mix dilution from de29c86 (2026-08-31) — PRIMARY CAUSE

The batch shipped **10+ new therapist listing pages** all competing for overlapping "therapist" queries:
- therapists-in-chennai, therapists-in-delhi, therapists-in-kolkata, therapists-in-mumbai, therapists-in-pune
- online-therapists-india
- couple-therapists-in-bangalore
- anxiety-therapists-in-delhi, ocd-therapists-in-delhi
- therapists-for-anxiety-and-depression

**Total therapist listing pages now in index: ~13** (2 original + therapists-in-mysore + 10 new)

Google sees 13 Mindtalk therapist listing pages and struggles to canonically resolve which serves "therapist near me." The primary /doctors/therapists-in-bangalore page (original Tier A) is now competing with 12 siblings for domain's therapist-query budget. Internal signals are diluted.

Key aggravating factor: `couple-therapists-in-bangalore` directly competes on Bangalore + therapist intent and may be siphoning Bangalore local signals specifically.

### 2. Hyderabad thin content — SECONDARY CAUSE for Hyderabad crash

The therapists-in-hyderabad MDX has `filterCity: "Hyderabad"` but the Cadabams/Mindtalk clinician database shows **only 2 clinicians in Hyderabad** (per de29c86 commit note: "Bangalore 44, Mysore 13, Hyderabad 2"). The page renders a listing of 2 professionals while claiming "expert therapist services." Google is likely downranking it as thin or misleading local content (pos 10.1 → 49.5 = 5 pages down = severe algorithmic demotion).

### 3. Content depth gap — TERTIARY CAUSE for both pages

Both MDX files lack:
- `faqs:` frontmatter block (only body H3 FAQs — no FAQPage JSON-LD schema)
- `quickAnswer` / `keyTakeaways` fields (zero SERP feature signals)
- Reviewer assigned (no `reviewedBy` JSON-LD on doctor listing pages — distinct from illness pages)
- Differentiation language: content is near-identical between all city variants

The de29c86 siblings have the same thin content structure, further reducing each page's differentiating value.

## What is NOT the root cause

- **Algorithm penalty**: ALGO_WATCH cleared 2026-09-10 with no YMYL drops. The regression is too granular and specific to the therapist cluster to be a site-wide update.
- **Technical issues**: Pages return 200 (confirmed). The `/doctors/` route is a programmatic React page.tsx reading doctors-listings collection — confirmed functional.
- **Deindexation**: Impressions still rising on therapists-in-bangalore (856→1,167) — not deindexed, just position-diluted.

## Git history

- therapists-in-bangalore.mdx: last modified **2026-04-14** (phone number fix) — 154 days ago, **AP4 CLEAR**
- therapists-in-hyderabad.mdx: last modified **2026-04-14** — 154 days ago, **AP4 CLEAR**
- de29c86 (2026-08-31): 52 new listing pages shipped — timing aligns with regression onset

## Recommended actions

### B8-BLR: ship_REFRESH_brief — therapists-in-bangalore (MEDIUM priority)

**Action:** Create and ship a refresh brief for therapists-in-bangalore.mdx targeting:
- Add `faqs:` frontmatter (5 Q&As targeting: "what does a therapist do in Bangalore", "how much does therapy cost in Bangalore", "best therapist near me Bangalore", "how to book a therapist", "online vs in-person therapy Bangalore")
- Add `quickAnswer:` frontmatter ("Find experienced therapists in Bangalore at Mindtalk's 4 centres — Indiranagar, Sarjapura, Kanakapura Road, Kalyan Nagar. Book in-person or online sessions from ₹1,000.")
- Add `keyTakeaways:` frontmatter (5 bullets: 4 Bangalore centres, 44+ therapists, evidence-based modalities, booking options, fee range)
- Differentiate from siblings: add Bangalore-specific H2 ("Therapy at Mindtalk's 4 Bangalore Centres") with centre names + availability; add comparison table (in-person vs online)
- AP4 CLEAR (154 days). No clinical sign-off needed (doctor listing page, not YMYL illness/treatment).
- Assign reviewer: `dr-sneha` (load 3, available)
- Expected: restore therapists-in-bangalore to pos 9–11 within 21d, +30–80 clicks/wk

### B8-HYD: flag_for_human — therapists-in-hyderabad (URGENT)

**Action:** Kushal decision required on Hyderabad strategy:
- **Option A — Redirect:** 301 therapists-in-hyderabad → /doctors/online-therapists-india (online therapy remains real capability even without physical Hyderabad centres)
- **Option B — Reframe:** Edit MDX to be explicitly an "Online Therapists Serving Hyderabad" page; remove claims of in-person service; change `filterCity: null` to show all online-capable therapists; update title to "Online Therapists for Hyderabad | Book a Video Session | Mindtalk"
- **Option C — Hold:** Keep current content, monitor if pos recovers post-algorithm update. Low probability — the thin-listing root cause is structural.

**Recommendation: Option B** (lowest dev effort, honest to actual capability, recovers local intent signal for Hyderabad patients seeking online therapy).

### B8-SIBLING: monitor — 10 new therapist listing pages (WATCH 14d)

Watch the de29c86 batch therapist pages for 14 days (check 2026-09-29):
- Do they collectively rank for "therapist near me" variants?
- Does the Bangalore primary page recover once Hyderabad's thin-content issue is resolved?
- If 3+ siblings all rank at pos 40–70 for "therapist near me" variants and none produce clicks → consider canonical consolidation (all → therapists-in-bangalore as canonical)

## Watch window

- **B8-BLR** (refresh): once brief written and shipped → W-B8-BLR opens, check Day-14 + Day-42
- **B8-SIBLING** (monitor): 14d → check 2026-09-29

## Notes

GSC cache files for both pages were pulled with wrong URL path (`/doctors-listings/therapists-in-bangalore` instead of `/doctors/therapists-in-bangalore`). All data cited here comes from T20's query-level GSC pull (page-attributed, verified 2026-09-12). Fresh GSC pull needed for tracking.
