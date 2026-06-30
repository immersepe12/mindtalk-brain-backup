# investigation_regression: burnout-treatment — 2026-06-30

**Triggered by:** BACKLOG #21 (CRITICAL), W22 opened 2026-06-29 by Strategist.
**Type:** Read-only AP5 spike check + cannibalization diagnostic.
**Verifier verdict:** APPROVE (2026-06-30, agent a2d1808d90d5e669c).
**Constraint:** ALGO_WATCH active through 07-02. No content action taken.

---

## What we investigated

Weekly summary Jun 20-26 flagged "burnout treatment" as a CRITICAL position drop:
- Reported: pos 6.8 → 85.9 (-79.1 positions)
- URL: `/blogs/burnout-treatment`
- Page published: 2026-05-18 (42 days before today)
- Reviewer: dr-akanksha-bhor

Two hypotheses to test:
1. **AP5 QDF spike** — was pos 6.8 a freshness boost for a newly published page?
2. **Cannibalization** — is the 184KB guide-to-burnout-syndrome.mdx suppressing this page?

---

## What we found

### AP5 Spike Check — CONFIRMED QDF NORMALIZATION

Timeline of events:
- Published: 2026-05-18
- Peak position 6.8 observed: Jun 13-19 (days 26-32 post-publish)
- Position collapse to 85.9: Jun 20-26 (days 33-39 post-publish)

**Verdict: HIGH CONFIDENCE QDF spike.** Day 26-32 is the textbook QDF (Query Deserves Freshness) window. Google routinely boosts newly published content into top-10 for 3-5 weeks while crawling/evaluating quality, then normalizes once the freshness signal decays. The timing is precise: peak at day 26-32, collapse at day 33-39. This is not a ranking regression — it is standard QDF decay.

**AP5 rule applies:** The prior week's value (pos 6.8) was a temporary spike above the page's organic baseline. Per AP5, do NOT treat normalization as a real drop warranting content action.

---

### Cannibalization Diagnostic — PRESENT but SECONDARY

**Sibling burnout pages (all indexed, competing for the cluster):**

| Page | Published | Size | Pos (Jun 20-26) | Notes |
|---|---|---|---|---|
| guide-to-burnout-syndrome.mdx | 2025-08-21 | 184,817 bytes | **7.1** (page 1) | 10 months old; 30-min read; H2 "Treatment Options for Burnout" covers CBT explicitly |
| burnout-recovery-prevention-guide.mdx | 2026-01-14 | 9,845 bytes | **9.1** (page 1) | 5.5 months old; covers causes, prevention, recovery |
| burnout-treatment.mdx | 2026-05-18 | 9,653 bytes | 85.9 (not ranking) | 7 weeks old; post-QDF decay |
| how-to-manage-emotional-burnout.mdx | 2026-05-18 | 9,805 bytes | not tracked | same publish date as burnout-treatment |

**Key finding:** `guide-to-burnout-syndrome.mdx` (184KB, Aug 2025) has an explicit **"## Treatment Options for Burnout"** section that covers CBT, lifestyle changes, and recovery — the same territory as burnout-treatment.mdx. Google has chosen the 10-month-old monster guide (pos 7.1) as the dominant cluster page because it is more authoritative (older, 19x larger, better E-E-A-T signal from extended history).

The cannibalization is real and structural, but it is a **pre-existing condition**, not the cause of the pos 6.8→85.9 "drop." The drop was QDF decay. The cannibalization explains why burnout-treatment has no independent organic floor after QDF expired.

---

## What we did NOT do

- No content refresh (ALGO_WATCH active; AP4 safety pause)
- No brief created (QDF normalization, not a Core Update regression)
- No tracking-db change (burnout-treatment is `BRIEF_CREATED` status — this is correct)

---

## Recommended action

**DO NOT add burnout-treatment to #18 YMYL recovery batch.**

Reasoning:
1. The "drop" is QDF normalization, not a Core Update demotion — the #18 batch is for confirmed Core Update casualties (ptsd, alzheimers, drug-addiction). burnout-treatment was never a Core Update casualty.
2. Search volume is 244/mo (low) — below the threshold for high-priority recovery sprints.
3. burnout-treatment.mdx is a thin page (9.6KB) competing against a monster guide (184KB) on the same query intent. A generic refresh won't move the needle — the page needs **differentiation**, not just a content bump.

**Future action (post-07-14):**
Once organic floor position is established (~4-6 weeks post-QDF = mid-July), assess whether burnout-treatment can find a differentiated ranking niche:
- Target specific sub-queries: "CBT for burnout India," "burnout therapy cost India," "workplace burnout treatment steps"
- Differentiate from guide: DO NOT cover general burnout signs/stages/prevention (the monster guide owns those); focus exclusively on the therapeutic pathway (what therapy looks like session-by-session, what to expect, India-specific context)
- This is a sprint-type action for Strategist to queue in July; NOT urgent

**For the cluster AP5 check on high drops (relationship-problem, psychosis, bangalore geo):**
Same AP5 lens applies. Hold all under ALGO_WATCH per existing BACKLOG guidance. The Bangalore geo drops are genuine P9 priority but action is gated to 07-02+.

---

## BACKLOG update

- **#21 (investigate_regression burnout-treatment):** COMPLETED — QDF normalization confirmed, no content action needed, no #18 inclusion.
- **W22 status update:** 🟡 QDF CONFIRMED — MONITOR (not a regression; no watch follow-up; monitor organic floor mid-July)

---

## Expected outcome

- Short-term: no content action, no ranking change
- Mid-term (07-14): once QDF fully settled, assess organic floor. If page settles below pos 50, differentiation sprint in Q3 2026 backlog (low priority vs #18 and ADHD hub).
- Learning: validate that tracking page launches with QDF spike detection — a pos 6.8 reading on day 26-32 for a new /blogs/ page should auto-flag as likely-QDF before adding to CRITICAL drop queue.

---

## Tags

#burnout #qdf-spike #cannibalization #ap5 #no-action
