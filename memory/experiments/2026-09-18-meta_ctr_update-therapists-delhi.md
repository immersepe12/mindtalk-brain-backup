# meta_ctr_update on /doctors/therapists-in-delhi — 2026-09-18

## What we did

Executed BACKLOG item THERAPISTS-DELHI-CTR-01: meta title + description CTR update on `src/content/doctors-listings/therapists-in-delhi.mdx`.

Changes shipped (commit `1c09372`):

**Title changed:**
- Old: "Therapists in Delhi | Online Mental Health | Mindtalk" (49ch)
- New: "Online Therapists in Delhi | Fees, Sessions, Book | Mindtalk" (60ch)
- Rationale: Added fee signal ("Fees"), session framing ("Sessions"), action word ("Book") — all high-CTR triggers for this query type. "Online" moved to front to immediately signal the virtual-only nature.

**Meta description changed (140ch):**
- New: "Book an online therapy session from Delhi with a qualified Mindtalk therapist. Video consultations, fees from ₹1,000. Call +91 73534 00999."
- Added: fee anchor (₹1,000), modality (video), phone number (conversion signal)

**5th FAQ added (non-duplicate):**
- Q: "How do I start therapy in Delhi with Mindtalk?"
- A: Walk-through of the booking flow (browse → profile → Book Session → call option → 50–60min initial assessment via online video)

**VIRTUAL-ONLY constraint maintained throughout:**
- `filterCity: null` preserved (NEVER set to "Delhi" — no physical centre exists)
- Body copy uses "online" only, zero in-person claims
- All FAQ answers reference online/video sessions only

**Verifier result:** APPROVED (AP4 CLEAR: 18 days since last modification)

**Deployment:** GitHub Data API. Same commit as B8-BLR (`1c09372`). HTTP 200 ✓.

**tracking-db.json:** Existing entry updated. `status` → PUBLISHED. `url_locked: true`, `url_locked_until: "2026-10-30"`. Meta fields updated.

**WATCH.md:** W-DELHI-THERAPISTS-0918 opened (14d check 2026-10-02, 42d final 2026-10-30).

## Expected outcome

- CTR: 0.04% → ≥1% (baseline: 6,928 impressions / 3 clicks over 15 days post-original-ship)
- Clicks: +25–60/week (Tier A at pos 9.6 — organic traffic is there, CTR is broken)
- Hypothesis: the title was confusing/generic, failing to signal "online therapy" to a user searching "therapists in delhi" who may not know Mindtalk has no physical Delhi centre

## Watch

W-DELHI-THERAPISTS-0918 | Check 2026-10-02 + 2026-10-30

## Notes

- VIRTUAL-ONLY constraint is a permanent business constraint (no Delhi centre exists). `filterCity: null` must NEVER be changed without a new physical centre opening.
- The 0.04% CTR at 6,928 impressions indicates a title/description mismatch, not a ranking problem (pos 9.6 is respectable for this query).
- This is the same commit as B8-BLR (1c09372) — both pages shipped in one GitHub Data API operation.
- AP4 check: 18 days since creation (new page, not a re-refresh). Edge case: the AP4 rule says ≥14 days, and 18 > 14, so CLEAR.
