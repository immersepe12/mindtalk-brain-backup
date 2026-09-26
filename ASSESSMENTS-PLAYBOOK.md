# ASSESSMENTS PLAYBOOK — canonical rules for /assessments/* (created 2026-09-25)

**Owner:** Kushal (decisions) · every task that touches assessment pages MUST read this file.
**Why it exists:** assessments are the site's largest organic section — **8,430 clicks / 465,197 impr / 1.81% CTR over 90d (06-27→09-24, page-dimension GSC, all countries)**. The 2026-09-25 sprint (commits `c9b9b731` + `0c4562a6`) rebuilt the section; this file keeps every task consistent with it.

---

## 1. Source of truth

| Thing | Where |
|---|---|
| Every assessment the app offers (203 tests, 36 categories, Clinical/Self, app links) | Company master `MindTalk_Assessments.xlsx` → working copy `reports/MindTalk_Assessments_master_v2.xlsx` (tab **Page Coverage & SEO** = page status, India volume, KD, recommendation, licence flag) |
| App IDs the site uses for hub grids / ItemList | `src/data/inventory/assessments.json` (129 entries; master is the superset) |
| Page content | `src/content/assessments/<slug>.mdx` (type `item` or `category`) |
| Template | `src/app/assessments/[slug]/page.tsx` + `src/lib/discover-schema.ts` |
| Index page copy | `src/content/pages/discover-assessments.mdx` |

**New assessment page = a test that exists in the master.** Never invent an instrument. `assessment_app_id` must come from the master's link (`/assessments/<id>/details`). Add the ID to `assessments.json` in the same commit (category must be one of the inventory categories).

Known gap: master is MISSING 4 IDs the site uses — GAD-7 std `cmpc9j73l00jp01qp5xcf9l3d`, ITQ `woi1cncqbbzftmo6f0260mqo`, WHO-5 `cmrd7ictu002b01shldoh6670`, STAI `jddn9uw0n28bssjn379t42xp`. Do NOT "fix" these pages to master IDs.
Nine item pages deliberately share a sibling's app ID (educational page → closest app test): am-i-depressed-test+bdi→PHQ-9, pcl-5→ITQ, bai→STAI, k10→PSS-10, wender-utah→ASRS, ace-test→CHILDAFF, stress-tolerance-test→DERS-16, y-bocs→OCI. By design — not a defect.

## 2. Keyword ownership map (anti-cannibalisation — check before any brief/refresh)

