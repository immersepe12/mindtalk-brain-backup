# draft_sprint_prompt on T17-7 (/Doctors AEO) — 2026-07-24

## What we did
Drafted an AEO (Answer Engine Optimization) sprint prompt for the /Doctors listing page.
Saved to: `prompts/auto-drafted-sprint-aeo-doctors-2026-07-24.md`

## Prompt contents
- 5-question `faqs:` frontmatter array targeting booking-flow PAA queries
  (Who are Mindtalk's psychiatrists? How to book? First appointment? Near me in Bangalore? Cost?)
- MedicalOrganization JSON-LD to consolidate the Mindtalk = Cadabams online therapy entity signal
- Structured E-E-A-T intro paragraph naming 4 Bangalore centre locations + credential claims
- Pre-fire fact-check checklist (pricing, doctor count, location names, RCI/MCI licensing claim)
- AP3 accuracy review gate (no clinical efficacy claims; process + credential facts only)

## Expected outcome
From BACKLOG: MT is already #2 on "near me psychiatrist" + "psychiatrist closest to me" (110K/mo).
When Google AI OV expands to local-intent MH queries, MT needs AEO-structured content to capture citation.
FAQ rich results: +0.1–0.3pp CTR lift on doctor pages (currently ~1.66% CTR).
Entity disambiguation: MedicalOrganization JSON-LD routes AI citations to mindtalk.in, not cadabamshospitals.com.

## Watch
T17-7-REVIEW row added to BACKLOG. 24h review gate = ready 07-25.
No watch task needed yet (no content shipped; watch fires after the sprint is actually executed).

## Notes
- Critical pre-fire decision: confirm if /doctors page is MDX-editable or programmatic (src/app/doctors/page.tsx).
  If programmatic → dev required to add FAQ schema to the page component, not an MDX content edit.
- Fact-check required: ₹1,250 pricing, 72+ doctor count, 4 location names (Jayanagar, Bannerghatta Road, Hebbal, Indiranagar)
- DO NOT fire this sprint without human review — `draft_sprint_prompt` action type requires explicit human confirmation.
