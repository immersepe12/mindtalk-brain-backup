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
| 2026-06-24 (7d) | 5,941 | 745 | 6 | 136 | 79 | 69% | Page views +56%✅; book_click -54%⚠⚠ (intent dilution — new traffic is SEO/blog, not commercial); LP form +5% (absolute leads stable); backend fail ~36% (stable); where-to-start +367%✅ (3→14); riya 10 (doubled, still tiny) |

2026-06-17T11:00 IST | T19 SCHEDULED FIRE — attribution recheck | Cadabams consult (3986277) STILL not visible in Get-Projects. Searched accessible US projects for migrated consult booking events: 4026555 cadabams-org (none), 4015752 professionals (none), 4013942 cadabams hospitals (`book_appointment_clicked` only — hospital funnel, not consult), 3984638 cadabams group (EU-locked). Conclusion: consult revenue-validation funnel not reachable from US MCP. Cross-domain attribution remains blocked. No website re-pull (inaugural classification already current for this week).

2026-06-25T10:00 IST | T15 SCHEDULED — weekly conversion monitor | 7d unique users |
  VOLUME:
  - $mp_web_page_view: 5,941 (+56% WoW ✅ traffic surge)
  - blog_viewed: 1,077 | doctor_profile_viewed: 522 | treatment_page_viewed: 228 | illness_page_viewed: 144 | riya_page_viewed: 10 (doubled from 5, still tiny ⚠)
  - where_to_start_page_viewed: 14 (+367% WoW ✅; was 3 — internal linking working)
  - book_appointment_clicked: 745 (-54% WoW ⚠⚠ CRITICAL — page views surged +56% but book clicks halved; intent dilution from SEO/blog traffic)
  - form_submitted: 6 (-25%) | lp_form_submitted: 136 (+5% ✅ absolute leads stable)
  - form_started: 12 (-33%) | form_error: 2 | lead_create_failed: 79 (+13%)
  - whatsapp_clicked: 90 (+13%) | call_clicked: 39 (-32% ⚠) | cta_clicked: 130 (first recorded)
  FUNNELS:
  - A (main): page view 5,941 → book CTA 744 (13%, was 17%) → form_submit 2 (<0.1%)
  - B (doctor-driven): doctor_profile 522 → book CTA 359 (69%, STABLE ✅) → form_submit 2 (0.6%)
  - C (where-to-start): viewed 14 → started 6 (43%) → completed 6 (100%)
  KEY METRICS:
  - lp:form ratio = 22.7x (up from 16x ⚠ — LP form still the real lead channel)
  - Backend fail rate: 79/(136+6+79) = 35.7% (was ~34%; STABLE, persistent engineering issue ⚠)
  - Doctor→book CTA: 69% (no change, strongest intent path ✅)
  WoW FLAGS (>20%):
  ⚠⚠ book_appointment_clicked -54% (intent dilution — new traffic is low-commercial-intent SEO content)
  ✅ Page views +56% (SEO traffic growing strongly)
  ⚠ form_submitted rate from page views: 0.10% vs 0.21% (-52%) — denominator effect; absolute leads stable
  ⚠ lp_form_submitted rate: 2.29% vs 3.42% (-33%) — same denominator effect
  ⚠ call_clicked -32% (57→39)
  ✅ where_to_start_page_viewed +367% (3→14)
  ✅ riya_page_viewed +100% (5→10, still tiny)


