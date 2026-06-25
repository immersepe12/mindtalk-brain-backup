
## 2026-06-17 — Conversion data refreshed (T19 INAUGURAL, LIMITED_BASELINE)
- Goldmines: /doctors (321% intent), /experts/expert-therapists (62%)
- Rockets (high intent, grow traffic): /doctors/telugu-speaking-doctors (95%), /doctors/tamil-speaking-doctors (91%)
- Leaky (verify instrumentation first): / homepage (298v, 0 tracked book intent)
- Dead weight (de-prioritize for conversion): 6 high-traffic blogs + /treatments/drug-deaddiction (0 book intent — discovery content)
- Geo concentration: Bengaluru 65% of all intent / Karnataka 67%. Mumbai (69%), Chennai (71%), Delhi (55%) high-intent + low-volume = GROW. Hyderabad/Telangana 11% = LEAK.
- New patterns (week 1/3, seed only): language-specific doctor pages convert hot; doctor hub = goldmine; blogs ≈ 0 booking intent.
- Proposed content angles for T5: 2 (kannada/malayalam/hindi-speaking-doctor pages; metro doctor pages) — locked, need ≥3 wks.
- ⚠️ Caveats: book_appointment-only intent this week (lp_form/whatsapp/call site-level). Homepage 0-intent likely a tracking gap. Singapore 213v + China = bot noise, excluded.
- Cross-domain attribution (Cadabams consult 3986277): UNAVAILABLE — project not visible in MCP today; revenue-validated layer deferred to next run.

## 2026-06-25 11:00 IST — T19 W26 run (SECOND RUN — paid/organic separation ACTIVE)

**Data period:** Jun 18-24, 2026. Unified project 4011856. 5,620 unique visitors (+47.4% WoW).

**Key signals this week:**
- Paid/organic separation confirmed: lp_form_submitted = 96.4% paid. book_appointment_clicked organic = 57.6% (1,026 events). Revenue events 100% organic (ads paused).
- UTM attribution LIVE (first full week): 15 payments via mindtalk_web UTM. Doctor card CTAs = 66.7% of attributed payments. Homepage hero = 20%.
- CRITICAL UX friction: booking/53196 has 444 rage+dead clicks — single doctor with broken slot availability. find-therapist wizard 293 friction events. Dev review required.
- Hyderabad REVERSAL: +350% WoW (16 → 72 clicks). Telugu-speaking-doctor page growth driving Hyderabad bookings. Was W25's worst geo leak. Now #4 city.
- AI search channel detected: chatgpt.com = 57 book_appointment_clicked (3.2% of total), larger than any single city except Bengaluru/Delhi/Mumbai. Mindtalk.in appearing in ChatGPT mental health responses.
- NRI: UK+US+Gulf = ~84 international book intent events. Persistent across weeks.

**Pattern updates (week 2):**
- Language-specific doctor pages: STRENGTHENED (Telugu +59.5% visitors, Tamil +82.9%). Intent softened (95%→72.9%) but still top Rockets at 2× site median. 1 more week needed before T5 unlock.
- Doctor hub /doctors Goldmine: STRENGTHENED (intent 321%→390% despite -21.8% visitor drop = qualification effect).
- Blogs≈0 intent: CONFIRMED again.
- Geo×page paradox: RESOLVED — Hyderabad +350%, Telugu pages working for Hyderabad users too.
- NEW: AI search (chatgpt.com) seeded as Pattern 5. Need 2 more weeks.

**Reclassifications vs W25:**
- Homepage: Leaky → Tracking Gap (3 real payments confirmed via UTM). NOT leaky.
- /lps/*: Dead → Paid LP (not organic; 96.4% paid form submissions). Exclude from organic tier ranking.

**Content angles proposed:** 4 total (2 week-2, 2 new week-1 seeds). None yet actionable for T5 (need ≥3 weeks).

## 2026-06-17 11:00 IST — Scheduled T19 fire (addendum to morning inaugural)
- No re-classification: inaugural full run already completed this morning on the current 7-day window (same data, same week). Tiers/GEO/patterns unchanged — see PAGE-CONVERSION-MAP.md / GEO-CONVERSION-MAP.md.
- Cross-domain attribution recheck: STILL BLOCKED. Project 3986277 (Cadabams consult) absent from accessible-project list again. Investigated whether consult booking events migrated to another accessible US project: 4026555 cadabams-org (no appointment/book events), 4015752 professionals (none), 4013942 cadabams hospitals (has `book_appointment_clicked` but that is the hospital-site funnel, NOT consult `Appointment Booked`/`Doctor Booking Page Viewed` — wrong project for Mindtalk→consult attribution), 3984638 cadabams group (EU-region-locked, needs mcp-eu.mixpanel.com). Revenue-validated layer remains deferred until 3986277 is restored or the consult funnel is located in an accessible US project.
