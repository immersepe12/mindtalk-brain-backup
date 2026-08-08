# Strategist Signal Feed

**Written by:** T19 Conversion Intelligence (weekly, Wednesdays)
**Read by:** T10 Strategist
**Purpose:** High-priority signals that need strategic decision or immediate action. Cleared each week after T10 reads.

---

## W31 signals (2026-07-29) — FOR T10 STRATEGIST

### 🔴🔴 CRITICAL: /prescriptions page broken (1,014 friction events)
- consult.cadabams.com/prescriptions: 887 dead + 127 rage = #1 UX crisis in T19 history
- Brand new this week — something deployed broken
- **Action:** Escalate to app dev IMMEDIATELY. This is leaking post-engagement, high-intent users.

### 🔴🔴 CRITICAL: UTM chain broken on expert-page ad campaigns
- 215/232 W31 appointments = undefined UTM source
- New Pan-India Plan campaigns (NND_Psychologist, FTA_Professional_Therapist, etc.) landing on /experts/* pages without UTM pass-through to consult.cadabams.com
- Can't separate organic from paid performance while this is broken
- **Action:** Fix UTM tags on all CTA links on /experts/* ad landing pages. Add utm_source=expert_ads&utm_medium=paid&utm_campaign=[campaign_name] to every booking CTA on those pages.

### 🔴 HIGH: Homepage hero attribution collapsed (9→0 payments)
- Pattern 7 demoted. mindtalk_web-attributed payments fell 22→15 entirely due to homepage hero dropping 9→0.
- **Investigate:** (a) Was homepage hero CTA changed/removed? (b) Is utm_source=mindtalk_web&utm_medium=homepage still being appended to the hero CTA link? (c) Was W28 anomaly?
- Doctor card still solid at 13/wk — only mindtalk_web decline is via homepage.

### 🟡 HIGH: /home dead click explosion (+421%)
- consult.cadabams.com/home dead clicks: 129→673 in one week
- New ad campaigns routing users through /home after sign-up or post-session
- **Action:** Audit /home navigation elements. Check if W29-W31 feature deployment broke click handlers.

### 🟡 MEDIUM: find-therapist still broken (4th week, 419 events)
- consult.cadabams.com/consult/find-therapist has had 300-400+ dead clicks for 4 consecutive weeks
- **Action needed from dev:** Inspect filter UI and therapist card click handlers. 4 weeks = not being prioritized.

### 🟡 MEDIUM: checkout dead clicks stuck (3+ weeks, ~70 events)
- Every dead click at checkout = direct payment abandoned
- **Action:** Inspect payment form CTA and submit button handlers.

---

## Positive signals (maintain momentum)

### 🟢 Revenue records W31
- Payment Successful 193 (+63.6% vs W28) — best week ever
- Appointment Booked 232 (+116.8% vs W28) — best week ever
- Organic book clicks 1,348 (+7.9%) — steady organic growth
- Cause: ads re-activated + organic growth. Revenue is real.

### 🟢 chatgpt.com now 10.2% of all book clicks (203 W31, +31%)
- P5 Week 5 confirmed. AI citation growing without any targeted AI SEO content.
- T5 proposal: create AI-citable authority pages to compound this channel.

### 🟢 Geographic diversification (Bengaluru 60.2%→51.3%)
- Delhi +49%, Kolkata +193%, Mumbai +36% = national expansion
- Kolkata 41 clicks is largest single-week new market entry since Vijayawada W27 (which was noise)
- **Action:** T5 should consider `/doctors/psychologists-in-kolkata` — but confirm W32 first.

### 🟢 US market ~100 book clicks (first major week)
- California 26, San Francisco 16, Texas 16, Illinois 15, NY 12
- Zero US-specific content exists — pure organic NRI demand
- P10 seed (Week 1). If W32 confirms: propose "online therapy for Indians in USA" to T5.

### 🟢 Kerala P8 expanding (20 clicks, Kochi+TVM+Kozhikode)
- W2 of Kerala market signal. Malayalam page still #1 proposed T5 angle.
- One more week → confirm and fire.

---

## Standing instructions for T10

1. **Doctor content > all other content types.** 58 doctor_card payments over 5 weeks = highest-confidence revenue attribution.
2. **Every content piece must mandate internal links to /doctors or /experts.** Pattern 3 (blogs=0 direct booking) confirmed 5 weeks.
3. **AI search channel (chatgpt.com) = new organic KPI.** Add to weekly scorecard. Currently 10.2% of book clicks.
4. **Language pages are the single highest-ROI SEO action.** Malayalam + Kannada + Hindi pages = top 3 T5 proposals, all at +30 pts.
5. **Expert pages + ads = UTM broken.** Organic + paid attribution is polluted. Fix before W32.
6. **Supermetrics trial expired.** GA4 data unavailable. Mixpanel remains sole conversion source.

---

## W32 Update — 2026-08-05 11:00 IST

### Revenue: NEW RECORDS (both metrics)
- Payments: **205** (+6.2% WoW) — all-time high
- Bookings: **264** (+13.8% WoW) — all-time high
- Organic-attributable book clicks: **1,369 / 2,035** (67.3%)
- Paid book clicks: **666** (32.7%) — UTM sources: google/facebook/meta/instagram

### Tier Classifications (W32)
| Tier | Pages |
|---|---|
| 🟢 Goldmine | /doctors/* (60 cumul payments 6wks), /experts/* (ads + organic) |
| 🟡 Rocket | /doctors/telugu-speaking-doctors (Hyderabad 83 clicks), /doctors/tamil-speaking (WATCH — Tamil crash 83→27) |
| 🔵 Engagement Engine | /blogs/* (P3 confirmed 6wks — top-of-funnel only, no direct booking) |
| 🔴 Leaky Bucket | /appointments (762 dead clicks CRITICAL), /assessments (725 dead clicks CRITICAL) |
| ⚫ Dead Weight | /illnesses/*, /treatments/*, /lps/* |

### 🚨 Alerts requiring action
1. **UX CRITICAL**: /appointments (814 rage+dead) + /assessments (803 rage+dead) — simultaneous crash = deploy regression. Check deploys Jul 28–Aug 4.
2. **doctor_card UTM crash**: 13 → 5 payments. Hypothesis: paid /experts ads overwrite session UTM on /doctors navigation. Monitor W33.

### Geo highlights
- Bengaluru: 1,156 clicks (58.7% share — recovery from 51.3%)
- Doha/Qatar: 47 clicks (P11 stable — content gap = highest ROI)
- Australia: 60 clicks (NSW+VIC — P12 Week 2)
- Tamil Nadu: 27 clicks (CRASH from 83 — P1 Tamil on HOLD)
- Kolkata: 7 clicks (CRASH from 41 — hold /psychologists-in-kolkata proposal)

### New patterns (W32)
- **P11 (Doha)**: Week 2 stable (47 book clicks, 0 content)
- **P12 (Australia NRI)**: Week 2 growth (60 clicks, 0 content)
- **P13 (Riya revenue)**: Week 1 seed (1 payment, utm_medium=riya)

### Content proposals queued → T5
- URGENT: Gulf diaspora content (Qatar 47 + UAE 16 = 63 NRI clicks, 0 content)
- WATCH: Australia NRI (confirm W33 before proposing)
- HOLD: /psychologists-in-kolkata (Kolkata crashed 41→7)
- HOLD: Tamil-speaking doctor pages (Tamil crashed 83→27)
- ACTIVE: Kannada/Malayalam/Hindi doctor pages (+30 pts, unchanged)
- ACTIVE: Delhi/Mumbai/Hyderabad psychologist pages (unchanged)
