# PRINCIPLES — Hard-won lessons

**Read by:** Strategist before every decision.
**Written by:** Learner (Task 12) after every closed watch window.

Each entry: principle + evidence + when it applies.

---

## P1. YMYL pages without named clinical reviewer get demoted by Core Updates
- Evidence: 2026-05-25 audit found 30/31 illness + 25/26 treatment pages had no reviewer; cluster bleeders (dementia -82%, alzheimers -88%, PTSD -40%, drug-addiction -38%) all matched this pattern
- Action: every illness, treatment, blog with YMYL content MUST have `reviewer:` frontmatter + visible byline + JSON-LD `reviewedBy: Physician`
- Established: 2026-06-09 via Sprint A (commit `270cf0c`)

## P2. AI Overview cannibalisation can't be fixed by SEO refresh alone
- Evidence: dominant-personality (pos 7.7→6.6 BETTER but -84% impr), 20-quotes (-74%), emotional-distress (-67%) — positions improved while impressions collapsed = textbook AI Overview snippet stealing
- Action: when position improves but impressions drop ≥50% over 4 weeks, the page needs interactive content (self-assessment, matcher, calculator) + unique India-specific stat (NIMHANS, NIMHS-2023, AIIMS) + breadcrumb JSON-LD sitelink schema
- Established: 2026-06-09 via Sprint B
- ✅ **CONFIRMED 2026-06-23 (Sprint B 14-day check):** all 3 treated pages reclaimed AI Overview citation on their money terms (cited 5×/3×/5× in live India-geo AIO) and impressions recovered (96→1,152, 64→549, 41→128 impr/wk). 2/3 GREEN, 1/3 YELLOW. The fix works — but see P10 for the limit. Memo: `memory/patterns/sprint-b-result-2026-06-23.md`

## P3. Per-content-type URL builders > generic wrappers
- Evidence: 2026-05-28 `buildReturnToUrl` was wrapping every CTA in `/login?returnTo=...` which got stripped by consult.cadabams.com auth redirect (verified via `curl -sIL`). Direct URLs preserve the param correctly.
- Action: never wrap with auth-prefix; emit direct destination URLs and let target site handle auth. Use one builder per content type since suffix patterns differ.
- Established: 2026-05-28, commits `e29f4eb` + `255265a`

## P4. The shipping step is the bottleneck, not the brief generation step
- Evidence: 2026-06-15 audit found 51 BRIEF_CREATED vs only 11 PUBLISHED — 22% conversion rate. Cap raise 10→20 didn't help because cap was never the bottleneck
- Action: solve shipping with auto-ship pipelines (Task 9 for NEW blogs, Executor T11 for refreshes after safety pause)
- Established: 2026-06-15

## P5. Cluster-history alerts can produce false-positive CRITICAL from regression-to-mean
- Evidence: "Reduce Stress Daily" cluster reported -92.2% impressions WoW; investigation found 1059 was a single-week spike vs 73/72/110/83 baseline. Position actually improved 11.2→9.9 and CTR went to 3%.
- Action: before treating a cluster-level drop as CRITICAL, check if prior week was >3x median of preceding 4 weeks. If yes, use 4-wk trailing median as comparison, not the spike.
- Established: 2026-06-02

## P6. Refresh briefs need a 14-day safety pause after their target page was last touched
- Evidence: tracking-db shows pages refreshed multiple times in short windows get unstable rank signal; harder to attribute recovery to any single change.
- Action: Strategist checks `last_modified` of target MDX before queuing refresh; if < 14 days, push to next cycle.
- Established: 2026-06-15 (principle-by-design — no negative case yet)

## P7. Algo_watch HOLD is the workflow's way of protecting YMYL during Core Updates
- Evidence: May 2026 Core Update affected E-E-A-T signals; Task 2 flagged many YMYL refreshes with `algo_watch: YES` (4 such briefs in last 14d). Workflow correctly holds them.
- Action: NEVER override algo_watch HOLD unless you have explicit evidence the update has settled (look for cluster-history showing volatility decreasing for >7 days)
- Established: 2026-06-09

---

(Learner appends new principles weekly. Strategist consults this file every run.)

## P9 — Conversion-validated tiers weight Strategist scoring more than impression-only signals (2026-06-16)

**Source:** Kushal's insight + T19 architecture. The loop was optimizing for clicks (proxy) — should optimize for bookings (real).

