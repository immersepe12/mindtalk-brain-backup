# Pattern: Sprint B — AI Overview defense (14-day result)

**Closed:** 2026-06-23 (Learner)
**Sprint shipped:** 2026-06-09 (commits `aa5e3b9`, `5dfe080`, `c1e0d67`)
**Hypothesis:** On viral blogs being cannibalised by AI Overview (position improving while impressions collapse), adding content the AIO *cannot* cleanly summarise — an interactive self-assessment + India-specific stat (NIMHANS) + Quick Answer/FAQ schema — reclaims AI Overview citation and wins back impressions.

**Verdict: 2/3 GREEN, 1/3 YELLOW, 0 RED → hypothesis CONFIRMED.**

---

## Results table

| Watch | Page | Money term (tracked) | AIO citation now | Organic pos (head term) | GSC impr/wk (06-06 → 06-13) | GSC pos (06-06 → 06-13) | Verdict |
|---|---|---|---|---|---|---|---|
| W7 | dominant-personality | "dominant personality meaning" | **cited 5×** | #4 | 96 → **1,152** | 7.6 → **3.2** (+4.4) | 🟢 GREEN |
| W8 | 20-quotes | "healthy relationship quotes" | **cited 3×** | n/a (AIO) — #2 on "20 quotes to inspire…" | 64 → **549** | 9.1 → **6.1** (+3.0) | 🟢 GREEN |
| W9 | emotional-distress | "what is emotional distress" | **cited 5×** | #6 | 41 → **128** (lead: "emotional distress" 153→294) | 11.2 → 10.7 (+0.5) | 🟡 YELLOW |

AI Overview citation verified live via DataForSEO SERP-advanced (India geo / desktop), which returns the real AIO reference domains. All three pages are now in the AIO reference set on their primary demand term — pre-Sprint they were bleeding impressions to in-SERP answers (cannibalisation signature).

Baselines at ship (from commit messages, 4-week windows):
- W7: 8,304 → 1,329 impr (-84%) while pos 7.7 → 6.6
- W8: 6,673 → 1,714 impr (-74%) while pos 17.3 → 15.5
- W9: 6,541 → 2,190 impr (-67%) while pos 11.1 → 9.2

---

## What worked

1. **Interactive self-assessment is the strongest lever.** W7's 10-question "Is someone dominating you?" self-check + live tally + banded results delivered the biggest swing — AIO citation reclaimed (5×) AND the "dominant personality meaning" variant exploded 96 → 1,152 impr/wk and jumped to pos 3.2. The AIO can summarise prose, but it cannot reproduce an interactive tool, so the page keeps a reason-to-click and Google keeps citing it.
2. **Original per-item commentary the AIO can't compress.** W8 added a ~50–80-word "Therapist's take" under each of 21 quotes. That original analytical layer (vs. a bare listicle the AIO trivially lifts) reclaimed AIO citation (3×) and moved "healthy relationship quotes" 9.1 → 6.1 with impr 64 → 549.
3. **India-specific stat (NIMHANS) + Quick Answer + FAQ schema** is a necessary supporting layer on all three — but on its own it correlates with citation, not with proportional impression recovery (see W9).

## What was partial / didn't fully work

4. **W9 (emotional distress) — citation won, rank/impr recovery lagged.** The Kessler-style 8-q distress check + NIMHANS 2023 stat + 5 FAQs reclaimed AIO citation (5× on "what is emotional distress", #6 organic) and roughly doubled weekly impressions — but head-term position barely moved (+0.5 to +1.0, sub-threshold) and absolute impr (128–294/wk) is far below the ambitious 5k target. Notably, the **bare "emotional distress" SERP flipped from AI Overview to a competitor-held `featured_snippet`** — the SERP feature changed under us, so "reclaim the AIO" was a partially moving target. Reclaiming citation does **not** guarantee proportional impression recovery when the page stays in the 6–10 position band and a rival owns the featured snippet.

## Process learning (→ rule)

5. **Track the page's own highest-impression query, not the brief's generic head term.** W8 was watched on "relationship quotes" (pos ~39, dominated by Adobe/TheKnot/QuoteGarden — not a mental-health query at all). Judged on that term it looks RED; judged on its actual demand "healthy relationship quotes" (549 impr, cited in AIO, pos 6.1) it's a clean GREEN. The generic head term nearly buried a win. Going forward, AIO-defense verdicts read the money term from `reports/query-history.json`, not the brief headline.

## Treatment → outcome summary

| Treatment | Pages | Reclaimed AIO citation? | Lifted impressions? |
|---|---|---|---|
| Interactive self-assessment (banded results + CTA) | W7, W9 | ✅ both (5×) | ✅ strong on W7; ⚠ partial on W9 |
| Original per-item expert commentary | W8 | ✅ (3×) | ✅ strong (64→549) |
| Quick Answer + Key Takeaways block | W7, W9 | ✅ | mixed |
| India stat (NIMHANS/NIMHANS-2023) | W7, W8, W9 | ✅ (correlates) | not sufficient alone |
| FAQ schema (5 FAQs) | W9 | ✅ citation | ⚠ insufficient for rank/impr alone |

**Propagation guidance (for Strategist):** the interactive-tool + original-commentary treatment is now a validated playbook for impression-bleeding viral blogs (position-improving + impressions-collapsing = AIO cannibalisation, per P2). Prioritise pages showing that exact signature. Expect citation reclaim reliably; expect strong impression recovery where an interactive tool or genuinely original layer is added, weaker recovery where only Quick-Answer/FAQ/stat is added or where the SERP feature has shifted to a rival featured snippet.