2026-07-01T10:00 IST | T15 SCHEDULED — weekly conversion monitor | 7d unique users |
  VOLUME:
  - $mp_web_page_view: 6,397 (+7.7% WoW)
  - blog_viewed: 1,275 | doctor_profile_viewed: 558 | treatment_page_viewed: 247 | illness_page_viewed: 161 | riya_page_viewed: 6 (down from 10 ⚠) | where_to_start_page_viewed: 17 (+21% ✅)
  - book_appointment_clicked: 764 (+2.6% — stable ✅)
  - form_submitted: 4 (-33%) | lp_form_submitted: 151 (+11% ✅)
  - form_started: 15 | form_error: 2 | lead_create_failed: 17 (-78%!! WAS 79 ✅✅✅)
  - whatsapp_clicked: 92 (+2%) | call_clicked: 54 (+38% ✅) | cta_clicked: 126 (-3%, stable)
  FUNNELS:
  - A (main): page view 6,397 → book CTA 758 (11.8%, was 13%) → form_submit 2 (~0%)
  - B (doctor-driven): doctor_profile 558 → book CTA 369 (66%, was 69%) → form_submit 2 (0.5%)
  - C (where-to-start): viewed 17 → started 11 (65%) → completed 11 (100% of started; 65% overall)
  KEY METRICS:
  - lp:form ratio = 37.75x (151/4) — up from 22.7x. LP form is the ONLY real lead channel ⚠
  - Backend fail rate: 17/(151+4+17)=9.9% — DOWN from 35.7% ✅✅✅ MAJOR IMPROVEMENT
  - Doctor→book CTA: 66% (was 69%, -4.3%, still stable)
  - Riya discovery rate: 0.094% (was 0.168%, -44%; tiny absolute, inconclusive)
  WoW FLAGS (>20%):
  ✅✅✅ lead_create_failed -78% (79→17) — backend fail rate 35.7%→9.9%; may indicate engineering fix deployed
  ✅ lp_form_submitted +11% (136→151)
  ✅ call_clicked +38% (39→54) — recovery after -32% last week
  ✅ where_to_start +21% (14→17)
  ⚠ form_submitted -33% (6→4) — tiny sample, noise likely
  ⚠ riya_page_viewed -40% (10→6) — tiny absolute, inconclusive (more blog traffic diluting discovery)
  ⚠ lp:form ratio 22.7x→37.75x — on-site booking form increasingly irrelevant

| 2026-07-01 (7d) | 6,397 | 764 | 4 | 151 | 17 | 66% | PAGE VIEWS +8%✅; BACKEND FAIL -78%✅✅✅ (35.7%→9.9% — possible engineering fix); LP form +11%✅; call_clicked +38%✅; book CTA stable; lp:form=38x⚠; riya still invisible |
| 2026-07-08 (7d) | 6,342 | 784 | 5 | 129 | 2 | 73% | Page views stable (-1%); BACKEND FAIL -88%✅✅✅ (9.9%→1.5% — recovery continues, now effectively negligible); riya +133%✅✅ (6→14, first real break from invisibility); illness -27%⚠ (161→118); lp_form -15% (151→129, watch); doctor→book CTA +10.6% new high (73%); lp:form=25.8x |
| 2026-07-22 (7d) | MCP_BLOCKED | — | — | — | — | — | ⛔ MCP_BLOCKED: Mixpanel returned "account blocked — payment required". Billing issue on Mixpanel account. No data this week. See mixpanel-access-blocked.md. |
| 2026-07-29 (7d) | 8,167 | 743 | 97 | 55 | 11 | 31% | Page views +28.8%✅ (vs 07-08, 3-wk gap); 🚨 form_submitted 5→97 (INVERTED lp:form — on-site form now primary; ads paused explains LP drop); lp_form -57%⚠ (129→55, ads pause); doctor→book CTA -57%⚠⚠ (73%→31%, absolute clicks stable 431→406 — new doctor traffic is low-intent SEO visitors); backend fail crept up 1.5%→6.7%⚠ (still ok; was 35.7% peak); riya -29%⚠ (14→10); doctor views +118%✅✅ (592→1,293 — T9 content driving discovery); where-to-start +31%✅ (16→21) |
| 2026-08-05 (7d) | 9,884 | 780 | 115 | 55 | 14 | 29% | Page views +21%✅ (8,167→9,884); doctor views +26.5%✅ (1,293→1,636 — T9 content compounding); form_submitted +18.6% (97→115); net leads 170 (115+55 = best week if Freshsales confirmed ✅); lp_form stable (55, 0%); doctor→book CTA -7.6% (31%→29%, stable); CTA→form 5%→8.75%✅ (on-site booking form conversion continuing to improve); lp:form=0.48:1 (on-site form dominant, ads still paused); backend fail crept 6.7%→7.5%⚠ (14 failures, watch trend — was 35.7% peak); riya -30%⚠ (10→7, still invisible); where-to-start 21→19 (-9.5%, stable) |
| 2026-08-26 (7d) | 10,344 | 740 | 55 | 58 | 18 | 33% | 🚨 form_submitted -52%⚠⚠ CRITICAL (115→55 — largest drop since structural shift began; August Core Update proximity?); net leads 113 (-33.5%⚠⚠ vs 170); backend fail 7.5%→13.7%⚠⚠ (4th consecutive rise; 18 failures; was 35.7% peak); doctor→book CTA 29%→33%✅; CTA→form crashed 8.75%→7.4%⚠; riya +86%✅ (7→13 — small base but real jump); lp_form +5.5%✅ (55→58, stable/slight improvement); doctor profile −8.7% (1,636→1,494); where-to-start 53% overall ✅ (17 viewed, 9 completed) |


