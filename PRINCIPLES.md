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
