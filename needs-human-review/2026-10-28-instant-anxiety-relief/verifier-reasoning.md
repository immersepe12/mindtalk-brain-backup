# T9 NEEDS_HUMAN — /blogs/instant-anxiety-relief — 2026-10-28

**Verdict:** NEEDS_HUMAN (independent Verifier sub-agent, 2026-10-28 run)

## What passed (all literal, independently re-derived, not taken from narrative claims)
- Frontmatter complete: title, seo.metaTitle/metaDescription, slug, category, reviewer,
  publishedOn/lastReviewed (both 2026-10-28, today), quickAnswer, keyTakeaways, faqs,
  intent_tier: B present per INTENT-PRIORITY.md §2.
- FAQ count: 5 (≥5 required) — passes.
- Word count: 1,267 words in body excl. frontmatter (counted directly) — passes (≥1,200).
- metaTitle: 63 chars, ends "| Mindtalk" — passes (≤65). metaDescription: 154 chars — passes (≤160).
- Internal links: 5 found (2 doctor + 2 blog + 1 treatment), ≥3 required — passes.
- Tier A link count (INTENT-PRIORITY §1 Tier B rule, ≥2 Tier A booking surfaces):
  2 — /doctors/anxiety-specialists and /doctors/psychologists-in-bangalore — satisfied.
  (The brief itself only listed 1 Tier A target; the shipped MDX correctly added a
  second, so the policy is met in the artifact even though the brief draft would not
  have been.)
- Link validity: all 5 live URLs curled directly (production is the source of truth,
  not local repo/tracking-db, which is an incomplete mirror for /doctors/ and
  /treatments/) — all 5 returned HTTP 200 with correct, substantive titles. No broken
  links.
- Reviewer: dr-sneha is a real, listed slug in reviewer-load-state.json, load=4
  (live top-level counter), well below heavily-loaded reviewers (sucheta-saha 26,
  dr-arohi-vardhan 21, tirzah-johnson 9) — not overloaded.
- No algo_watch/do-not-publish hold: tracking-db row is clean (status BRIEF_CREATED,
  no flags); BRAIN.md confirms ALGO_WATCH CLEARED 2026-10-18, no reversal since.
- AP3 N/A (blog, not /illnesses/ or /treatments/ or suicide-safety).
- Clinical/safety framing: appropriately hedged ("for many people," "worth trying"),
  frames techniques as symptom management not treatment, directs to professional help
  in FAQ + "What These Techniques Don't Do" + closing CTA. No unverifiable clinical
  claims (brief's draft "RCT support" language was correctly dropped from the shipped
  MDX). No unsafe advice.

## What needs a human decision
Possible query/topic cannibalisation that this brief's "Collision check passed ✓
(verified 2026-10-19)" line does not evidence was actually checked:
- An existing live page, `top-8-tips-for-immediate-anxiety-relief` (published
  2025-08-21, same "anxiety" category, title "Top 8 Immediate Anxiety Relief Tips to
  Calm Your Mind"), targets near-identical semantic intent to the new "instant anxiety
  relief" query.
- `reports/queries-2026-10-26.csv` shows this exact query cluster active and
  worsening: "instant anxiety relief" position 8.8 -> 12.3, and a near-duplicate query
  ("immediate anxiety relief: discover the top 8 expert tips") LOST entirely.
- `BRAIN.md`'s own 2026-10-27 entry made GSC query-ownership checks mandatory after a
  same-week cannibalisation VETO on a different brief (can-stress-kill-you). This
  brief's collision check predates that lesson (dated 2026-10-19) and shows no
  evidence it screened for this near-duplicate.

This is a materially different situation from the same-run VETO on
`yoga-for-anxiety-and-overthinking`: there, GSC data showed the *exact* primary
keyword already ranking well (pos 5.6-6.7) via a near-identical sibling page, which
is a clear-cut VETO. Here, the overlap is with a *differently-worded* existing page
("top 8 tips" vs. "instant relief") whose own rankings are declining rather than
strong, so it is plausible the two pages target distinct enough intents (a listicle
of tips vs. an acute-moment technique guide) to coexist — but that has not been
confirmed, which is why the sub-agent correctly declined to auto-approve.

**Needed from Kushal:** a one-line read on whether `instant-anxiety-relief` and
`top-8-tips-for-immediate-anxiety-relief` are meant to compete for the same query
(in which case: differentiate the angle further, or merge/refresh the existing page
instead) or are intentionally distinct enough to both exist. Once confirmed, this
page has no other blockers and can ship on the next T9 run, or be added ad hoc to an
open PR.

Proposed MDX is saved alongside this file as `proposed.mdx`.