2026-08-26T10:00 IST | T15 SCHEDULED — weekly conversion monitor | 7d unique users (vs 2026-08-05 baseline) |
  VOLUME (unique users — page views + funnel entries; total events in parentheses where different):
  - $mp_web_page_view: 10,344 unique funnel entry (44,698 total events; +4.7% unique WoW)
  - blog_viewed: 1,477 | doctor_profile_viewed: 1,494 unique funnel (-8.7% vs 1,636) | treatment_page_viewed: 403 | illness_page_viewed: 194 | riya_page_viewed: 13 (+85.7%✅ vs 7) | where_to_start_page_viewed: 17
  - book_appointment_clicked: 740 unique funnel (-5.1% vs 780) | 2,051 total events | whatsapp_clicked: 90 | call_clicked: 56 | cta_clicked: 220
  - form_submitted: 55 unique (-52.2%⚠⚠ vs 115) | 112 total events
  - lp_form_submitted: 58 (+5.5%✅ vs 55) | form_started: 20 | form_error: 4 | lead_create_failed: 18 (+28.6%⚠ vs 14)
  FUNNELS:
  - A (main): page view 10,344 → book CTA 740 (7.2%, was 7.86%) → form_submit 55 (7.4% of CTA; 0.53% of PVs, was 0.69%)
    CTA→form: 8.75%→7.4% (-15%, deteriorating ⚠)
  - B (doctor-driven): doctor_profile 1,494 → book CTA 491 (32.9%, was 29.0%✅) → form_submit 4 (0.8% of CTA, was 2.1%⚠⚠)
    Absolute form submissions from doctor path: 10→4 (-60%⚠⚠)
  - C (where-to-start): viewed 17 → started 10 (59%, was 31.6%✅✅) → completed 9 (90% of started; 53% overall, was 31.6%✅✅)
  KEY METRICS:
  - Net total leads: 55+58 = 113 unique submitters (vs 170 last week = -33.5%⚠⚠)
  - Backend fail rate: 18/(55+58+18) = 13.7% (was 7.5% — 4th consecutive weekly rise; was 35.7% at peak ⚠⚠ WATCH)
  - Doctor→book CTA: 32.9% (was 29.0%, +13.4%✅ — rate improving even as absolute doctor viewers declined)
  - Riya discovery rate: 13/10,344 = 0.126% (was 7/9,884 = 0.071%, +77%✅ — best reading in 6 weeks)
  WoW FLAGS (>20% vs 2026-08-05):
  🚨 form_submitted -52.2% (115→55) — CRITICAL; on-site booking form crash; largest single-week drop since structural shift; August Core Update today (08-26) may be the catalyst (pre-update SERP volatility visible Aug 10-16) — check next week to confirm
  ⚠⚠ backend fail rate +82.7% (7.5%→13.7%) — 4th consecutive rise; 18 raw failures; trend now significant; was 35.7% peak
  ⚠⚠ net leads -33.5% (170→113) — driven entirely by form_submitted crash; lp_form stable
  ⚠⚠ overall conversion rate -23.2% (0.69%→0.53% of page views)
  ✅ riya_page_viewed +85.7% (7→13) — best reading in 6 weeks; 08-18 T9 overthinking/situationship batch driving discovery?
  ✅ doctor→book CTA +13.4% (29%→33%) — structural improvement in commercial intent on doctor pages
  ✅ where-to-start completion rate +67% (31.6%→53% overall) — feature is now more sticky when found
  ⚠ lead_create_failed +28.6% (14→18) — consistent with fail rate rise
  NOT FLAGGED: page views +4.7% (10,344 vs 9,884); doctor views -8.7% (1,494 vs 1,636); lp_form +5.5% (58 vs 55)
  IMPLICATIONS:
  - The form_submitted crash is the #1 signal. August Core Update launched 08-26 — check next T15 run (09-03) to determine if this is SERP-traffic-quality decline or product regression.
  - Backend fail rate hitting 13.7% needs engineering attention — if ads restart, this will amplify.
  - LP form (58) stable = ads still paused and LP organic traffic holding. When ads restart, LP form should surge.
  - Riya page views reaching 13 — the 08-18 batch of high-volume blogs (overthinking, situationship) may be routing users toward Riya. Worth monitoring.

