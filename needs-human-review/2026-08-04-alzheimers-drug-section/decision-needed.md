# NEEDS HUMAN: Alzheimer's New Drug Section

**Date raised:** 2026-08-04
**BACKLOG row:** W28-YMYL-BATCH-SHIP-01 (batch 2/2)
**Verifier verdict:** NEEDS_HUMAN (§5 AP3 spirit violation)
**Slack sent:** 2026-08-04 ts:1785842473.454069

## What is blocked

`/illnesses/alzheimers` refresh — second attempt (YMYL_RECOVERY_FAILED).

The brief adds:
- Caregiver support section (~180w) ✅ Clean under Sprint A sign-off
- Alzheimer's vs Dementia rewrite (~60w) ✅ Clean
- 4 FAQs (which doctor, age of onset, cost, treatability) — FAQ on treatability mentions Lecanemab/Donanemab ⚠️
- New treatments section (~120w on Donanemab, Lecanemab, India availability) ⚠️ BLOCKED
- Meta title/desc updates ✅ Clean
- CTA fix ✅ Clean
- 3 internal links ✅ Clean

## Why blocked

The brief itself explicitly says: "Any new clinical content (new treatments section) must be reviewed by a qualified psychiatrist or neurologist before publish." Sprint A's dr-arun-kumar sign-off (2026-06-09) covered the page as it existed then. The Donanemab/Lecanemab claims are NEW clinical content not in the Sprint A scope. Shipping specific FDA drug names, India availability, and clinical trial claims to a YMYL_RECOVERY_FAILED page without fresh review = AP3 violation.

## Kushal's options

**Option A — Strip and ship now:** Remove Donanemab/Lecanemab section + affected FAQ. Ship everything else immediately. T11 can execute this in the next run.

**Option B — Targeted sign-off, then ship complete:** Get a focused review from dr-arun-kumar or a neurologist specifically on the new treatments section. Update brief frontmatter with new `clinical_reviewer_signed_off` date covering this content. T11 ships full brief on next run after sign-off confirmed.

## Brief location

`briefs/alzheimers-brief.md`

## Target page

`src/content/illnesses/alzheimers.mdx`
