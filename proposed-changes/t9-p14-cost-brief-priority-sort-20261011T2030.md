# Proposal: Add P14 priority sort step to Task 9 — ship cost/pricing briefs first per run
**Proposed:** 2026-10-11T20:30:00+05:30
**Source:** task13-meta-learner-2026-10-11
**Apply on:** 2026-10-18T20:00:00+05:30
**Status:** preview

## Issue detected

Category: **Missing signals / wasted work (1c + 1b)**

T12 Learner established **Principle P14** today (2026-10-11): *"Cost/pricing queries are a premium T9 blog target class — land top-5 within 42 days, 3–5× higher impressions."* Evidence: W43 Day-42 finals — 3/3 cost queries confirmed EXCEPTIONAL (therapy-cost-in-india pos 4.7, couple-therapy-cost pos 4.6, rtms-treatment-cost pos 4.1).

**Task 9 gap:** T9 Step 1 collects brief candidates via `sorted(BRIEFS.glob('NEW-*-brief.md'))` — alphabetical sort by filename. With a 7-per-run cap, the 7 briefs that ship this run are determined by alphabetical slug order, not by impression-return potential. If 3 cost/pricing briefs and 10 standard briefs are in the queue this week, alphabetical sort might ship `analytics-for-mental-health.md` and `art-therapy-for-anxiety.md` first (A-sort), leaving `couples-therapy-cost-in-bangalore.md` for next week despite its P14 premium status.

**Cost:** Each deferred cost/pricing brief likely costs 3–5× the impressions of a standard blog that shipped in its place, per run. Over 4 weeks of cap misalignment, this compounds.

## Proposed change
**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task9-auto-ship-new-blogs.md`
**Edit type:** sed-replace

### Before
```
Regardless of whether candidates were found, run this secondary check:


### Step 2 — Apply safety filters to each candidate
```

### After
```
Regardless of whether candidates were found, run this secondary check:


### Step 1b — P14 priority sort (added 2026-10-11 — P14 alignment)
Before proceeding to safety filters, re-sort the candidates list to surface P14-premium briefs first:

**P14-premium detection:** A brief is P14-premium if its filename slug OR its `Primary Keyword:` frontmatter field (read the first 20 lines of each brief file) contains any of: `cost`, `price`, `pricing`, `fees`, `charges`, `how-much`, `how much`.

```python
# In-place sort: P14-premium candidates first, then alphabetical within each group
p14 = [c for c in candidates if any(kw in c[1] for kw in ['cost','price','pricing','fees','charges','how-much','how much'])]
standard = [c for c in candidates if c not in p14]
candidates = p14 + standard
```

Log the result:
```
P14 sort: {len(p14)} premium (cost/pricing) → front | {len(standard)} standard → follow
```

This ensures cost/pricing briefs consume their per-run slots before standard candidates when both types are queued, maximising impression yield per run. Per P14 (brain/PRINCIPLES.md): 3–5× impressions vs average T9 blog, confirmed 3/3 W43 Day-42.


### Step 2 — Apply safety filters to each candidate
```

## Rationale
P14 is now established with the minimum 3 confirmed data points. The economic case is clear: a cost/pricing blog delivers 3–5× the impressions of a comparable standard blog within the same 42-day window. Yet T9's alphabetical queue ordering is agnostic to this signal. The fix is a 4-line sort step — zero change to safety filters, zero change to MDX generation or shipping logic. It only changes which 7 of N candidates run this week. The sort is conservative: it promotes P14-premium candidates, not at the expense of safety filters (those still apply to every candidate). If a cost/pricing brief fails a safety filter, it's skipped like any other.

## Risk assessment
Low. The sort step is pure ordering — no candidates are added or removed. The only failure mode is a slug-detection false positive (e.g., a brief named `how-to-price-your-therapy-practice.md` is NOT a Mindtalk target-page and would be vetoed by the Tier A/B/C filter anyway). The sort is a pre-filter optimization, not a gate. Safety filters (Step 2) catch any misclassification downstream.

## Rollback
Copy `brain/before-snapshots/task9-auto-ship-new-blogs.md-20261011T2030.bak` back to `cowork-tasks/task9-auto-ship-new-blogs.md`.

## Veto instructions
To veto: rename `t9-p14-cost-brief-priority-sort-20261011T2030.md` → `t9-p14-cost-brief-priority-sort-20261011T2030.vetoed.md` and add a `## Veto reason` section.
To approve early: rename → `t9-p14-cost-brief-priority-sort-20261011T2030.approved.md` — Strategist's next 8 PM run will apply it.
If neither, auto-applies on 2026-10-18.