2026-08-05T10:00 IST | T15 SCHEDULED — weekly conversion monitor | 7d unique users (vs 2026-07-29 baseline) |
  VOLUME (unique users):
  - $mp_web_page_view: 9,884 (+21.0% WoW ✅)
  - blog_viewed: 1,327 | doctor_profile_viewed: 1,636 (+26.5%✅) | treatment_page_viewed: 355 | illness_page_viewed: 188 | riya_page_viewed: 7 (-30%⚠) | where_to_start_page_viewed: 19 (-9.5%, stable)
  - book_appointment_clicked: 780 (+5.0%) | whatsapp_clicked: 115 (+6.5%) | call_clicked: 54 (+3.8%) | cta_clicked: 170 (-19.8%, borderline)
  - form_submitted: 115 unique (+18.6%) | lp_form_submitted: 55 unique (0%, stable)
  - form_started: 26 | form_error: 3 (+200% vs 1, tiny absolute) | lead_create_failed: 14 (+27.3%⚠)
  FUNNELS:
  - A (main): page view 9,884 → book CTA 777 (7.86%, was 9.0%) → form_submit 68 (8.75% of CTA, 0.69% of PVs)
    CTA→form conversion: 5%→8.75% +75%✅✅ (on-site booking form continuing to improve)
  - B (doctor-driven): doctor_profile 1,636 → book CTA 475 (29.0%, was 31.4%) → form_submit 10 (2.1% of CTA, 0.61% of PVs)
  - C (where-to-start): viewed 19 → started 6 (31.6%, was 38.1%) → completed 6 (100% of started)
  KEY METRICS:
  - Net total leads: 115+55 = 170 unique submitters (vs 152 last week = +11.8% ✅ — verify Freshsales)
  - lp:form ratio: 55/115 = 0.48:1 (on-site form dominant; ads still paused; LP form flat)
  - Backend fail rate: 14/(115+55+14) = 7.5% (was 6.7% — second consecutive week creeping up ⚠)
  - Doctor→book CTA: 29.0% (was 31.4%, -7.6% — within normal range, stable)
  - Riya discovery rate: 7/9,884 = 0.071% (was 0.12%, -40% — consistently invisible)
  WoW FLAGS (>20% vs 2026-07-29):
  ✅ page_views +21.0% (8,167→9,884) — organic traffic compounding
  ✅ doctor_profile_viewed +26.5% (1,293→1,636) — T9 content driving sustained doctor discovery
  ⚠ lead_create_failed +27.3% (11→14) — backend fail rate 6.7%→7.5%; 3rd consecutive increase; was 35.7% at peak; still far below but trend is wrong direction
  ⚠ riya_page_viewed -30% (10→7) — persistent invisibility (5 consecutive weeks <15 views)
  ⚠ form_error +200% (1→3) — tiny absolute (3 users), not actionable yet but watch
  NOT FLAGGED: form_submitted +18.6% (just under), CTA→form +75%✅ (highly positive structural shift)

