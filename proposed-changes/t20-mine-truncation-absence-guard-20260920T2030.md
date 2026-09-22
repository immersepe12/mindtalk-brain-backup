# Proposal: T20 brief-refill must validate "no holder" via per-query GSC pull, not bulk mine absence
**Proposed:** 2026-09-20T20:30:00+05:30
**Source:** task13-meta-learner-2026-09-20
**Apply on:** 2026-09-27T20:00:00+05:30
**Status:** preview

## Issue detected

T20's brief-starvation auto-fix runs a 100k-row `query×page` bulk GSC mine and concludes "no holder" for queries that don't appear in the mine. T20 09-19 proved this is wrong:

> "99 'zero-organic-impression' converting terms — apparent blind spots. They are not blind spots. Per-query filtered GSC pulls (the only honest test) show the site does appear, mostly on page 1: `marriage counselor near me` pos 1 (173 impr) · `in person therapy bangalore` pos 1 (147) · `marriage counseling near me` pos 2 (165) · `offline therapist near me` pos 6 (33) · `psychological assessment` pos 6.3 (122). Root cause: a 100,000-row `query×page` pull is TRUNCATED — absence from it is not evidence of absence."

The 09-19 T20 explicitly filed: "MINE-TRUNCATION-ABSENCE-01: any 'no holder' claim must be proven by a per-query filtered pull, never by absence from a bulk mine." Without this guard in the task spec, future T20 refill runs will produce briefs for queries where Mindtalk already ranks #1 — wasting brief slots and potentially cannibalizing existing pages.

**Recurring risk:** T20 caught this on 09-19 before writing any briefs — but only because it happened to run the per-query validation for another reason. Future runs with tighter time windows may not.

## Proposed change
**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task20-auto-remediation.md`
**Edit type:** append

Append the following block immediately after the Brief starvation auto-fix row in the REMEDIATION REGISTRY (after the line ending "Refill to ≥12 shippable."):

### Before
```
| **Brief starvation** (`/blogs/` queue < 6 shippable) | Run `scripts/new-content-discovery.py --all` (PYTHONPATH=.pip-packages). Then run `scripts/google-ads-search-terms.py` for paid-conversion terms. Generate blog briefs from the top opportunities that pass the Intent Gate (INTENT-PRIORITY.md §2), Tier A/B only, each with `intent_tier`, `faqs:`, ≥3 internal links, a `reviewer`. Refill to ≥12 shippable. |
```

### After
```
| **Brief starvation** (`/blogs/` queue < 6 shippable) | Run `scripts/new-content-discovery.py --all` (PYTHONPATH=.pip-packages). Then run `scripts/google-ads-search-terms.py` for paid-conversion terms. Generate blog briefs from the top opportunities that pass the Intent Gate (INTENT-PRIORITY.md §2), Tier A/B only, each with `intent_tier`, `faqs:`, ≥3 internal links, a `reviewer`. Refill to ≥12 shippable. **⚠ MINE-TRUNCATION-ABSENCE-01 (filed 2026-09-19):** Before writing any brief for a query the bulk mine shows as "no holder", validate with a per-query GSC filtered pull (`dimensions=[query]`, `rowLimit 25`, the target query as filter). If the per-query pull returns a Mindtalk URL at position ≤ 10, the query already has a holder — reclassify as `REDIRECT_TO_REFRESH`, do NOT create a new brief. Absence from a 100k-row `query×page` bulk mine is NOT evidence of absence from rankings (mine is truncated; confirmed 5 queries at pos 1 that did not appear in the bulk pull, 2026-09-19). Skip the per-query check only when the query has paid conversions AND confirmed 0 impressions via a direct filtered pull already run this session. |
```

## Rationale

The bulk mine truncates at 100k rows and will miss queries where the site ranks page 1, especially long-tail and geo variants. Creating briefs for these would waste a brief slot and risk cannibalizing an existing ranking page. The per-query validation is cheap (one GSC API call per candidate) and prevents the class of error identified 09-19. T5's discovery script has a similar Step 3a intent check; T20's refill step had no equivalent gate.

## Risk assessment

Medium. The per-query GSC call adds latency to the refill step — roughly 1-2 seconds per candidate. If T20 evaluates 50+ candidates in a session, total overhead is ~1-2 minutes. The 180-second bash cap may be reached on very large candidate lists; if so, T20 should process candidates in batches of 20 and log partial progress. The alternative risk (briefs for pos-1 queries) is higher-impact and harder to detect after the fact.

## Rollback

Copy `brain/before-snapshots/task20-auto-remediation-mine-truncation-20260920T2030.bak` back to `cowork-tasks/task20-auto-remediation.md`. This restores the pre-guard behaviour; T20 will need to validate "no holder" claims manually as it did on 09-19.

## Veto instructions
To veto: rename to `t20-mine-truncation-absence-guard-20260920T2030.vetoed.md` and add a `## Veto reason` section.
To approve early: rename to `t20-mine-truncation-absence-guard-20260920T2030.approved.md`.
