# NEEDS_HUMAN: gender-identity-disorder
**Date:** 2026-08-04
**Task:** T9 Auto-Ship
**Verifier verdict:** NEEDS_HUMAN — §3: illness hub conflict / keyword cannibalization

## Issue
`/illnesses/gender-identity-disorder.mdx` EXISTS — this is the illness hub page targeting the same head keyword "gender identity disorder".
Shipping a /blogs/ page on the same keyword creates direct cannibalization between illness hub and blog.

## Options
- **(A) Accept risk** — ship as-is; /illnesses/ and /blogs/ pages can coexist, Google tends to prefer the illness hub for clinical queries anyway; blog may rank for informational variants
- **(B) Reframe blog title** — differentiate from hub: e.g., "Gender Identity Disorder vs Gender Dysphoria: The DSM-5 Change & India Law | Mindtalk" (covers the naming shift + legal context not in the illness hub)
- **(C) Merge** — add the blog's content (DSM-5 change history, ICD-11, India legal context) directly into the illness hub as new sections instead of shipping a separate blog

## Proposed MDX
Saved at: `/outputs/gender-identity-disorder.mdx`
Reviewer assigned: tejal-jaiswal (ACT / affirming therapy specialist)
Meta title: "Gender Identity Disorder: What It Is & Getting Support | Mindtalk" (65 chars)
Meta desc: "Understand gender identity disorder (now called gender dysphoria), what the DSM-5 and ICD-11 say, and how affirming mental health support works in India." (153 chars)

## Action Required
Kushal decision: A / B / C
Recommendation: Option B (reframe title) — lowest effort, avoids cannibalization, adds unique angle (DSM-5 renaming + India law) not covered by illness hub.