2026-07-29T10:00 IST | T15 SCHEDULED — weekly conversion monitor | 7d unique users (vs 2026-07-08 baseline — 07-22 was MCP_BLOCKED) |
  VOLUME (unique users):
  - $mp_web_page_view: 8,167 (+28.8% vs 07-08; 3-week gap so ~+9.6%/wk avg)
  - blog_viewed: 1,425 (total events) | doctor_profile_viewed: 1,293 unique (+118.4%✅✅) | treatment_page_viewed: 541 total | illness_page_viewed: 197 total (+67% vs 118, recovery) | riya_page_viewed: 10 unique (-28.6%⚠ vs 14) | where_to_start_page_viewed: 21 unique (+31.3%✅)
  - book_appointment_clicked: 743 unique (-5.2%, stable) | whatsapp_clicked: 108 (+3.8%) | call_clicked: 52 (-1.9%, stable) | cta_clicked: 212 total
  - form_submitted: 97 unique (+1,840%!! vs 5) | lp_form_submitted: 55 unique (-57.4%!! vs 129)
  - form_started: 28 total | form_error: 1 | lead_create_failed: 11 unique (+450% vs 2)
  STRUCTURAL SHIFT: lp:form ratio INVERTED. Was 25.8x (LP dominates). Now 0.57x (on-site form (97) > LP form (55)).
  EXPLANATION: Ads are paused → LP gets no paid traffic → lp_form_submitted crashes. Organic traffic up 29% → users find site naturally → hit on-site form. Net total submitters: ~152 unique (97+55) vs 134 (5+129) = +13% — total lead volume may actually be GROWING.
  ⚠ Verify with Freshsales: are ~97 on-site form submitters arriving as leads? If yes, this is the best lead week recorded.
  FUNNELS:
  - A (main): page view 8,167 → book CTA 735 (9.0%, was 12.3%) → form_submit 37 (5.0% of book CTA, 0.45% overall; was 0.51%→0.06%)
    Note: book CTA→form conversion EXPLODED 0.5%→5.0% — structural change in form placement or flow
  - B (doctor-driven): doctor_profile 1,293 → book CTA 406 (31.4%, was 73%⚠⚠) → form_submit 6 (1.5% of CTA, 0.5% overall)
    Note: absolute book clicks from doctor path stable (406 vs 431) — new doctor visitors are low-intent SEO; the 73%→31% rate drop is denominator explosion, not fewer commercial-intent visitors converting
  - C (where-to-start): viewed 21 → started 8 (38.1%, was 56%) → completed 8 (100% of started; 38% overall)
  KEY METRICS:
  - lp:form ratio: 55/97 = 0.57:1 (INVERTED from 25.8:1) — on-site form now primary channel
  - Backend fail rate: 11/(97+55+11) ≈ 6.7% (was 1.5% — creeping up from near-zero; was 35.7% at peak ⚠ watch)
  - Doctor→book CTA: 31.4% (was 73% — rate collapse, absolute stable)
  - Riya discovery rate: 10/8167 = 0.12% (was 14/6342 = 0.22%, -45%)
  WoW FLAGS (>20% vs 2026-07-08 — NOTE: 3-week gap, not 1 week):
  🚨 form_submitted +1,840% (5→97) — structural shift; on-site form now primary lead channel (ads paused → LP dies → on-site takes over). Verify Freshsales.
  ⚠⚠ lp_form_submitted -57.4% (129→55) — expected given ads pause; LP without paid traffic has no volume
  ✅✅ doctor_profile_viewed +118% (592→1,293) — T9 content sprint driving organic doctor discovery
  ✅ page views +28.8% (6,342→8,167) — organic traffic growing strongly (+~10%/wk avg)
  ✅ where_to_start +31% (16→21) — internal linking working
  ⚠ lead_create_failed +450% (2→11) — backend fail rate 1.47%→6.7%; still far below peak (35.7%) but trend reversal worth watching
  ⚠ riya_page_viewed -29% (14→10) — tiny absolute, inconclusive; more traffic diluting discovery rate
  ⚠⚠ doctor→book CTA rate -57% (73%→31%) — rate drop is structural (denominator doubled), not a signal that commercial visitors are converting worse; absolute book clicks stable
  ⚠ page→book CTA rate -27% (12.3%→9.0%) — intent dilution from SEO discovery traffic (expected)
  IMPLICATIONS:
  - Total leads (~152 unique submitters) may be the best weekly number recorded — but quality unknown. Verify Freshsales URGENTLY.
  - On-site booking form conversion jump (book CTA→submit 0.5%→5%) suggests either form placement improved or a tracking fix fired. Investigate what changed.
  - Doctor profile content strategy is working for discovery but not converting at the old commercial rate — this is expected and acceptable; the doctor pages serve the top-of-funnel SEO role.
  - Riya page continues to under-index; needs dedicated internal linking / feature placement.


