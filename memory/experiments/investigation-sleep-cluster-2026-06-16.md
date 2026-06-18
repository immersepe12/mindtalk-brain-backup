# investigate_regression — Sleep cluster "drop to position 100" — 2026-06-16

**Run:** Executor (T11) 16:35 IST · **Verifier verdict:** APPROVE (read-only diagnostic; non-YMYL blog pages; IS the AP5-mandated verification)
**BACKLOG row:** #1 · **Status:** RESOLVED — deindex/technical hypothesis **REFUTED**. No content action.

---

## What we investigated

BRAIN + BACKLOG #1 flagged a suspected **technical deindex**: two page-1 siblings —
`/blogs/how-anxiety-affects-sleep` (5→100) and `/blogs/cognitive-behavioral-therapy-for-insomnia` (11→100) —
allegedly dropped to **exactly position 100 on 2026-06-12**, with a third sibling
`/blogs/sleep-disorder-tests-from-insomnia-to-hypersomnia` GSC-confirmed −49.8% impr. The "exactly 100, simultaneous"
signature was hypothesised to be technical (deindex / canonical / sitemap), not gradual algo. BRAIN marked it UNVERIFIED
(never re-pulled since the 06-12 weekend gap). AP5 requires verify-before-act.

## What the data actually shows

### 1. GSC re-pull (authoritative — Google's own index/serving state), `pulled_at: 2026-06-16`

| Page | Impr (cur vs prev) | Avg position (cur vs prev) | Δpos | Signal |
|---|---|---|---|---|
| how-anxiety-affects-sleep | 32 vs 65 (−50.8%) | **32.8** vs 33.4 | −0.6 (improved) | **NOISE** |
| cognitive-behavioral-therapy-for-insomnia | 97 vs 130 (−25.4%) | **10.1** vs 12.6 | −2.5 (improved) | **NOISE** |
| sleep-disorder-tests-from-insomnia-to-hypersomnia | 230 vs 414 (−44.4%) | **41.5** vs 44.8 | −3.3 (improved) | **NOISE** |

A deindexed page returns **zero** GSC impressions. All three reported impressions across **31 / 50 / 50 keywords**
respectively in the 06-06→06-13 window, at average positions of **33 / 10 / 42** — nowhere near 100 — and every page's
average position **improved** week-over-week. The diagnostic classifier labelled all three `NOISE` (small absolute
volumes, positions holding/improving, zero click delta).

### 2. cluster-history.json (GSC weekly rollup) — the alleged-drop window was their *best*

- **cognitive-behavioral-therapy-for-insomnia**, week_start 2026-06-06: **348 impr, avg_position 15.0, 6 clicks, CTR 1.8%, 101 queries** — the strongest week in the entire series (most clicks, highest CTR, most queries). Position improved from 20.8 (05-31) → 15.0.
- **sleep-disorder-tests-from-insomnia-to-hypersomnia**, week_start 2026-06-06: **57 impr, avg_position 6.9, 1 click, CTR 1.3%** — its **best average position on record** (prior range 11–30).
- **how-anxiety-affects-sleep**: sparse in cluster-history (1 impr on its tracked head query at pos 2–3); the 7-day GSC window above (32 impr / pos 32.8 across 31 keywords) is the fuller view and is healthy.

The pages were thriving in the exact window DataForSEO claimed they fell to 100.

### 3. Git history — no event to cause a technical drop

All three MDX files' most recent commit is **2026-05-25** (`feat(seo): add named clinical reviewer` batches `2703a7a` / `9c564c4` / `9574ebf`). Nothing — no deploy, migration, canonical edit, or sitemap change — touched these files anywhere near 06-12.

### 4. Frontmatter — clean

All three: `reviewer: sucheta-saha` present, published (`publishedAt` set), and **no `noindex` / `robots` / `canonical` override**. No accidental de-indexing directive.

### 5. Live HTTP/canonical fetch — NOT performed this run

`web_fetch` was blocked by the sandbox provenance restriction (URLs not previously in context), and policy forbids curl/wget/python fetching. Not a gap: GSC index-coverage (impressions across dozens of keywords) is a **stronger** signal of indexation than a server-side HTTP 200, because it reflects Google's actual index, not just origin availability. Recommend a one-line live confirmation on the authenticated Mac Mini if desired (HTTP 200 + self-canonical), but it is not required to close this.

## Root cause

The "position 100 on 06-12" reading is a **DataForSEO single-keyword rank-tracker artifact**. "100" is the tracker's
sentinel for "the tracked keyword was not found in the top 100 on this specific pull" — which happens with SERP
volatility, weekend pulls, personalization/location drift, or head terms the page never strongly held. It is **not** a
statement about whether Google indexes the URL. GSC (index coverage + impressions + positions) and cluster-history both
contradict the tracker; the URL-level reality is healthy and improving.

This is a textbook **P5** (cluster/alert false-positive from small samples) + **AP5** (verify spike-vs-baseline before
acting) case — with a sharper, newly-observed wrinkle worth codifying (see below).

## Recommended action (replaces BACKLOG #1)

**NO content action. Close.** Do not refresh, restructure, escalate, or open a recovery watch on these three pages —
they are healthy page-1/page-2 performers and perturbing them would only muddy attribution (anti-goal: "refreshing
recently-touched / healthy pages"). The verify-before-act loop did its job: it prevented a wasteful, risk-bearing edit
to two healthy pages.

Follow-ups (for the owning roles, NOT executed here):
1. **Learner (T12):** consider promoting the candidate pattern below to PRINCIPLES.md / ANTI-PATTERNS.md.
2. **Strategist (T10):** the existing `sleep-disorder-tests` brief's SHIP-NOW E-E-A-T housekeeping (leading/trailing
   spaces in metaTitle `" 7 Diagnostic Tests for Sleep Disorders | Mindtalk "`, broken-H2, reviewer byline/JSON-LD)
   remains valid but is **separate** from this refuted regression and stays under the existing algo_watch hold (~06-23).
   Not a deindex remediation.
3. Optional informational: confirm the *tracker itself* recovered off "100" on the next scheduled DataForSEO rank run
   (cheap, not required — GSC already settles the question).

## Candidate pattern (for Learner to ratify — 3+ evidence rule)

> **DataForSEO rank-tracker "position 100" ≠ deindex.** A tracked keyword reading exactly 100 (or "simultaneous
> siblings at 100") is a sentinel for "not in top 100 on this pull," not a Google index-state signal. Before treating a
> "drop to 100" as technical (deindex/canonical/sitemap), cross-check (a) GSC index coverage / impressions, (b)
> cluster-history weekly trend, and (c) git log for an actual deploy/content event in the window. If GSC shows
> impressions and positions are holding/improving, classify as tracker NOISE and take no action. Evidence #1: sleep
> cluster 2026-06-16 (this investigation).

## Expected outcome

No ranking change (intentional — no action taken). The win is **avoided harm**: two healthy page-1/2 pages were not
needlessly edited, and a false "technical deindex" alarm was retired with authoritative GSC evidence.

## Watch

No recovery watch opened. WATCH.md "Sleep cluster" pending-observation row closed: **confirmed DataForSEO noise**
(per its own pre-stated rule: "if recovered → confirmed DataForSEO noise, close").

## Notes

- PII check (VERIFIER §10): this file and the Slack summary contain only aggregated keyword/impression/position metrics
  and URLs — no emails, phone numbers, or user-ids.
- Blast radius: 0 pages modified. Read-only diagnostic.
