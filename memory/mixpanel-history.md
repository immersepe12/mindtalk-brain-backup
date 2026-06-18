# Mixpanel History — Mindtalk website (project 4011856)

One line per Task 15 run. Most recent at bottom.

2026-06-15T16:20 IST | INAUGURAL | ACCESS BLOCKED | direct API: HTTP 402 plan-gated | MCP: per-project access not enabled (confirmed 2 projects) | events discovered: 0 | organic users: n/a | conversion events found: none (could not query)

2026-06-17T10:25 IST | MANUAL_RERUN (T15 silent-failed at 10:12) | mindtalk website 7d unique users + booking-intent events |
  - $mp_web_page_view: 3,805 unique
  - blog_viewed: 1,001 unique | doctor_profile_viewed: 489 unique | treatment_page_viewed: 192 unique | illness_page_viewed: 126 unique | riya_page_viewed: 5 ⚠ STILL invisible
  - book_appointment_clicked: 1,620 (last week 1,521, +6.5%)
  - form_submitted: 8 (last week 6, +33%)
  - lp_form_submitted: 130 (last week 124, +5%)
  - whatsapp_clicked: 80 | call_clicked: 57 | lead_create_failed: 75 (last week 77, -3%)
  - ⚠ Cadabams Consult project (3986277) NO LONGER VISIBLE in MCP today — cross-domain attribution layer broken. Was working 06-16. Either deleted/disabled/access-revoked. NEEDS INVESTIGATION.

2026-06-17T10:40 IST | FULL_T15_COMPLETION (access confirmed enabled — completes the 10:12 silent-fail + 10:25 volume-only rerun) | 7d window, unique users |
  - VOLUME (from 10:25 rerun, ~15min drift): page views 3,805 (funnel entry 3,818) | book_appointment_clicked 1,620 (+6.5% WoW) | form_submitted 8 (+33%) | lp_form_submitted 130 (+5%) | whatsapp 80 | call 57
  - FORM HEALTH: form_started 18 unique | form_error 3 | lead_create_failed 70 unique (≈34% of all lead attempts fail backend — persistent, was 75/77 prior weeks) ⚠
  - FUNNEL A (main booking, sequential 7d unique): page view 3,818 → book CTA 662 (17%) → form_submit 2 (~0%)
  - FUNNEL B (doctor-driven): doctor_profile_viewed 491 → book CTA 340 (69%) → form_submit 2 (1%)
  - FUNNEL C (where-to-start): viewed 3 → started 2 (67%) → completed 2 (100%) — page barely discovered (3 viewers/7d), same invisibility class as riya_page (5)
  - KEY: lp_form_submitted (130) vs form_submitted (8) = 16x ratio ⚠ (>5x flag). Real lead capture is the landing-page form, NOT the website booking form. Sequential form_submitted from page view is effectively 0 — the on-site multi-step booking funnel converts almost nobody; bookings happen via LP forms + doctor-profile CTA paths.
  - riya_page_viewed: 5 ⚠ STILL invisible (3rd week flagged)
  - Cadabams Consult (3986277) cross-domain: deferred to T19 (11:06 run) to confirm visibility.

| Week | Page views | book_click | form_submit | lp_form_submit | lead_fail | doctor→book % | Notes |
| 2026-06-17 (7d) | 3,805 | 1,620 | 8 | 130 | 70 | 69% | Full T15. lp:form=16x; on-site booking funnel ~0%; backend fail ~34%; riya+where-to-start invisible |

2026-06-17T11:00 IST | T19 SCHEDULED FIRE — attribution recheck | Cadabams consult (3986277) STILL not visible in Get-Projects. Searched accessible US projects for migrated consult booking events: 4026555 cadabams-org (none), 4015752 professionals (none), 4013942 cadabams hospitals (`book_appointment_clicked` only — hospital funnel, not consult), 3984638 cadabams group (EU-locked). Conclusion: consult revenue-validation funnel not reachable from US MCP. Cross-domain attribution remains blocked. No website re-pull (inaugural classification already current for this week).