| Query family | Owner page | Must NOT target it |
|---|---|---|
| psychometric test(s), psychology test | `/assessments` (index) | mental-health-test |
| mental health test | `/assessments/mental-health-test` | index |
| depression test | `/assessments/depression` (hub) | phq-9, am-i-depressed-test |
| am I depressed | `am-i-depressed-test` | phq-9 |
| PHQ-9 | `phq-9` | am-i-depressed-test |
| anxiety test | `/assessments/anxiety` (hub) + `gad-7` (title lead "Anxiety Test (GAD-7)") | other anxiety items |
| stress test, stress level test | `stress-and-tension` (hub) + `pss-10` ("Stress Level Test") | stress-burnout (= burnout angle) |
| burnout test | `am-i-burnt-out-test`, `stress-burnout` hub = work-stress/burnout chooser | — |
| OCD test | `/assessments/ocd` (hub) | y-bocs (owns "ybocs / y-bocs scoring") |
| trauma test, PTSD test | `trauma-ptsd` (hub) | itq (owns "CPTSD test"), pcl-5 |
| BPD test | `am-i-borderline-test` | bsl-23 |
| ADHD test / adult ADHD test | `asrs` | wender-utah (owns "Wender Utah / childhood ADHD symptoms") |
| attachment style test | `attachment-style-test` | `attachment-styles` hub (= "compare attachment quizzes") |
| personality test | `personality-and-identity` hub | big-5 owns "big five" |
| narcissist test | `npi` | — |
| love language test | `love-language-quiz` (Mindtalk's own quiz; "5 Love Languages" is a trademark — never claim to be official) | — |
| compatibility test | `compatibility-test` | — |

## 3. Frontmatter contract (item pages) — every new/edited page must satisfy

Required: `slug, type: item, title, subTitle, category: assessments, category_filter, assessment_app_id, assessment_abbreviation, assessment_full_name, time_minutes, crisis_sensitive, about_condition, publishedOn, lastReviewed, reviewer, returnTo, returnTo_path (/assessments/<app_id>/reports), seo{metaTitle ≤60 chars ending "| Mindtalk", metaDescription 140–158, primaryKeywords, relatedKeywords}, quickAnswer (60–90 words, first sentence answers "what is the <plain-English> test"), keyTakeaways (5–7; template renders up to 7), howToSteps (3), faqs (5–7).`
Optional: `question_count` (only if verified), `normalRange`, `signDetected`, `safetyNotice*`.
Read by NO code (don't rely on them): `category, question_count (display only), returnTo_path, crisis_sensitive, ymyl, review_date, clinical_review_status, featured`.

## 4. Body standard (what made the sprint pages)

1. **Scoring / results section** — GFM table of *published, verified* cut-offs only. If none exist (most Mindtalk Self tests), say so explicitly and describe how the app presents results.
2. **"Validation and evidence" H2** with `### References` — every reference verified. **PubMed web pages CAPTCHA automated fetches → verify via NCBI E-utilities** (`https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esummary.fcgi?db=pubmed&id=<PMID>&retmode=json`): title, first author, year must match. Never invent a PMID, DOI, cut-off, sensitivity figure, or "validated in India / Hindi / NIMHANS" claim. The sprint removed dozens of such unverified claims — do not reintroduce them.
3. **Internal links** — ≥1 `/illnesses/<slug>` + ≥1 `/treatments/<slug>` that exist, + a sibling assessment where genuinely useful.
4. **"What the test does not tell you"** — screening, not diagnosis.
5. Body ≥ ~700 words, no padding.
6. MDX safety: no bare `<` before a letter/digit (write "under 10" or `\<`), no `{}`, no HTML comments.
7. Copyright: never reproduce item wording of licensed instruments (BDI/BDI-II, BAI, STAI, PSQI, HSP Scale, MBI, HADS, ISI, Epworth, Conners, GHQ, WHOQOL). Describe domains instead.

## 5. Gates

- **Safe-messaging slugs** (`c-ssrs`, `eat-26`, `bes`, `bsl-23`, `suicide-safety`, `eating-disorders-body-image`, plus self-harm-adjacent items phq-9/epds/madrs/ham-d): any title/meta/quickAnswer change must follow `Obsidian vault build/PR/safe-messaging-guidelines.md` — no method/means content, no weight/BMI/calorie numbers, crisis resources never weakened, clinician routing kept. `suicide-safety` stays feature-flagged.
- **Clinical sign-off:** (2026-09-25: Kushal confirmed all clinicians signed off in-app; reviewer = best specialty match, never the most junior — psychiatrists for clinician-rated scales, senior clinical psychologists for self-report psychometrics.) Kushal's standing rule — assign the most senior appropriate clinician as `reviewer` (seniority is part of the credential test; e.g. krishna-k-r 22y, rangapriya-raghavan 20y, vishal-kasal 17y, swarupa-mohan-udgiri 17y, dr-arun-kumar 13y, smicky-priya-das 13y) and proceed; log any change to a clinical number in `brain/needs-human-review/`.
- **Do-not-build list (decided):** Enneagram, DISC, MBTI/16-type branded, Thomas-Kilmann, Mensa/IQ, mental-age (trademark / no app test / off-brand); **Dosha** (YMYL credibility); GHQ, WHOQOL-BREF, EDE-Q (licence needed). 32 of 34 unpaged clinical instruments have ~0 India demand — keep in-app only. Built: THI, Sleep-Hygiene-Index, Cube (honest "not validated" framing).
- **Next build candidates from master (if demand re-checked):** SAID → fold into social-anxiety; AILT (long-term compatibility) only if compatibility-test reaches page 1; Synesthesia/Ikigai/Empathy/Archetype (150–200/mo, KD 0–5) = low priority batch.

## 6. Measurement rules (hard)

- **Page totals from GSC `dimensions:["page"]` ONLY.** Summing `["query"]` rows = ~40% of truth (anonymised queries) — GSC-QUERY-UNDERCOUNT-01. `scripts/gsc-pull.py` fixed 2026-09-25.
- **URL lists from the live sitemap**, not tracking-db/keyword-map (gad-7, the #1 page, was never pulled) — GSC-URL-LIST-GAP-01. `gsc-pull.py --all` now unions the sitemap.
- **Absence from a truncated pull ≠ not ranking** (MINE-TRUNCATION-ABSENCE-01).
- **Ahrefs:** use for India volume/KD + competitors only (it sees 34 keywords for gad-7 vs 1,382 real GSC queries). Prefix mode needs `www.mindtalk.in/assessments/`. Trust Ahrefs India head-term over Keyword Planner (which reports variant groups / global).
- Section baseline + per-page watches: `brain/WATCH.md` → blocks "ASSESSMENTS GROWTH SPRINT" and "ASSESSMENTS PHASE 2" (W-ASSESS-*-0925). Midpoint **2026-10-16**, Day-42 **2026-11-06**.
- AI citations: `brain/AI-PRIORITY-QUERIES.md` → assessment add-on queries A1–A8.

## 7. Shipping mechanics (the only path that works from this environment)

Local checkout is stale (100+ commits behind) and disk is full, so `npm run build` cannot run locally. **AP6 is satisfied by a Vercel PREVIEW build:** pull fresh files from `origin/main` via GitHub API → edit → push to a feature branch via Git Data API → wait for the branch deployment `READY` (Vercel MCP `list_deployments branch=…`) → fetch 2–3 pages from the preview (share-token cookie) → merge branch → confirm prod READY on the merge SHA → **curl the live pages** (AP10). Helper: `outputs/stage/gh.py` pattern (pull / push / merge). Never write scratch to `/tmp` (disk full → writes silently fail and you read stale files).

## 8. Template facts (so nobody re-diagnoses them)

Emitted on every assessment page since `0c4562a6`: Organization + WebSite (same @ids as homepage `https://www.mindtalk.in/#organization` / `/#website`), MedicalWebPage (named `reviewedBy`, `speakable` on `[data-speakable]` quick-answer/key-takeaways, publisher, inLanguage), BreadcrumbList, FAQPage, MedicalTest + HowTo (items), ItemList with real item URLs (hubs). Visible `ReviewerByline` ("Clinically reviewed by Dr X, credentials. Last reviewed <date>."). Sitemap lastmod = `lastReviewed`. 33 orphan URLs 308 → canonical via `middleware.ts` SLUG_FIXES.
Not done (dev backlog): `citation` schema, Quiz/WebApplication node.

## 9. Intent tier for assessment briefs (INTENT-PRIORITY.md gate)

Every assessment brief still needs `intent_tier` in frontmatter:
- **Tier B** — clinical/condition screeners (anxiety, depression, OCD, trauma, ADHD, BPD, autism, bipolar, addiction, burnout, sleep, etc.). Must link to **≥2 Tier A** surfaces (a `/doctors/...` listing + the in-page doctor/booking CTA the template already renders).
- **Tier C — sanctioned exception "ASSESSMENT-DEMAND-GEN"** (Kushal, 2026-09-25: "triple down" on assessments): consumer/self tests from the company master (love language, compatibility, cube, chronotype, RIASEC, HSP, introvert-extrovert, etc.) MAY be built when §5 demand threshold is met. They count toward a separate demand-gen allowance (max 2 per weekly run), not the 10% Tier C cap, and are judged on signups / assessments completed / assisted traffic — never on bookings. Each must link to at least one validated clinical assessment and one Tier B page.

## 10. Recommended NEW app assessments (not in the master — needs the app team) — 2026-09-25
Demand = Google Keyword Planner India exact-term (Ahrefs units exhausted until 09-30; re-verify then). Build page only after the app test exists.
| Priority | New app test | Instrument (licence) | India searches/mo | Why |
|---|---|---|---:|---|
| 1 | Memory / cognitive check | SAGE (Ohio State, free) — NOT MMSE/MoCA (licensed) | memory test 2,900 · cognitive test 1,600 | Caregiver intent → dementia/geriatric Tier A |
| 3 | Geriatric depression | GDS-15 (public domain) | 880 | Easy, clinical, elderly-care funnel |
| 4 | Early psychosis screen | PQ-B (free) — clinician-routed, safe-messaging | schizophrenia test 720 | Family intent → Cadabams inpatient strength |
| 5 | Adult dyslexia checklist (ADULTS ONLY) | Adult Dyslexia Checklist (Vinegrad/BDA) or equivalent free screener | dyslexia test 1,900 (shared with child intent) | Adult learners only — child framing belongs to CDC |
| 6 | Insomnia | Athens Insomnia Scale (free) — NOT ISI (licensed) | 390 | Sleep cluster already built |
| 7 (optional, brand call) | Psychopathy traits | LSRP (free for non-commercial research — confirm) | psychopath 1,900 · sociopath 720 | Curiosity traffic, Tier C |
Check first whether AUTC = AQ (aq test 590, raads r 320) before adding an adult autism instrument.

## 11. 🚸 CHILDREN → CadabamsCDC, never Mindtalk (Kushal, 2026-09-25)
**Everything children-related (child/adolescent assessments, toddler screens, school-age learning difficulties, child ADHD/autism, parenting-of-young-children tests) belongs on Cadabam's Child Development Centre — https://www.cadabamscdc.com/ — not mindtalk.in.** (Not to be confused with the vault project "CadabamsCDC" = Cadabams Diagnostics middleware.) Live assessment pages were scrubbed of child-instrument recommendations on 2026-09-25 (SCAS, A-DES, EDE-A, ITQ-CA → CDC routing link).
- Do NOT create child-focused assessment pages on mindtalk.in: M-CHAT(-R), SCAS, ITQ-CA, A-DES, EDE-A, child ADHD (Vanderbilt/Conners), child dyslexia/learning screens, TMH teen check, developmental-delay/speech-delay tests.
- Mindtalk assessment pages stay adult-framed (autism-test = adults, asrs = adult ADHD, wender-utah = adults recalling childhood symptoms, childhood-trauma-test / ace-test = adults reflecting on their own childhood — these are fine).
- Child-intent demand found 2026-09-25 (hand to the CDC SEO effort): mchat 1,900/mo · dyslexia test 1,900 (mixed adult/child) · "adhd test for kids", "autism test for kids", "anxiety test for kids", "developmental delay test", "speech delay test" (KP groups these under the head terms).
- Existing mindtalk illness pages with child scope (developmental-delay, cerebral-palsy, intellectual-disability, learning-disability, conduct-disorder, play-therapy) pre-date this rule — flagged for a Kushal decision (redirect/cross-link to CDC vs keep); do not expand them.
