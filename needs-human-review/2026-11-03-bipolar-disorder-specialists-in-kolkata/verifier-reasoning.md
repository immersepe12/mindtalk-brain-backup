# T9 NEEDS_HUMAN — /doctors/bipolar-disorder-specialists-in-kolkata — 2026-11-03

**Verdict:** NEEDS_HUMAN (independent Verifier sub-agent, 2026-11-03 run)

## What passed
- Path safety, slug-collision (absent from live main + all 4 open PRs), /doctors/
  cluster cap (3/6 -> 6/6 at, not over, cap with the other 2 pages in this run),
  weekly cap (trivial, fresh week), no url_locked conflict, no PII, no algo_watch
  HOLD language in the source brief, impact claim appropriately hedged (no
  per-page outsized-spike claim).
- Frontmatter correction: brief's own `filterCity: "Kolkata"` was independently
  confirmed wrong and corrected to `filterCity: null` (virtual-only pattern,
  matching the proven live template and the 2026-10-30 run's correction of the
  same defect class).

## What needs a human decision
This page's body makes specific clinical claims that go beyond the lighter-touch
template used by the only directly comparable live page,
`/doctors/bipolar-disorder-specialists-in-bangalore` (which says only "medication
management (where indicated)"):

- Names bipolar I vs. bipolar II and "mixed episodes" as specific diagnostic
  sub-categories.
- States a specific, unsourced treatment timeline: "ongoing monitoring for 6 to
  12 months to confirm the right dose and combination."
- Claims the clinic takes over medication review/adjustment for patients
  diagnosed elsewhere who are "not stabilising" (i.e. treatment-resistant cases).

AP3's literal gate (`brain/VERIFIER.md` §5) only requires `clinical_reviewer_signed_off`
for paths matching `/illnesses/*`, `/treatments/*`, or suicide-safety topics — this
ships to `src/content/doctors-listings/`, so the gate is formally not triggered,
and 5 prior same-process APPROVEs for doctors-listings pages (2026-09-16, 09-18,
09-25, and three on 10-30) all logged "reviewer N/A for this content type."

But the Verifier judged that precedent doesn't resolve this case cleanly: those
prior approvals were language/city-matching listings or defect-fixes explicitly
carrying no clinical content, and the 10-30 `counsellors-in-hyderabad` entry shows
this verification chain already treats "no new clinical claims" as a live gating
fact distinct from folder path. `PRINCIPLES.md`'s P1 ("every illness, treatment,
blog with YMYL content MUST have reviewer") and `GOALS.md`'s quality-bar table are
framed around YMYL *substance*, not the `/illnesses|/treatments` path literal — the
AP3 path-list is arguably a proxy for that substance test, and this page (name a
serious psychiatric illness + unsourced timeline + medication-takeover framing) may
be the proxy's blind spot. AP15 (clinical-claim verification) is also unmet: the
"6 to 12 months" figure has no primary-source citation in the brief or the drafted
MDX.

**Needed from Kushal — one of:**
1. **Ship as-is / ratify "doctors-listings = non-YMYL, no exceptions."** The folder
   path is the only test that matters; condition-filtered listing pages never need
   clinical_reviewer_signed_off regardless of body content. If so, this page can
   ship on the next T9 run with no changes.
2. **Require a named clinical reviewer** on condition-filtered doctors-listings
   pages specifically when the body makes diagnostic-subtype, treatment-timeline,
   or medication-management claims — even though the folder is `doctors-listings/`
   — and have this (and future) briefs of this shape carry
   `clinical_reviewer_signed_off` before T9 will ship them.
3. **Trim the body** to the lighter Bangalore-style template (drop the bipolar
   I/II/mixed-episode subtyping, the 6–12 month timeline, and the
   treatment-resistant/medication-takeover line) so it matches the established
   non-clinical listing pattern, then ship without a reviewer.

Proposed MDX (as drafted, before any trim) is saved alongside this file as
`proposed.mdx`. The other 2 pages in this run — `/doctors/adhd-specialists-in-chennai`
and `/doctors/relationship-issues-specialists-in-mumbai` — were independently
Verifier-APPROVEd and shipped via PR; this page was held back.