**Rule:** When Strategist scores actions, conversion-tier classification (Goldmine/Rocket/Leaky/Dead from T19's PAGE-CONVERSION-MAP) carries more weight than raw impressions/CTR signals.

**Specific scoring updates Strategist applies starting 2026-06-17:**

| Signal | Score |
|---|---|
| Action target is a 🟢 Goldmine | +50 |
| Action target is a 🟡 Rocket (traffic-driving action: refresh, internal links) | +30 |
| Action target is a 🟡 Rocket (anything else) | +20 |
| Action target is a 🔴 Leaky Bucket (UX fix / professional input action) | +25 |
| Action target is a 🔴 Leaky Bucket (traffic-growth action) | -30 |
| Action target is ⚫ Dead Weight | -40 |
| Action target unclassified (page not yet in T19's analyzed set) | 0 (no penalty, no boost) |
| GEO bonus: action targets a high-converting state/city | +20 |
| Action matches a confirmed High-Converter Pattern (4+ weeks evidence) | +25 |
| Stated intent_rate "expected impact" exceeds 2x current tier baseline | -20 (impact realism check) |

**Sanity-check via cross-domain validation:** Strategist must also read the validated-revenue layer (real bookings on consult.cadabams.com attributed back to Mindtalk pages). If a page is classified Goldmine on intent but has 0 attributable bookings in 4 weeks, treat as "intent inflated" — score normally but flag for Learner review.

**Why this matters:**
- Strategy now optimizes for the business
- Vanity clicks penalized; conversion-validated investment rewarded
- Geographic insights mean SEO investment goes where Bangalore + tier-1 cities convert

**How to apply:** Before any action's score is finalized, Strategist must read brain/PAGE-CONVERSION-MAP.md, GEO-CONVERSION-MAP.md, and HIGH-CONVERTER-PATTERNS.md. The strategist-signal-feed.md is the digest version Strategist reads first; the full maps are read when scoring a specific action.

## P10 — AI Overview citation is reclaimed by interactive/original content, but citation ≠ guaranteed impression recovery (2026-06-23)

**Source:** Sprint B 14-day check (W7/W8/W9). Refines P2.

**What works (validated):** On AIO-cannibalised viral blogs, the reliable lever for *reclaiming AI Overview citation* is content the AIO cannot cleanly summarise — an **interactive self-assessment** (banded results + CTA) or **original per-item expert commentary**. All 3 Sprint B pages regained AIO citation this way (cited 5×/3×/5× in live India-geo AIO). The strongest impression recovery came from the interactive tool (W7: 96→1,152 impr/wk, pos 7.6→3.2) and original commentary (W8: 64→549, pos 9.1→6.1).

**The limit (new):** Quick-Answer + FAQ schema + India stat **alone** correlate with citation but **not** with proportional impression/rank recovery. W9 reclaimed citation (5×) yet head-term rank moved only +0.5..+1.0 and impressions stayed low — and its bare head term's SERP **flipped from AIO to a competitor `featured_snippet`**. So: reclaiming AIO citation does not guarantee traffic when (a) no interactive/original layer was added, or (b) the page is stuck in the 6–10 band, or (c) a rival owns the featured snippet.

**Rule:** (1) Prioritise the interactive-tool / original-commentary treatment, not FAQ-schema-only, for impression-bleeding pages. (2) **Judge AIO-defense on the page's own highest-impression query** from `reports/query-history.json`, not the brief's generic head term — W8's tracked query "relationship quotes" (pos ~39, non-clinical) nearly buried a clean GREEN that lived on "healthy relationship quotes" (pos 6.1, cited).

## P11 — Meta-rewrite CTR depends on *style*, not the act of rewriting: add a number + credibility token + match intent (2026-06-23)

**Source:** Sprint C 14-day check (W10 — top-20 by impression, commit `7c3c2c4`). Bulk meta-only rewrite. Impressions held flat (+1.1%), so it was a clean CTR test.

**What happened:** 4 GREEN / 8 YELLOW / 8 RED. Cluster clicks **net −12/wk** (321→309), impression-weighted CTR **−0.022pp** (0.453%→0.432%). Target (+400–680/wk; W10 +2,180) **missed**. Rewriting the top 20 with an inconsistent style guide was a coin-flip — wins and losses roughly cancelled.

**The lever that actually moves CTR (validated both directions):**
- ✅ **Add a specific number** to the title where the page is steps/list content — "8 Steps" (+0.173pp, clicks +75%), "7 Poses" (+0.18pp, +50%), both on flat impressions.
- ✅ **Front-load the exact keyword + drop filler + add a credibility/curiosity token** ("Explained", "That Actually Work") — hamilton-anxiety +0.314pp on a high-base page.
- 🔴 **Removing an existing number** kills CTR — "Top 11 Reasons"→none (−0.127pp), "7 Approaches Explained"→"Which One Is Right for You?" (−0.357pp).
- 🔴 **Swapping informational → geo-commercial** ("[X] in Bangalore") on a nationally/informationally-searched query mismatches intent and craters CTR — drug-deaddiction −0.402pp (worst), rtms-therapy −0.113pp.
- It is NOT about character length or emotional tone; it is number + specificity + intent-match.

**Rule:** When rewriting a meta title for CTR: (1) front-load the exact head keyword; (2) add a specific number iff the page is list/steps content; (3) add one credibility/curiosity token; (4) **never delete an existing number**; (5) **never convert an informational title to a geo-commercial "…in Bangalore" angle unless GSC confirms the query's own intent is local-commercial.** (6) A meta change cannot fix a snippet-starved top-3 page with ~0 CTR (dementia, pos 2.7) — that is an AI-Overview/featured-snippet problem (P2/P10), not a copy problem. (7) Read meta-only verdicts on **page-level CTR at flat impressions and stable position** — segregate pages whose impressions/rank moved materially.

**Ties to AP1:** Sprint C bulk-shipped 20 ranking pages with no staged 10% sample → 8 went RED. Sprint C v2 must ship a 2-page (10%) sample with a 7-day CTR read before the rest. Memo: `memory/patterns/sprint-c-meta-rewrite-result-2026-06-23.md`

