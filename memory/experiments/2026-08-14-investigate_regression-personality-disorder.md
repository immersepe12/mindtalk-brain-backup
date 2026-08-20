# investigate_regression — /illnesses/personality-disorder — 2026-08-14

## What we did
Ran focused diagnostic on /illnesses/personality-disorder following GSC-confirmed HIGH_PRIORITY_DROP (pos 5→9, -100% clicks WoW, -38% impressions). Checked tracking-db, read MDX file, read GSC data file, reviewed existing brief, checked git history.

## Signal — What's Actually Happening

### GSC data (2026-08-03 to 2026-08-10)
- Page-level avg position: **34.4** (significant drop from pos 5 on primary keyword)
- Clicks: 0 | Impressions: 53 (down from ~86 impressions in prior window per BACKLOG)
- Primary keyword "personality disorder treatment bangalore": not visible in current GSC window — likely outside top 100
- Secondary keyword "counselling for personality disorder": pos 58.7 (dropped from ~53.3)
- Notable: ranking pos 2 for "am i a sociopath?" and "high functioning ocpd" (but 1 impression each — near-zero volume)

### Git History
- Last modification: commit `270cf0c` — "feat(ymyl): add clinical reviewer to 30 illness + 25 treatment pages" (2026-06-09, Sprint A)
- Commit before that: `cccb20d` — original live commit
- **AP4 check: CLEAR** — last modification 66 days ago, well past 14-day threshold

### MDX Content Analysis
- **ZERO "Bangalore" mentions** anywhere — title, H1, or body
- **No QuickAnswer block** present
- **No KeyTakeaways block** present
- **No FAQs / `faqs:` frontmatter** — 0 FAQ entries (§5 pre-check fail risk)
- **Empty H2 heading**: "Mental Health Professional For Personality Disorder" has no body content — thin content signal
- **Old-format frontmatter**: `reviewer: dr-sneha` present but NO `clinical_reviewer_signed_off.date` (Sprint A format, pre-AP3-B Option B)
- **Internal links**: 6 contextual links present (anxiety, OCD, depression, talk-therapy, DBT, CBT) ✅
- Word count: ~2,981 words (thin for a competitive top-10 YMYL page)

### Tracking-db Status
- status: **BRIEF_CREATED** (2026-08-11)
- brief_path: `briefs/personality-disorder-brief.md`
- primary_keyword: "Personality Disorder Treatment Bangalore"
- severity: MODERATE
- type: REFRESH

## Root Cause — Primary
**Zero Bangalore geo signal.** The primary target keyword is "Personality Disorder Treatment Bangalore" but the word "Bangalore" does not appear ONCE in the URL, title, H1, or body. All top-3 SERP competitors (cadabams.org, maargamindcare.com, sukoonhealth.com) have "bangalore" in URL path, title, AND body. Google.co.in is heavily geo-weighting results — this structural gap is almost certainly the primary driver of the pos 5→9 (and ongoing) drop.

## Root Cause — Secondary
**AP9 confirmation.** This page was at pos 5 when Sprint A added the reviewer (`dr-sneha`) without any content depth refresh. AP9 says: reviewer-only fix fails for pages at pos ≤20. The page is now at pos 34.4 page-average, confirming AP9 predicted outcome. Content depth fixes needed alongside geo signal.

## Recommended Action
**Status: BRIEF ALREADY EXISTS** — no new investigation action required. The brief at `briefs/personality-disorder-brief.md` (created 2026-08-11) is comprehensive and addresses:
- Bangalore geo signal fix (title, H1, new intro section)
- 3 new H2 sections (Treatment approach, Family support, FAQ)
- 5 mandatory FAQs
- Meta title + description updates with "Bangalore"
- Internal linking improvements
- §5 pre-check: ALL pass at brief level

**Blocker before shipping:**
- AP3-B: YMYL page requires `clinical_reviewer_signed_off.reviewer + date ≤90d + scope`. Current frontmatter has `reviewer: dr-sneha` (old Sprint A format) but no signed-off date. Dr. Sneha must sign off with date before the brief can ship.
- T11 hard constraint: YMYL pages cannot be auto-shipped — requires human action.

## BACKLOG Update
PERSONALITY-DISORDER-DROP-01 (investigate_regression) → REPLACED WITH:

`PERSONALITY-DISORDER-YMYL-SIGNOFF-01 | flag_for_human | Brief ready at briefs/personality-disorder-brief.md. Needs AP3-B sign-off from dr-sneha before shipping. Root cause: zero Bangalore geo signal + AP9 content depth deficit. Once signed off, T11 can queue as ship_REFRESH_brief. | Score: 15 Tier A ×1.5 | NEXT_RUN`

## Watch
No new watch opened — existing brief governs this page. Watch opens when brief ships.

## Notes
- Verifier APPROVED investigate_regression (all 11 checks passed)
- This is a textbook AP9 case: Sprint A reviewer-only fix at pos 5 (top-10) → AP9 predicted failure; confirmed.
- The Strategist (T10) brief creation on 2026-08-11 was the right call. The investigation confirms the brief is ready.
- T11 flagged to Kushal via Slack with brief status and AP3-B requirement.
