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

## ⚠ NEW BLOCK — 2026-07-22 (T15 Wed run)

| Project | Error | Date | Previously |
|---|---|---|---|
| 4011856 Mindtalk website | `"Your account is blocked because payment is required. Please contact support via https://mixpanel.com/get-support"` | 2026-07-22 | ✅ Working — last successful T15 run was 2026-07-08 |

This is a **new error class**: the 2026-06-15 block was "per-project access not enabled" and was resolved by enabling project-level access. The 2026-07-22 block is a billing/payment block on the Mixpanel account — likely the MCP service account's subscription lapsed or the Mixpanel plan expired.

**Kushal action required:** Log into Mixpanel → check account billing status → resolve payment issue → confirm MCP access restored.

**Impact:** T15 has no Mixpanel data for W30 (2026-07-22 run). No conversion KPIs updated in TRAJECTORY.md this week.

---

## Service account rotation pending

EU service account (`mp-autonomous-seo-loop.d7e328.mp-service-account`) was created and secret was exposed in chat. Since the loop can't use it anyway, Kushal should delete it from eu.mixpanel.com → Settings → Service Accounts when convenient. No urgency — secret is useless without API access.
