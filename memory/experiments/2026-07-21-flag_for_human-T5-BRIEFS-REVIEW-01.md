# flag_for_human on T5-BRIEFS-REVIEW-01 — 2026-07-21

## What we did

Fired flag_for_human for T5-BRIEFS-REVIEW-01 (T11 Executor, 4:30 PM IST run). Posted Slack to #seo-workflow-mindtalk (channel C0AUAPS4J83) documenting the T9 run status and remaining brief queue decision needed from Kushal.

## State at time of flag

**T9 already ran at ~4:20 PM today (before Executor's 4:30 PM window)** and shipped 5 blogs to LOCAL main (NOT pushed to origin):

| Blog | Reviewer | Status |
|------|----------|--------|
| common-relationship-issues | rangapriya-raghavan | ✅ SAFE — was T5-approved slug |
| how-to-choose-a-de-addiction-centre-in-india | shilpa-avarebeel | ✅ SAFE |
| what-is-act-therapy | tejal-jaiswal | 🔴 CONFLICT with CANNIBAL-BLOG-01 |
| what-is-biofeedback-therapy | vijayalaxmi-umate | 🔴 CONFLICT with CANNIBAL-BLOG-01 |
| what-is-rtms-treatment | dr-thejus-kumar | 🔴 CONFLICT with CANNIBAL-BLOG-01 |

**Original 5 T5 briefs from the BACKLOG flag:**
- common-relationship-issues → SHIPPED today ✅
- what-is-group-therapy → still in queue, NOT shipped
- what-is-couple-therapy → still in queue, NOT shipped
- what-is-meditation-therapy → still in queue, NOT shipped
- types-of-counselling → still in queue, NOT shipped

**T5 decision pending from Kushal:** For the remaining 4 briefs (group/couple/meditation therapy, types-of-counselling): (a) keep all 4, (b) keep only if no /treatments/ sibling, or (c) add AP9 canonical hints.

## Why flag_for_human (not auto-execute)

- 3 of the 5 T9 blogs conflict with CANNIBAL-BLOG-01 retirements on local main
- The conflict is compounded by missing redirects.mjs (see CANNIBAL-PUSH-01 experiment log)
- Remaining 4 brief decisions require AP9 cannibalization assessment against /treatments/* siblings
- AP3 Option B: what-is-group-therapy / what-is-couple-therapy / what-is-meditation-therapy are YMYL-adjacent (therapy modalities) — T9 must verify these do NOT replicate /treatments/* siblings before shipping

## Expected outcome

Kushal reviews T9's conflict state on Mac Mini, decides Option A/B for the 3 CANNIBAL slugs, and rules on the 4 remaining T5 briefs. Once resolved, Mac Mini pushes with clean state.

## Watch

None — status flag only, no content shipped.

## Notes

- Verifier pre-flight: APPROVE (trivial — flag_for_human has zero blast radius; no content changes, no push)
- Slack message link: https://cadabamsgroup.slack.com/archives/C0AUAPS4J83/p1784632535682619
- Production is SAFE: origin/main at 3a82ca1 (07-17); all conflicts are local-only
- /blogs/ cluster cap: was 6/6 as of 07-14; RESETS 07-21 (today)
