# ship_REFRESH_brief on /doctors/therapists-in-bangalore — 2026-09-18

## What we did

Executed BACKLOG item B8-BLR: full content refresh of `src/content/doctors-listings/therapists-in-bangalore.mdx`.

Changes shipped (commit `1c09372`):

**Frontmatter additions:**
- `reviewer: dr-sneha` + `lastReviewed: "2026-09-18"`
- `quickAnswer`: 2-sentence answer covering 4 Bangalore centres + fee anchor (₹1,000)
- `keyTakeaways`: 4 bullets (4 centres, evidence-based approaches, online parity, booking CTA)
- `faqs:` frontmatter block — 5 Q&As driving FAQPage JSON-LD:
  1. Where are Mindtalk's therapy centres in Bangalore?
  2. How much does therapy cost at Mindtalk Bangalore?
  3. Can I book an online therapy session with a Bangalore therapist?
  4. How long is a therapy session in Bangalore?
  5. What types of therapy does Mindtalk Bangalore offer?

**Body additions:**
- `## Mindtalk Therapy Centres in Bangalore` — 4-centre list (Indiranagar, Sarjapura, Kanakapura Road, Kalyan Nagar) with internal links to `/illnesses/anxiety`, `/illnesses/depression`, `/treatments/cognitive-behavioural-therapy-cbt`
- `## In-Person vs Online Therapy in Bangalore` — 5-row comparison table (cost, format, suitability, booking, wait time)

**Verifier result:** APPROVED (corrected: added ≥3 internal links per §7 requirement; AP4 CLEAR at 157 days since last modification)

**Deployment:** GitHub Data API (FUSE environment). Single tree commit with Delhi page (THERAPISTS-DELHI-CTR-01). Both pages HTTP 200 ✓.

**tracking-db.json:** New entry added. `url_locked: true`, `url_locked_until: "2026-10-30"`.

**WATCH.md:** W-BLR-THERAPISTS-0918 opened (14d check 2026-10-02, 42d final 2026-10-30).

## Expected outcome

- Primary query "therapists in bangalore": pos 16.2 → ≤11 (recover pre-drop baseline of 9.3)
- Clicks: +30–80/week (Tier A, current ~4 clicks/week from -43% regression)
- FAQPage schema appearance in SERP within 7–14 days
- Reviewer attribution on card (dr-sneha)

## Watch

W-BLR-THERAPISTS-0918 | Check 2026-10-02 + 2026-10-30

## Notes

- This was B8-BLR from the T12 Learner's regression diagnosis. The drop (pos 9.3 → 16.2, -43% clicks) was sustained over 8+ weeks.
- Committed in the same tree as THERAPISTS-DELHI-CTR-01 (efficiency: 2 blobs, 1 tree, 1 commit).
- AP4 was clear: last MDX modification was 157 days prior.
- The 4-centre structure is factually accurate per Mindtalk's physical footprint in Bangalore.
- VIRTUAL-ONLY constraint does NOT apply here (in-person sessions ARE available at BLR centres).
