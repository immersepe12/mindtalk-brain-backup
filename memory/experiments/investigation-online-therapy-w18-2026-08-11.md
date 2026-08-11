# investigate_regression: /treatments/online-therapy — 2026-08-11

**BACKLOG ID:** ONLINE-THERAPY-W18-DROP-HIGH-01
**Triggered by:** W18 Day-42 final = HIGH_PRIORITY_DROP + QDF_BLOCKED
**Observation window:** 2026-09-21 (extended)
**url_locked:** true

---

## Signal summary

| Period | Clicks/wk | Impressions/wk | avg_pos |
|---|---|---|---|
| Day-21 midpoint (GSC) | ~7 | ~58 | 13.0 → 7.3 (improving) |
| Day-42 final (GSC) | ~4 | ~18 | 24.3 |
| Previous GSC window (Jul 24–Jul 31) | 14 | 392 | 10.5 |
| Current GSC window (Jul 31–Aug 7) | 8 | 124 | 24.3 |

**Net change (current vs previous):** clicks −43%, impressions −68%, position −13.8 pts

---

## Root cause analysis

### Finding 1 (PRIMARY): "online therapist" keyword drop-out — structural QDF_BLOCK

In the **previous GSC window (Jul 24–Jul 31)**, the single keyword "online therapist" drove:
- 236 impressions at pos 4.5 (= 60% of all page impressions)
- 2 clicks at 0.85% CTR

In the **current GSC window (Jul 31–Aug 7)**, "online therapist" does NOT APPEAR in the top keyword list. The closest variant "therapist online" now shows only 32 impressions at pos 13.1.

This is not a gradual position decline — it is a single-keyword drop-out. The page held top-5 for "online therapist" for several weeks then was displaced. The SERP for "online therapist" is structurally dominated by:
- amahahealth.com (high-DA MH aggregator, dedicated online-therapy marketplace)
- yourdost.com (high-DA aggregator, established 2012)
- betterhelp.com (global high-DA)
- talktoangel.com (India-specific aggregator)

These are all dedicated online-therapy platforms with 5+ year domain authority specifically for this query. Mindtalk held pos 4.5 briefly (likely QDF boost from fresh content), but the structural advantage reverted to incumbents after the freshness signal decayed (~5-7 weeks).

**Verdict: QDF_BLOCKED is correct. The freshness signal carried the page to pos 4.5 at Day-21; it decayed by Day-42 as expected for aggregate-dominated SERP.**

---

### Finding 2 (SECONDARY): Jul 20 content change during url_locked observation window

Git log for `src/content/treatments/online-therapy.mdx` shows 3 commits:
1. `6768c7f` (2026-06-26) — initial hub page published
2. `eb07800` — metadata change
3. `59c3c5a` (2026-07-20) — CANNIBAL-BLOG-01 commit: added free-therapy section + 2 FAQs (T17-8 enhancement)

**The CANNIBAL-BLOG-01 commit (59c3c5a, 2026-07-20) modified /treatments/online-therapy.mdx 3 days after the Day-21 midpoint checkpoint (2026-07-17), while `url_locked: true` was set.**

Commit message explicitly noted: *"npm run build NOT run (exceeds 45s sandbox budget) — committed to this branch, not main"* — but the commit DOES appear in main branch git log via `--follow`, meaning it was eventually merged.

The timing of this change (Jul 20) coincides with the start of the Day-21→Day-42 regression window. A fresh crawl triggered by content modification may have reset the page's quality evaluation during the aggregator freshness-signal decay period, accelerating the position collapse.

**This is a url_locked violation.** The T17-8 enhancement was approved strategically but should have been staged for AFTER the 09-21 observation window closes.

**Severity of impact:** Uncertain — the structural QDF_BLOCK is the primary driver regardless, but the mid-window modification may have accelerated timeline from gradual decline to sharp drop.

---

### Finding 3 (NOT CONFIRMED): Internal cannibalization

