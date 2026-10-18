# Proposal: Elevate cost/pricing queries to P14 premium tier in Task 5 priority order
**Proposed:** 2026-10-11T20:30:00+05:30
**Source:** task13-meta-learner-2026-10-11
**Apply on:** 2026-10-18T20:00:00+05:30
**Status:** preview

## Issue detected

Category: **Missing signals / cross-task inconsistency (1c + 1a)**

T12 Learner established **Principle P14** today (2026-10-11): *"Cost/pricing queries are a premium T9 blog target class. Pattern: cost/pricing queries land top-5 within 42 days, 3–5× higher impressions than average T9 blog."*

Evidence (W43 Day-42 finals confirmed 2026-10-11):
- `therapy-cost-in-india` — pos 4.7, 3,245 impr 🟢 EXCEPTIONAL
- `couple-therapy-cost-in-bangalore` — pos 4.6, 483 impr 🟢 EXCEPTIONAL
- `rtms-treatment-cost-in-india` — pos 4.1, 780 impr 🟢 EXCEPTIONAL ("rtms therapy cost" pos 1.8 — #1 commercial result)

All 3 confirmed page-1 at Day-42, exceeding T9 average blog outcomes by 3–5× impressions.

**Task 5 gap:** `cowork-tasks/task5-new-content-discovery.md` Step 2 priority order currently lists "cost of…" only as a modifier example inside tier 2 (`TREATMENT_BLOG 150-300 vol AND commercial-modifier query`). Cost/pricing queries are treated the same as "…in India" or "…online" modifiers. P14 proves they deserve their own premium tier with a lowered volume floor (because the CTR-per-impression advantage compensates), surfacing above the standard ≥300 vol TREATMENT_BLOG tier.

## Proposed change
**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task5-new-content-discovery.md`
**Edit type:** sed-replace

### Before
```
1. **TREATMENT_BLOG** with search_volume_mo ≥ 300 → **highest priority** (commercial intent, converting cluster)
2. **TREATMENT_BLOG** with 150-300 vol AND commercial-modifier query (e.g., "…in India", "…online", "cost of…") → high-priority
```

### After
```
0. **COST/PRICING BLOG** — any `TREATMENT_BLOG` or `ILLNESS_BLOG` whose primary query contains "cost", "price", "pricing", "fees", "charges", "how much does", or follows the pattern `{treatment/condition} cost in {city/India}` → **P14 PREMIUM (front-load this run's cap)**. Volume floor: 100/mo (lower than standard because 3–5× impressions compensate). Evidence: W43 Day-42 finals (2026-10-11) — 3/3 cost queries hit page-1 within 42 days (therapy-cost-in-india pos 4.7, couple-therapy-cost pos 4.6, rtms-treatment-cost pos 4.1, all EXCEPTIONAL). See `brain/PRINCIPLES.md` P14.
1. **TREATMENT_BLOG** with search_volume_mo ≥ 300 → **highest priority** (commercial intent, converting cluster)
2. **TREATMENT_BLOG** with 150-300 vol AND commercial-modifier query (e.g., "…in India", "…online") → high-priority [note: "cost of…" promoted to tier 0 above per P14]
```

## Rationale
P14 is now established with 3 confirmed data points (the minimum threshold for a Principle). Cost/pricing queries consistently produce 3–5× impressions vs average T9 blog and reach page-1 within 42 days — outperforming even standard ≥300 vol TREATMENT_BLOGs which are currently the highest priority tier. By adding a dedicated tier 0 with a lower volume floor (100/mo), T5 will surface cost/pricing opportunities that today it de-prioritises or misses (because they often have 100–200 monthly searches, below the TREATMENT_BLOG 300 threshold). This directly translates to more high-return briefs entering the pipeline.

## Risk assessment
Low. Tier 0 is additive — all existing tiers (1–7) remain unchanged. The only risk is false-positives (topics that *contain* "cost" but are definition queries, e.g., "sunk cost meaning" — zero-click AP11 trap). Mitigated by the existing AP11 rejection filter: "BLOG_ARTICLE with pure informational intent AND zero historical booking-intent → do NOT brief." A "sunk cost meaning" page would fail the Intent Gate before reaching the brief stage. No anti-pattern violated.

## Rollback
Copy `brain/before-snapshots/task5-new-content-discovery.md-20261011T2030.bak` back to `cowork-tasks/task5-new-content-discovery.md`.

## Veto instructions
To veto: rename `t5-p14-cost-query-premium-20261011T2030.md` → `t5-p14-cost-query-premium-20261011T2030.vetoed.md` and add a `## Veto reason` section.
To approve early: rename → `t5-p14-cost-query-premium-20261011T2030.approved.md` — Strategist's next 8 PM run will apply it.
If neither, auto-applies on 2026-10-18.
