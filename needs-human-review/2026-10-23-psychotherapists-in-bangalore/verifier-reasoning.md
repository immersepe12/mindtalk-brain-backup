# T9 NEEDS_HUMAN — /doctors/psychotherapists-in-bangalore — 2026-10-23

**Verdict:** NEEDS_HUMAN (independent Verifier sub-agent, 2026-10-23 run)

## What passed
- Slug collision, query-ownership (35%/1%), children-rule, cluster cap (3/6 after this
  run's other 2 ships), weekly cap (2/20 after this run) — all PASS.
- AP16 reviewer fit: navyashri-s (Consultant Clinical Psychologist) is a correct
  specialty match for a psychotherapy/talk-therapy listing page. (The orchestrator
  initially mis-assigned shilpa-avarebeel — a Senior Geriatric Consultant, the exact
  AP16 counter-example doctor — and self-corrected before this review.)
- Cannibalisation guard vs /doctors/therapists-in-bangalore is real (modality-led
  framing, distinct H2s/FAQ), not cosmetic.
- metaTitle 57 chars ending "| Mindtalk", 6 FAQs, 7 internal links all independently
  confirmed live, word count and PII in bounds.

## What needs a human decision
The brief states Mindtalk's 4 Bangalore centres as "Indiranagar, JP Nagar, Kalyan
Nagar, Kanakapura Road." The live `src/content/centers/` collection only has 4 entries:
Indiranagar, Kalyan Nagar, Kanakapura Road, Sarjapura — no JP Nagar. The orchestrator
substituted Sarjapura for JP Nagar in the draft (matching the live centers collection
and the already-shipped sibling page therapists-in-bangalore.mdx).

However, the assigned reviewer navyashri-s has her own doctor-profile `subLocation`
tagged "JP-Nagar" — not any of the 4 centres above. Two possibilities:
1. JP Nagar is a stale/incorrect tag on navyashri-s's profile — fine to ship with
   the 4-centre Sarjapura version as-is.
2. JP Nagar is a real satellite/consulting location missing from the `centers`
   content collection — in which case the page may be telling patients to visit
   centres that don't include where their listed clinician actually practices.

**Needed from Kushal:** confirm which is correct (one line). Once confirmed, this
page has no other blockers and can ship on the next T9 run.

Proposed MDX is saved alongside this file as `proposed.mdx`.
