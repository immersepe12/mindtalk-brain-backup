# Proposal: T5 — Add DOCTOR_LISTING classification branch to Step 4 + fix Step 6 tracking-db key

**Proposed:** 2026-11-08T14:41:00+05:30
**Source:** META-LEARNER T13 weekly run 2026-11-08T1441 (issue: DOCTOR-LISTING-BRIEF-MISFILE-01)
**Apply on:** 2026-11-15T14:41:00+05:30
**Status:** preview

## Issue detected

`brain/BACKLOG.md` flag **DOCTOR-LISTING-BRIEF-MISFILE-01** (added 2026-11-06 by T9) documents that
~90/122 "NEW blog" briefs are doctor/treatment listing content with no `Suggested File` path pointing
to `src/content/doctors-listings/`. Evidence from two sources:

1. **T5 Step 4 has no DOCTOR_LISTING routing branch.** The classification step only defines:
   - `→ BLOG_ARTICLE` (informational, comparison)
   - `→ SPOKE_PAGE under /treatments/` ("[therapy] for [condition]")
   - `→ SPOKE_PAGE under /illnesses/` (condition subtype)

   There is no `→ DOCTOR_LISTING under /doctors/` branch. When keywords like "psychiatrist in mumbai",
   "therapist in bangalore", "psychologist in delhi" (Tier A, 1,500–2,400/mo) are discovered, they
   fall through to `BLOG_ARTICLE` or get misclassified as `TREATMENT_BLOG`. Confirmed via
   `briefs/NEW-psychiatrist-in-mumbai-brief.md`: `content_type: TREATMENT_BLOG`,
   `url_path: /treatments/psychiatrist-in-mumbai` — both wrong; correct is DOCTOR_LISTING,
   `/doctors/psychiatrist-in-mumbai`.

2. **T5 Step 6 tracking-db template hardcodes `/blogs/`.** The template under Step 6 uses:
   ```
   "NEW-/blogs/[slug]": { "url_path": "/blogs/[slug]", "file_path": "src/content/blogs/[slug].mdx" }
   ```
   This means DOCTOR_LISTING entries get the wrong key, url_path, and file_path in tracking-db.json
   even when Step 5's brief correctly sets `Suggested File: src/content/doctors-listings/<slug>.mdx`.

   Cross-reference: `briefs/NEW-psychiatrist-in-mumbai-brief.md` has no `Suggested File:` line
   at all, confirming the classification gap predates even Step 5.

**Downstream impact:** T9's Step 1 audit-unshipped-briefs script uses `Suggested File:` to determine
the target directory; when that field is absent, it defaults to `/blogs/`. The T9 cluster cap
(Step 2 rule 5) then counts these against the wrong cap bucket. T9 also cannot apply the
listing-viability gate (Step 2 rule 7) without the correct target dir.

## Proposed change

**File to edit:** `cowork-tasks/task5-new-content-discovery.md`
**Edit type:** two line-edits (Step 4 addition + Step 6 template fix)

---

### Edit 1 — Add DOCTOR_LISTING branch to Step 4

**Before (after the `/illnesses/` branch, end of Step 4 section):**
```
**→ SPOKE_PAGE under /illnesses/** if:
- Keyword is a specific mental health condition variant or subtype not yet covered
- (Rare — most conditions are already covered)
- File path: src/content/illnesses/[slug].mdx
- Schema: MedicalCondition, FAQPage, MedicalWebPage

### Step 5 — Generate new content brief
```

