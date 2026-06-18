# Mixpanel access — partial resolution, 2026-06-16

## Resolved sources (autonomous loop has access)

| Project | Region | Method | Status |
|---|---|---|---|
| 4011856 Mindtalk website | US | MCP (mcp.mixpanel.com) | ✅ Working |
| 3986277 Cadabams consult | US | MCP (mcp.mixpanel.com) | ✅ Working |

## Blocked source (intentionally unaddressed)

| Project | Region | Wall | Decision |
|---|---|---|---|
| 3984638 cadabams group (Mindtalk app) | EU | Two stacked blockers: (a) no Mixpanel EU MCP connector in Cowork registry, (b) project plan tier blocks Data Export API (HTTP 402 on all /api/2.0/ endpoints) | **Kushal decided NOT to upgrade Mixpanel plan.** Wait for Anthropic to add EU MCP connector. No timeline. App engagement signals (assessments, journeys, Riya, audio) stay out of autonomous loop for now. |

## What this means for the loop

The autonomous loop's primary job is SEO + conversion. The two working sources cover:
- Marketing-site traffic, content engagement, top-of-funnel behaviour (4011856)
- Booking funnel, payment flow, doctor selection UX (3986277)

App engagement signals are product/UX inputs more than SEO inputs. Strategist + Learner have enough data to do their job; Meta-Learner can flag if they ever NEED the missing data to make a specific decision, at which point we revisit the cost/wait tradeoff.

## Service account rotation pending

EU service account (`mp-autonomous-seo-loop.d7e328.mp-service-account`) was created and secret was exposed in chat. Since the loop can't use it anyway, Kushal should delete it from eu.mixpanel.com → Settings → Service Accounts when convenient. No urgency — secret is useless without API access.
