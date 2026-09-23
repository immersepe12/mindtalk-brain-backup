# Proposal: task5 — query-level ownership gate (P12-E2) + tracking-db shape guard + queue/collection collision check
**Proposed:** 2026-09-14T23:30:00+05:30
**Source:** task20-auto-remediation-2026-09-14 (Verifier-audited: 17 APPROVE / 6 CORRECTION applied / 0 VETO)
**Apply on:** 2026-09-21T20:30:00+05:30 (auto-apply by Strategist if not vetoed; T13 sanity-check 2026-09-19)
**Status:** preview
**Companion:** `t5-doctors-listings-dead-route-20260913T2030.md` (apply 09-20) — this proposal does NOT repeat the route fix.

## Issue detected (ground truth, 2026-09-14)

T5's scheduled run (10:35 IST, cached-mode, `logs/new-content-2026-09-14.txt`) wrote **20 briefs and 19 of them were not shippable**
(`logs/t20-t5-brief-query-verify-2026-09-14.json` — GSC `dimensions=[page]` filtered by the brief's exact query, 28d + 90d; live curls no -L):

| Failure class | Count | Examples (owning live page → impr / clicks / pos, 90d) |
|---|---|---|
| Slug already LIVE (HTTP 200) | 1 | `dbt-therapy-near-me` → `/doctors/dbt-therapists` 200 |
| Duplicate of a brief already in `briefs/` | 2 | `child-psychologist-bangalore` = queued `NEW-child-psychologists-in-bangalore` (08-31); `online-psychologist-consultation` = queued `NEW-online-psychologist-india` |
| Synonym of a live national listing | 3 | `family-counselors` vs live `/doctors/family-therapists`; `emdr-therapists` vs `/doctors/emdr-specialists` (252/6/8.4); `biofeedback-therapists` vs `/doctors/biofeedback-specialists` (340/4/8.4) |
| Query already held on page 1 by a live URL (P12-E2) | 13 | `cptsd test` → `/assessments/itq` 2,067/52/9.3; `childhood trauma test` → `/assessments/childhood-trauma-test` (IDENTICAL slug) 863/21/9.5; `ocd test online` → `/assessments/ocd` 468/15/8.8; `social anxiety scale` → `/blogs/guide-to-liebowitz-social-anxiety-scale` 393/11/8.4; `couples therapy` → `/treatments/couples-therapy` 2,130/3/8.4; `deaddiction` → `/blogs/what-is-de-addiction` 365/4/7.4 + `/treatments/drug-deaddiction` 361/1/6.8; `psychiatrist online consultation free tamil` → `/doctors/tamil-speaking-doctors` 339/45/**1.7**; `erp therapy near me` → `/doctors/erp-therapists` 304/14/5.8; `tamil/telugu psychiatrist|psychologist near me` → `/doctors/{tamil,telugu}-speaking-doctors(-in-bangalore)` pos 2.1–8.4; `couple counselling online` → `/treatments/couples-therapy` 278/1/10.2 |

Only `adhd-specialist-near-me` (no national ADHD listing; property pos 18.5) and, on Verifier parity, `cbt-therapy-near-me` (no national CBT listing; 28d pos 11.5) survived.

Root causes in the spec, each verifiable:
1. **§2 "Redundancy / existing coverage" checks the `triggering_page` slug only** (INTENT/REDUNDANCY GATE, line ~159). It never asks GSC *which live URL already ranks for this exact query*. Four of the six Tier B picks were assessment queries the site already owns via `/assessments/*` — the same defect class as STUB-PILOT (07-09: "all 5 assessment picks redundant"). The 2026-09-12 T20/Verifier rule (P12-E2: site already page-1 at query level ⇒ VETO) exists only in T20's log, not in T5.
2. **No collision check against the other content collections or the existing brief queue.** `childhood-trauma-test` was proposed as `/blogs/childhood-trauma-test` while `src/content/assessments/childhood-trauma-test.mdx` is live; `child-psychologist-bangalore` duplicated a brief already queued for the same file.
3. **Step 6 shape violation (P1 — would have crashed tomorrow's Day-42 finals).** Step 6 specifies one top-level dict entry per brief (`"NEW-/blogs/[slug]": {...}`). The run instead wrote a single top-level key `new_content` whose value is a **list** of 20 dicts. `scripts/day42-evaluate-v2.py:40`, `day42-evaluate.py:34`, `day42-batch-gsc.py:84` iterate `for url, entry in db.items(): entry.get(...)` → `AttributeError: 'list' object has no attribute 'get'` (reproduced by T20 and independently by the Verifier). T20 converted the 20 items to spec-format entries and removed the key (backup `logs/tracking-db.json.backup-2026-09-14-2321-pre-t20`).
4. Also observed (no spec change proposed here, information for T13): the discovery cache carries `avg_position` as a per-page mean (rule g, 2026-09-12) — the log's "pos 7.5 … 11.8" for the four test queries were the *assessment pages'* positions, i.e. evidence of ownership, not of a gap.

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task5-new-content-discovery.md`
**Edit type:** insert (three hunks). No `scripts/*.py` change required — the gate is a GSC call the task already knows how to make (`scripts/gsc-pull.py` auth; sandbox env line `HOME=/tmp XDG_CACHE_HOME=/tmp TMPDIR=/tmp PYTHONPATH=.pip-packages`).

### Hunk 1 — after the INTENT/REDUNDANCY GATE bullet (Step 2, line ~159), insert:

```
- **QUERY-OWNERSHIP GATE (added 2026-09-21, from T20 2026-09-14 / P12-E2):** before briefing ANY candidate, query GSC with
  `dimensions=["page"]`, `dimensionFilterGroups=[{query equals <keyword>}]`, last 28d AND last 90d, `rowLimit ≥ 25` (rowLimit 6
  truncates 0-click queries — T20 lesson). If any live URL (excluding `?utm_` variants) holds ≥ 50 % of the query's impressions at
  position ≤ 12 in either window → the query is OWNED. Do NOT create a NEW brief; set the opportunity to `REDIRECT_TO_REFRESH`
  with `redirect_target = <owning URL>` and, if that URL's CTR < 1 % on ≥ 500 impressions, queue a refresh/CTR brief for it
  instead (Task 3 path). Log every OWNED rejection with the owning URL and numbers.
- **COLLECTION + QUEUE COLLISION CHECK (added 2026-09-21):** the proposed slug must not exist in ANY of
  `src/content/{blogs,assessments,treatments,illnesses,doctors-listings,worksheets,journeys,mindful-minutes}/` (GitHub tree at
  `main`, or the local checkout when it is current), must not return HTTP 200 at its live route (`/doctors/<slug>` for
  doctors-listings), and must not match the `Suggested File` of any brief already in `briefs/`. A collision = reject (log it), never
  a second brief.
```

### Hunk 2 — Step 6, immediately after the JSON example block, insert:

```
**Shape rule (added 2026-09-21):** `tracking-db.json` is a FLAT dict keyed by URL path (or `NEW-<path>`); every value is a dict.
Never add a list-valued or aggregate key (e.g. `new_content`). Before writing, assert
`all(isinstance(v, dict) for v in db.values())` — the Day-42 evaluators (`scripts/day42-evaluate*.py`) iterate `db.items()` and
crash on any other shape. On 2026-09-14 a list-valued key would have crashed the four Day-42 finals due 2026-09-15.
```

### Hunk 3 — §5.5 pre-check list, add one row:

```
- [PASS/FAIL] Query-ownership gate: no live URL holds the query on page 1 (owner + numbers logged)
- [PASS/FAIL] Collision check: slug absent from all content collections, live route 404, no queued brief for the same file
```

## Expected effect
- T5 stops spending its 20/week cap on pages the site already owns (19/20 today; 14/14 on 09-07 were dead-route duplicates).
- The refill that matters — Tier B decision-spoke blogs the site does NOT hold — becomes the only thing that reaches T9; the T9 Verifier's P12-E2 vetoes (3 of 7 on 09-12) move upstream to authoring time.
- tracking-db.json cannot be put into a shape that crashes T12's evaluators.

## Verification (T13, 2026-09-19)
1. Re-run `logs/t20-t5-brief-query-verify-2026-09-14.py` with `rowLimit` 25 on the 20 keywords — the 18 OWNED verdicts should reproduce; `cbt`/`adhd` should not be OWNED (no URL ≥ 50 % at ≤ 12 in 28d).
2. `python3 -c "import json;db=json.load(open('tracking-db.json'));assert all(isinstance(v,dict) for v in db.values())"` passes.
3. Next T5 run (2026-09-21): run log shows the two new gates with per-candidate OWNED/collision lines.

## Rollback
Remove the three hunks; nothing else depends on them. T20's data conversion is independent of this proposal (already applied, backed up).