2026-07-08T10:00 IST | T15 SCHEDULED — weekly conversion monitor | 7d unique users |
  VOLUME:
  - $mp_web_page_view: 6,342 (-0.9% WoW, stable)
  - blog_viewed: 1,246 | doctor_profile_viewed: 592 (+6.1%) | treatment_page_viewed: 294 (+19%) | illness_page_viewed: 118 (-26.7%⚠) | riya_page_viewed: 14 (+133%✅✅ — first real break from invisibility) | where_to_start_page_viewed: 16 (-6%, stable)
  - book_appointment_clicked: 784 (+2.6%, stable ✅)
  - form_submitted: 5 (+25%) | lp_form_submitted: 129 (-14.6%⚠)
  - form_started: 15 (stable) | form_error: 2 | lead_create_failed: 2 (-88%✅✅✅ — continued recovery)
  - whatsapp_clicked: 104 (+13%) | call_clicked: 53 (-1.9%, stable) | cta_clicked: 112 (-11%)
  FUNNELS:
  - A (main): page view 6,342 → book CTA 779 (12.3%, was 11.8%✅) → form_submit 4 (0.5% of book CTA, ~0.06% of page views)
  - B (doctor-driven): doctor_profile 592 → book CTA 431 (73.0%, was 66%✅✅ — new high) → form_submit 4 (0.9%)
  - C (where-to-start): viewed 16 → started 9 (56%) → completed 9 (100% of started; 56% overall, was 65%)
  KEY METRICS:
  - lp:form ratio = 25.8x (129/5) — down from 37.75x (on-site form marginally less irrelevant)
  - Backend fail rate: 2/(129+5+2) = 1.47% — DOWN from 9.9% ✅✅✅ (continued recovery; now effectively negligible)
  - Doctor→book CTA: 73% (was 66%, new high ✅✅)
  - Riya discovery rate: 14/6342 = 0.22% (was 0.094% — +134% ✅✅)
  WoW FLAGS (>20%):
  ✅✅✅ lead_create_failed -88% (17→2) — backend fail rate 9.9%→1.5%; holding and improving
  ✅✅ riya_page_viewed +133% (6→14) — first meaningful jump; may be responding to content/internal linking
  ✅✅ doctor→book CTA +10.6% (66%→73%) — new record high; doctor pages = strongest conversion path
  ⚠ illness_page_viewed -26.7% (161→118) — high-intent pages losing traffic; check ranking