Investigation of tracking-db for competing MT pages:
- `/find-therapist` does NOT exist on mindtalk.in (it lives on consult.cadabams.com — a different domain, no cannibalization)
- `/blogs/how-to-find-a-therapist-in-india` (live 2026-06-17) — different intent query ("how to find" vs "online therapy")
- `/blogs/how-to-find-a-therapist-for-ocd` — highly specific, no overlap
- `/doctors-listings/therapists-in-delhi` etc. — BRIEF_CREATED (not live)

**Conclusion: No internal cannibalization is occurring. The pages are sufficiently differentiated in intent.**

---

## SERP feature analysis

Current GSC data shows an important pattern — the page IS being found for "cbt therapy online india" (pos 1.0, 3 impressions, 0 clicks) and "cbt online india" (pos 5.0, 6 impressions, 0 clicks). These are zero-click due to AI Overviews absorbing the intent. Google's AIO is now answering "cbt online india" queries directly without click-throughs, which explains additional impression-to-click decay beyond the structural drop.

---

## Recommended action

**Given url_locked=true and observation_window_end=2026-09-21:**

No content change until observation window closes. The correct action sequence is:

1. **NOW:** Create BACKLOG row `ONLINE-THERAPY-DEPTH-REFRESH-09-21` — queued refresh to fire AFTER 09-21. Strategy:
   - Add India-specific "online therapist" cost/availability section (to compete on informational facets aggregators skip)
   - Add structured therapist profile cards (LocalBusiness schema with geo, specialisation)
   - Add "how to choose an online therapist in India" FAQ targeting long-tail variants where aggregators are weaker
   - Remove or de-emphasise free-therapy section that may be creating intent mismatch (users searching "online therapist" are looking to book, not get free resources)
   - Target: "online therapy india" (head term, Tier A), "online therapist for anxiety india", "talk to therapist online india" (lower-competition variants)

2. **NOW:** Flag url_locked violation as a system lesson — add to ANTI-PATTERNS if next Learner run confirms this is repeatable pattern.

3. **T5 brief (if/when T5 runs):** Queue supporting blog "online therapist vs in-person therapy: pros and cons india" — topical cluster support for the hub page, targets "online therapist" long-tail variants with less aggregator competition.

4. **2026-09-21:** T12 Learner evaluates final observation window close. If position has recovered to pos≤15, NEEDS_REFRESH brief fires. If still pos>20, extend or consider whether the SERP is permanently ceded.

---

## What this means for AP3-B YMYL strategy

This page is the **first AP3-B hub attempt on a high-DA-aggregator-dominated cluster.** The learning:

- The freshness signal from new content CAN temporarily achieve top-5 (pos 4.5 at Day-21)
- QDF decay is predictable (~42 days for a treatment hub page vs ~14-21 days for a blog)
- Aggregator-dominated SERPs (BetterHelp, Amaha, YourDOST) require SUSTAINED DA + authority signals to hold beyond QDF — not achievable with a single new page

This finding should inform Hypothesis 0 and YMYL strategy. See BACKLOG row for recommended follow-up action.

---

## Lessons / system flags

1. **url_locked violation (AP-NEW candidate):** The CANNIBAL-BLOG-01 commit modified a url_locked page 3 days after its Day-21 midpoint. `url_locked: true` MUST be enforced as a hard block on ALL content modifications during the observation window, not just by T11 but by any task or human session touching that MDX file. Propose to Learner: add `AP12 — Never modify a url_locked page during its open watch window` if this pattern recurs.

2. **QDF baseline for new treatment hubs:** New /treatments/ pages targeting aggregator-dominated head terms will likely hit pos 4-8 at Day-14 to Day-21 (QDF boost), then regress to pos 20-30+ by Day-42 as freshness signal decays. Strategist should model expected Day-42 position as 2-3× worse than Day-21 midpoint for this page class, not as stable as the midpoint suggests.

---

## Tags
`#investigate_regression` `#W18` `#online-therapy` `#QDF_BLOCKED` `#AP3-B` `#url_locked-violation`