**After:**
```
**→ SPOKE_PAGE under /illnesses/** if:
- Keyword is a specific mental health condition variant or subtype not yet covered
- (Rare — most conditions are already covered)
- File path: src/content/illnesses/[slug].mdx
- Schema: MedicalCondition, FAQPage, MedicalWebPage

**→ DOCTOR_LISTING under /doctors/** if:
- Keyword is "[role] in [city]", "[language]-speaking [role]", "[role] near me", "[specialty] specialist in [city]"
  (e.g. "psychiatrist in mumbai", "kannada speaking doctors bangalore", "ocd specialists in chennai")
- AND Mindtalk has ≥1 live profile in `src/content/doctors/*.mdx` matching the role + city/language filter
  (use listing-viability gate: `filterCity`, `filterLanguage`, `filterSpecialty`, or `filterAgeGroup` ≠ Teen/Children)
- AND the keyword is NOT age-group restricted to Teen/Children (those go to Cadabams CDC — see age-group rule below)
- File path: src/content/doctors-listings/[slug].mdx (renders at /doctors/[slug])
- Content Type: DOCTOR_LISTING
- Schema: MedicalBusiness + FAQPage
- Suggested URL: /doctors/[slug]  ← NOT /doctors-listings/ (dead route — always use /doctors/)

> **Age-group exclusion rule (CDC-EXCLUSION):** If the keyword contains any of the following signals,
> it targets a Teen/Children audience and belongs on the **Cadabams CDC website, NOT mindtalk.in**.
> Do NOT generate a mindtalk.in brief. Log: `CDC-EXCLUSION: "[keyword]" targets Teen/Children — route to Cadabams CDC`.
> Signals: teen, teenager, adolescent, child, children, kid, school-going, below 18, under 18, 12-18, toddler, M-CHAT.
> This applies to ALL content types (DOCTOR_LISTING, BLOG_ARTICLE, etc.).

### Step 5 — Generate new content brief
```

---

### Edit 2 — Fix Step 6 tracking-db key template

**Before (Step 6, tracking-db entry template):**
```json
"NEW-/blogs/[slug]": {
  "type": "NEW_CONTENT",
  "url_path": "/blogs/[slug]",
  "file_path": "src/content/blogs/[slug].mdx",
  "primary_keyword": "[keyword]",
  "status": "BRIEF_CREATED",
  "brief_created_at": "[TODAY]",
  "brief_path": "briefs/NEW-[slug]-brief.md"
}
```

**After:**
```json
"NEW-/[url_prefix]/[slug]": {
  "type": "NEW_CONTENT",
  "url_path": "/[url_prefix]/[slug]",
  "file_path": "src/content/[file_prefix]/[slug].mdx",
  "primary_keyword": "[keyword]",
  "status": "BRIEF_CREATED",
  "brief_created_at": "[TODAY]",
  "brief_path": "briefs/NEW-[slug]-brief.md"
}
```

> Where `[url_prefix]` and `[file_prefix]` are derived from the content type determined in Step 4:
> - BLOG_ARTICLE → url_prefix=`blogs`, file_prefix=`blogs`
> - SPOKE_PAGE/treatments → url_prefix=`treatments`, file_prefix=`treatments`
> - SPOKE_PAGE/illnesses → url_prefix=`illnesses`, file_prefix=`illnesses`
> - DOCTOR_LISTING → url_prefix=`doctors`, file_prefix=`doctors-listings`
>   (note: file is in `doctors-listings/` but public URL is `/doctors/`)

## Rationale

- Mindtalk has 200+ doctor listing pages at `/doctors/`. T5 has sourced 90+ DOCTOR_LISTING candidates
  from STANDING_BACKLOG and GSC query mining (1,200–2,400/mo, all Tier A). Without the routing branch,
  these Tier A pages are misfiled as `/blogs/` or `/treatments/`, causing incorrect cap-bucket
  attribution and missing listing-viability checks in T9.
- The BACKLOG explicitly routed this to Meta-Learner Sun 11-08 as "T5/T20 template proposal, ~25".
- Code-path changes to `scripts/new-content-discovery.py` are human-review-only per T13 constraints.
  This proposal targets only `cowork-tasks/task5-new-content-discovery.md` (workflow instruction).

## Risk assessment

- **Low risk.** The Before text does not exist in any applied/running state — the DOCTOR_LISTING branch
  simply doesn't exist, so adding it creates new behaviour, not changing existing.
- One edge case: keywords that could match BOTH TREATMENT (e.g. "psychiatrist for depression") AND
  DOCTOR_LISTING ("psychiatrist in mumbai"). The rule-set above is specific enough — city/language
  pattern is the discriminator. T9's listing-viability gate (≥1 live profile) provides a second guard.
- The age-group exclusion rule (CDC-EXCLUSION) is additive — it cannot block content that would
  otherwise have passed.

## Rollback

Revert by removing the `→ DOCTOR_LISTING under /doctors/` block and restoring the Step 6
tracking-db template to `"NEW-/blogs/[slug]"`. Both edits are isolated sections, easy to revert.
Brain backup: `brain/before-snapshots/task5-new-content-discovery-20261108T1441.bak`

## Veto instructions

To veto: rename to `t5-doctor-listing-classification-20261108T1441.vetoed.md` and add a `## Veto reason` section.

To approve early: rename to `t5-doctor-listing-classification-20261108T1441.approved.md`.
