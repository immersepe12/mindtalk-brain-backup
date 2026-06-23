# Pattern: Sprint C — CTR meta-rewrite, top-20 high-impression pages (14-day result)

**Closed:** 2026-06-23 (Learner)
**Sprint shipped:** 2026-06-09 (commit `7c3c2c4`, branch `feat/ctr-meta-rewrite-top-20-2026-06`)
**Watch:** W10
**Hypothesis:** A meta-title + meta-description rewrite on the top-20 pages by impression/opportunity score lifts CTR (from a ~0.4–0.8% cluster average toward 1.5–2%) **without new body content**, because only the snippet changed — so position should stay roughly stable while CTR rises. Target outcome: +400–680 clicks/wk (W10 stretch: +2,180/wk).

**Verdict: 4 GREEN / 8 YELLOW / 8 RED → hypothesis DISCONFIRMED as a blanket tactic.**
But a clean, actionable *conditional* pattern emerged — the rewrite **style** decides the outcome (see "The real finding").

---

## Windows
- **Baseline (pre-ship):** 2026-06-01 → 2026-06-07 (7 days, fully before the 06-09 rewrite)
- **Current (post-ship):** 2026-06-15 → 2026-06-21 (7 days, day-of-week aligned, 6–12 days after ship, inside GSC's reliable horizon)
- Page-level GSC totals (no query dimension) = true page CTR. Pulled live 2026-06-23.

## Aggregate
| Metric | Baseline | Current | Δ |
|---|---|---|---|
| Total clicks / wk (20 pages) | 321 | 309 | **−12** |
| Total impressions / wk | 70,830 | 71,596 | +766 (+1.1%, flat) |
| Impression-weighted CTR | 0.453% | 0.432% | **−0.022 pp** |
| Simple-mean CTR delta | — | — | −0.013 pp |

Impressions held flat (+1.1%) — so this *was* a clean test of the CTR lever, and the cluster CTR did **not** rise; it fell slightly. The +2,180 and +400–680 clicks/wk targets were missed (actual −12/wk).

**Anti-pattern alert:** 8 of 20 pages went RED (CTR dropped after rewrite) — exceeds the >5 RED spike-detection threshold → **flagged for Meta-Learner.** Sprint C is itself a textbook instance of **AP1** (bulk-rewrote 20 ranking pages in one shot, no staged 10% sample). The 8 RED pages are the evidence AP1 exists to prevent. See "Process learning."

---

## Per-URL results

| Verdict | Page | CTR Δ (pp) | Clicks (b→c) | Impr (b→c) | Pos Δ | Note |
|---|---|---|---|---|---|---|
| 🟢 GREEN | /blogs/understanding-the-hamilton-anxiety-rating-scale | **+0.314** | 61→67 | 4,053→3,683 | −0.6 | dropped filler, front-loaded keyword, +"Explained" |
| 🟢 GREEN | /blogs/guide-to-stop-overthinking-and-anxiety-naturally | +0.173 | 8→14 (+75%) | 3,742→3,616 | −1.1 | added number "8 Steps" |
| 🟢 GREEN | /blogs/yoga-for-anxiety | +0.180 | 8→12 (+50%) | 2,480→2,386 | −0.1 | number "7 Poses" + hook "That Actually Work" |
| 🟢 GREEN* | /doctors/psychiatrists | +0.363 | 0→4 | 1,833→1,103 | +4.4 | *soft: low base, rank worsened → set MONITOR |
| 🟡 YELLOW | /blogs/understanding-dry-begging-… | +0.221 | 41→27 (−34%) | 13,579→5,159 (−62%) | +0.2 | CTR rise = long-tail shedding, not engagement |
| 🟡 YELLOW | /illnesses/relationship-issues | +0.084 | 2→2 | 1,949→1,068 | −3.4 | low base; rank-driven |
| 🟡 YELLOW | /treatments/eclectic-therapy | +0.034 | 2→2 | 2,065→1,526 | +1.2 | low base; flat |
| 🟡 YELLOW | /doctors/psychiatrists-in-bangalore | +0.029 | 21→27 (+29%) | 2,932→3,624 (+24%) | −3.0 | clicks rode rank/impr, not meta |
| 🟡 YELLOW | /blogs/10-essential-steps-…-inner-peace | +0.011 | 18→21 | 5,006→5,666 | −0.2 | CTR flat; clicks rode impr |
| 🟡 YELLOW‡ | /blogs/20-quotes-to-inspire-healthy-relationships | −0.060 | 12→14 | 2,527→3,373 | +2.3 | ‡CONFOUND: same-day Sprint B body rewrite |
| 🟡 YELLOW‡ | /blogs/understanding-dominant-personality-… | −0.061 | 18→36 (+100%) | 6,735→17,446 (+159%) | 0.0 | ‡CONFOUND: Sprint B interactive tool |
| 🟡 YELLOW‡ | /blogs/emotional-distress-all-you-need-to-know | −0.276 | 8→10 | 1,227→2,660 (+117%) | +1.3 | ‡CONFOUND: Sprint B impr flood diluted CTR |
| 🔴 RED | /blogs/understanding-the-techniques-for-calming-a-panic-attack | −0.078 | 7→6 | 2,926→3,733 | +1.5 | rank slipped |
| 🔴 RED | /treatments/counselling-therapy | −0.094 | 12→4 (−67%) | 3,786→1,797 | −0.1 | impr also −52% |
| 🔴 RED | /blogs/trust-issues-signs-and-causes | −0.110 | 9→5 (−44%) | 4,174→4,707 | −0.9 | title blander ("Overcome"→"Heal") |
| 🔴 RED | /treatments/rtms-therapy | −0.113 | 26→21 (−19%) | 3,362→3,184 | −0.2 | **intent-swap → geo-commercial** |
| 🔴 RED | /blogs/exploring-reasons-and-effects-of-divorce-in-india | −0.127 | 33→17 (−48%) | 4,116→2,519 | +0.6 | **de-numbered ("Top 11"→none)** |
| 🔴 RED | /illnesses/dementia | 0.000 | 0→0 | 91→153 | +0.3 | snippet problem, not copy (pos ~2.7, 0 CTR) |
| 🔴 RED | /blogs/types-of-family-therapy | −0.357 | 2→0 | 561→136 (−76%) | +5.3 | **de-numbered ("7 Approaches"→none)** + rank loss |
| 🔴 RED | /treatments/drug-deaddiction | **−0.402** | 33→20 (−39%) | 3,686→4,057 | +1.4 | **intent-swap → geo-commercial** |

‡ = page also received a same-day Sprint B body rewrite (06-09) → meta-only attribution is inconclusive; these were already closed separately as W7 GREEN / W8 GREEN / W9 YELLOW.
\* = rule-GREEN on the +0.3pp CTR criterion but low base (0→4 clicks) with worsening rank → tracked as MONITOR, not RESOLVED.

---

## The real finding — rewrite **style** decides CTR, not the act of rewriting

The 3 best and 3 worst rewrites split on three concrete title levers. This is the value of the sprint.

**Top 3 winners (what they did):**
1. **hamilton-anxiety (+0.314pp).** `Understanding the Hamilton Anxiety Rating Scale (HAM-A) ` → `Hamilton Anxiety Rating Scale (HAM-A) Explained | Mindtalk`. Removed the filler "Understanding the", **front-loaded the exact keyword**, added a credibility token "Explained" + brand.
2. **guide-to-stop-overthinking (+0.173pp, clicks +75% on flat impr).** `How to Stop Overthinking and Anxiety Fast ` → `…: 8 Steps | Mindtalk`. **Added a specific number** ("8 Steps").
3. **yoga-for-anxiety (+0.18pp, clicks +50% on flat impr).** `Yoga for Anxiety: Top Poses for Stress Relief ` → `Yoga for Anxiety: 7 Poses That Actually Work | Mindtalk`. **Added a number** ("7 Poses") **+ a curiosity/credibility hook** ("That Actually Work").

**Top 3 losers (what they did — mirror image):**
1. **drug-deaddiction (−0.402pp, worst).** `Drug Deaddiction: Types, Benefits, and How it Works - Mindtalk` → `Drug De-Addiction Treatment in Bangalore | Mindtalk`. **Intent-swap:** an informational title became a narrow **geo-commercial** one, on a query whose GSC demand is national + informational. Snippet/intent mismatch → CTR crash.
2. **types-of-family-therapy (−0.357pp).** `…: 7 Approaches Explained | Mindtalk` → `…: Which One Is Right for You? | Mindtalk`. **De-numbered** (dropped "7 Approaches") and dropped "Explained" — deleted the exact two tokens the winners *added*. (Also lost rank, pos 5.8→11.1, which compounds it.)
3. **divorce-in-india (−0.127pp).** `Top 11 Reasons for Divorce in India & Their Effects` → `Divorce in India: Causes, Effects & Recovery`. **De-numbered** (dropped "Top 11") — removed the listicle hook.

**The differentiator is not character length or emotional tone — it is three specific levers:**
| Lever | Winners | Losers |
|---|---|---|
| Specific number in title ("8 Steps", "7 Poses") | **added** | **removed** ("Top 11", "7 Approaches") |
| Credibility / curiosity token ("Explained", "That Actually Work") | **added** | **removed** |
| Search intent (informational ↔ commercial) | **preserved** | **swapped** to geo-commercial ("…in Bangalore") on national informational queries (rtms, drug-deaddiction) |

rtms-therapy independently corroborates the intent-swap mechanism (same `… in Bangalore` move, −0.113pp). trust-issues corroborates the "blander = worse" direction ("Overcome"→"Heal", no number/hook added, −0.11pp).

**Even controlling for rank:** restricting to pages whose position moved ≤±1.0pp, the winners (hamilton, yoga) and losers (trust, counselling, rtms, divorce) keep the same CTR split — so the divergence is driven by the copy levers, not by rank movement. types-of-family is the one RED where rank loss (−76% impr) genuinely confounds the meta read.

---

## What this means for Sprint C v2 (next-20 batch)
1. **Keep the win formula, kill the loss formula.** Rewrite rule: front-load the exact keyword; **add a specific number** where the page is a list/steps page; add one credibility/curiosity token ("Explained", "That Actually Work", "…Backed by…"); **never delete an existing number**; **never convert an informational title to "[X] in Bangalore"** unless GSC shows the query is itself local-commercial.
2. **Retire (revert) the 4 clean copy-losers' new titles:** drug-deaddiction, rtms-therapy (intent-swap), divorce-in-india, types-of-family (de-numbered). Queued NEEDS_REFRESH.
3. **dementia is not a copy problem** — pos ~2.7 with 0 clicks = AI Overview/featured-snippet eating the click. Route to human review / AIO-defense (P2/P10), not a meta refresh.
4. **Ship staged, not bulk (AP1).** The next 20 must go out as a 10% sample (2 pages) with a 7-day CTR read before the rest — Sprint C's 8 RED is exactly what AP1 was written to catch.

## Process learnings (→ rules)
- **A meta rewrite is not free upside.** ~Half the pages dropped CTR; the cluster net-lost clicks. "Rewrite the top 20 by impressions" with an inconsistent style guide is a coin-flip. The lever that pays is *number + specificity + intent-match*, applied selectively — not bulk rewriting.
- **Confounding:** 3 of the 20 (20-quotes, emotional-distress, dominant-personality) got a same-day Sprint B body change. Never co-ship two experiments on one URL on one day — it cost clean attribution on 3 high-impression pages. (Add to scheduling discipline.)
- **Judge meta-only tests on page-level CTR at flat impressions/position.** Pages where impressions or rank moved a lot (dry-begging −62% impr, dominant +159% impr, types-of-family +5.3 pos) can't credit/blame the meta — segregate them before reading the verdict.

## Treatment → outcome summary
| Title move | Pages | CTR effect |
|---|---|---|
| Add specific number ("8 Steps", "7 Poses") | guide-overthinking, yoga | ✅ + clicks +50–75% on flat impr |
| Front-load keyword + drop filler + "Explained" | hamilton | ✅ +0.314pp on a high-base page |
| Remove an existing number | divorce, types-of-family | 🔴 −0.13 / −0.36pp |
| Swap informational → geo-commercial ("…in Bangalore") | drug-deaddiction, rtms | 🔴 −0.40 / −0.11pp |
| Cosmetic reword, no number/hook | trust-issues, counselling, calming-panic | 🔴 flat-to-down |
| Meta change on a snippet-starved top-3 page | dementia | ⚫ 0 clicks — wrong lever (AIO problem) |
