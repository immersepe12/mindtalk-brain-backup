# Investigation: /treatments/life-coach-therapy — 2026-06-17

**Trigger:** BACKLOG #6 `investigate_regression`. Round-1 content refresh (commit `58b7e39`, 2026-05-28) evaluated RECOVERY_FAILED/PARTIAL on 2026-06-11 — primary query "what is a life coach" went from 10.6 → not-in-top-100. Hypothesis to test (P2): position-up-impressions-down = AI-Overview cannibalisation, not quality.
**Action type:** Read-only diagnostic (no MDX edit, no 301, no push). Verifier verdict: **APPROVE** (2026-06-17).
**Today:** 2026-06-17. Target last modified 2026-06-09 (`270cf0c`, bulk reviewer add) → 8 days ago, inside AP4 14-day pause; also in algo_watch "Held this cycle"; RECOVERY_PARTIAL watch open to 06-25.

## What's the actual signal?

**Not a regression. This is a CTR/eligibility story on a page that is growing strongly.**

Two data sources, same conclusion:

1. **GSC (capped keyword export, pulled 06-04):** page signal = **IMPROVING**. Clicks 1→3 (+200%), impressions 233→283 (+21.5%), avg position flat ~18.7→18.9. Commercial + condition queries rank well: "life coach for anxiety" 6.1, "life coach for anxiety and depression" 6.3, "life coach for depression and anxiety" 6.0, "life coach counsellor" 8.7, "life coach in bangalore" 11.6, "life coach bangalore" 10.7. Generic definitional head terms are weak or absent: "life coach" pos 22.5 (84 impr, 0 clicks), **"what is a life coach" = absent from both windows (zero impressions)**.

2. **cluster-history (DataForSEO weekly ranked-keyword footprint):** strongly **EXPANDING**. Query footprint 95 (04-18) → **172 (06-06)**; avg position improving 11.1 → **10.8**; ranked-keyword pool growing week over week. Clicks/CTR remain ~0 throughout. (Note: cluster-history "impressions" run ~15× the GSC export — it tracks ranked-keyword search-volume footprint, not GSC actual impressions; trend direction is what matters, and it is up-and-to-the-right.)

## Root cause

- **"what is a life coach" is an intent/eligibility loss, NOT a recoverable ranking drop.** It had **zero impressions even in the May 11–25 window** — the loss *pre-dates* the round-1 refresh, so the refresh did not cause it (confirms the 06-11 recovery brief). The generic definitional SERP in India is now served by AI Overview + global authority (Tony Robbins, BetterUp, Coursera, Indeed). A Bangalore therapy-provider page is no longer eligible for that head term. The 10.6 baseline was a transient/stale GSC artifact. → **This matches P2's "position-up-impressions-down" only loosely; more precisely it is permanent SERP-eligibility loss on one head term, against a page that is otherwise gaining.**
- **The real picture:** the page is one of the site's better topical-authority growth stories (footprint +81% in ~7 weeks, position holding top-of-page-2 / borderline page-1) but it converts at **~0% CTR**. That is the CTR axis — the #1 Q3 priority — not a regression to chase.

## Recommended action

1. **Retire "what is a life coach" as the primary keyword for this URL.** It is not recoverable; stop treating it as a drop. (keyword-map update — data/metadata only, NOT a content change.)
2. **Reclassify the page as a CTR/position-harvest candidate**, not a regression target. Lever = title/meta rewrite toward its real demand ("life coach meaning" pos ~6.4 / 203 impr / 0 clicks per the 06-11 brief; plus the strong "life coach for anxiety/depression" and "life coach bangalore" commercial cluster) + a small position nudge from ~11 → top-10.
3. **Do NOT act on content this cycle.** Blocked by three independent gates: AP4 14-day pause (last touch 06-09), algo_watch "Held this cycle" (core update receding, resume ~06-23), and the open RECOVERY_PARTIAL watch (recheck 06-25). Queue the meta/title test **ready after 06-25**.
4. **Keep "life coach for anxiety and depression" untouched** — recovered to target (6.1), do not disturb.

## Effect on BACKLOG

Row #6 `investigate_regression` is **resolved**. Replaced in place with a deferred CTR/position meta-test row, ready after the 06-25 watch close, low blast radius (meta/title), Strategist to score against P9 conversion tiers and decide priority. No re-ordering of other rows.

## Notes / data caveats

- GSC export (≈50 keywords) vs cluster-history (159–172 keywords) diverge ~15× on impression magnitude — different instruments (actual GSC vs DataForSEO footprint). Trend agreement (both up) is the reliable read; absolute impression numbers from cluster-history should not be quoted as GSC impressions.
- Round-1 was a *content* fix; this was a *diagnostic*. No repeat-intervention (§8 clause clear, per Verifier).
- PII: aggregated keyword/impression/position data only — no emails, phones, or user-ids.
