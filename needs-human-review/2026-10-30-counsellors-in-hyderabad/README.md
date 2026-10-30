# REFRESH-counsellors-in-hyderabad: held at Verifier gate B1 (2026-10-30)
Verifier verdict: APPROVE (conditional). Blocking condition B1 (roster gate) could NOT be satisfied, so the Executor did not ship.
Evidence:
- main (EXARFit/mindtalk-website) src/content/doctors-listings/counsellors-in-hyderabad.mdx still has filterCity "Hyderabad" + filterRole "Counsellors".
- Sibling pages therapists-in-hyderabad / psychiatrists-in-hyderabad were set to filterCity: null (commit 7113261, 2026-08-05) because Hyderabad-tagged clinicians do not exist and the listing renders empty.
- Only 3 doctor profiles mention Hyderabad (kanchana-musrif, kirti-srivastava, sufia-nusrat); none confirmed with a Counsellor role. Languages English/Hindi only.
- Live page (HTTP 200) SSR HTML shows no doctor cards; live roster count N could not be read.
Decision for Kushal (any one):
1. Confirm N>=1 on the live page, then re-queue the refresh (T11 will ship as PR).
2. Approve filterCity: null (+ explanatory comment, 7113261 precedent) bundled with the copy refresh.
3. Leave the page as is.
Other conditions carried (B2-B6, C1-C6) are in brain/memory/verifier-log.md. Brief: briefs/REFRESH-counsellors-in-hyderabad-brief.md.
