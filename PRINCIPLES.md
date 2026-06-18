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

