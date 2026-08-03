# NEEDS_HUMAN: Trust Issues Cannibalization

**Date:** 2026-07-28
**Brief:** NEW-how-to-deal-with-trust-issues-brief.md
**Verifier verdict:** NEEDS_HUMAN (§3 Goal Alignment — cannibalization)

## Issue

`/blogs/how-to-deal-with-trust-issues` (proposed) and `/blogs/how-to-fix-trust-issues` (live since 2026-07-07) target the same user intent cluster.

Both pages:
- Address: how to [fix/deal with] trust issues in relationships
- Use CBT, schema therapy, EMDR as recommended approaches
- Category: relationship-issues
- Similar structure (5–7 evidence-based steps)

Shipping both would split authority and both would underperform on the "how to [verb] trust issues" SERP cluster.

## Decision Required

**(a) Consolidate:** Redirect `/blogs/how-to-fix-trust-issues` to the proposed URL (or vice versa), merge best content from both. Best for long-term SEO.

**(b) Differentiate:** Rewrite the proposed brief to have a genuinely distinct angle — e.g., "how-to-deal-with-trust-issues" = emotional processing and daily coping (not fixing); "how-to-fix-trust-issues" = step-by-step repair guide. Different user journey stages.

**(c) Retire brief:** Archive `NEW-how-to-deal-with-trust-issues-brief.md`. Add T9 rejection note. Keep existing page only.

## Existing page
URL: `/blogs/how-to-fix-trust-issues`
Published: 2026-07-07
Status: PUBLISHED (confirmed in tracking-db)

## Proposed brief
File: `briefs/NEW-how-to-deal-with-trust-issues-brief.md`
Not shipped — held by Verifier §3 NEEDS_HUMAN verdict.

---
## ✅ RESOLVED 2026-07-17 — Kushal decision: (c) + strengthen existing
Retire the proposed brief AND fold its unique value into the live page. Executed same session:
- Brief archived → `briefs/archive/NEW-how-to-deal-with-trust-issues-brief.md` (rejection note appended)
- Enrichment refresh created → `briefs/REFRESH-how-to-fix-trust-issues-enrichment-brief.md` (2 new PAA FAQs, deal-with/overcome keyword layer, attachment-therapy mention, coping-vs-fixing framing) — **HOLDS until 2026-08-18** (42d window) unless day-21 midpoint shows NEEDS_HELP
- tracking-db: NEW-/blogs/how-to-deal-with-trust-issues → RETIRED_MERGED
- Rule reinforced for T5/T3: verb-variant intent twins = one cluster, one page

---
## ⚠️ 2026-07-30 — DUPLICATE ESCALATION (Kushal delegated; Claude resolved)

**This decision was already made and executed on 2026-07-17.** The 2026-07-28 Verifier
NEEDS_HUMAN verdict and the 2026-07-29 T11 Slack escalation (ts 1785323469.310759) asked
for an A/B/C call that had been answered 11 days earlier.

**DECISION: (c)+ STANDS — no change.** Verified state is already correct:
- `NEW-how-to-deal-with-trust-issues-brief.md` IS in `briefs/archive/` (not in the active queue)
- `REFRESH-how-to-fix-trust-issues-enrichment-brief.md` exists and HOLDS until 2026-08-18 (42d window)
- Live page `/blogs/how-to-fix-trust-issues` (2026-07-07) remains the single page for this cluster

**No further action required. Do not re-escalate.**

### Process defect this exposed (worth fixing)
T11 enforces a 2-action cap. On 2026-07-29 both slots were consumed by flag_for_human
escalations — this one (already resolved) and T17-7-REVIEW — which caused
**YOGA-FOR-ANXIETY-SHIP-01 to be SKIPPED**. A redundant escalation displaced real content work.

**Guard to add:** before T11 raises a flag_for_human, check
`brain/needs-human-review/<packet>/README.md` for an existing `## ✅ RESOLVED` block.
If one exists and the resolution has been executed, close the item silently instead of
re-escalating and do not consume an action slot.
