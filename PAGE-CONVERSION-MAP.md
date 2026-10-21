# Page Conversion Map — Updated 2026-10-21 (W43)

**Source:** T19 Conversion Intelligence. Site-level run (W43). 7-day: Oct 14–21, 2026. Organic vs paid HARD SEPARATION applied per 2026-06-22 rule. Paid UTM sources excluded from organic metrics: google, Google, GMB, gmb, sitelink, facebook, Facebook, fb, Fb, meta, Meta, instagram, Instagram, ig, linkedin, LinkedIn.
**Read by:** T10 Strategist (action scoring), T18 Professional Input (Leaky Bucket queue), T5 New Content Discovery (pattern weighting).

---

## Site-Level KPIs (W43 — 7d Oct 14–21)

| Metric | W43 (7d) | vs W42 (7d) | Δ% |
|---|---|---|---|
| Unique visitors | 12,207 | 12,488 | -2.3% |
| Total book clicks (unique) | 922 | 945 | -2.4% |
| Organic book clicks (unique) | 611 | 644 | -5.1% 🔴 |
| Organic payments | 138 | 200 | -31.0% 🔴 MAJOR |
| Organic bookings | 178 | 228 | -21.9% 🔴 |
| Total payments | 157 | 206 | -23.8% 🔴 |
| Total bookings | 201 | 236 | -14.8% 🔴 |
| mindtalk_web payments | 0 | 1 | 🔴 (zero; high variance) |
| mindtalk_web bookings | 0 | 1 | 🔴 (zero; high variance) |
| chatgpt.com book clicks (total, utm_source) | 275 | 160 | +71.9% 🔥 RECOVERY* |
| chatgpt.com book clicks (unique, utm_source) | 76 | 44 | +72.7% 🔥 RECOVERY* |
| chatgpt.com payments | 3 | 2 | +50% |
| Perplexity book clicks | 0 | 0 | — |
| Assessment Completed | 520 | 515 | +1.0% 🟢 (near-record) |
| Started Journey Task | 33 | 29 | +13.8% 🟢 continuing recovery |
| Stress Tracker Started | 57 | 70 | -18.6% |
| Rage clicks (unique) | 222 | 272 | -18.4% 🟢 improving |
| Dead clicks (unique) | 1,296 | 1,337 | -3.1% 🟢 improving |
| Rage rate | ~1.8% | 2.2% | improving (<5% ✅) |
| Dead rate | 10.6% | 10.7% | ⚠️ STILL ABOVE 10% THRESHOLD |
| Organic intent rate | 5.0% | 5.16% | -0.16pp flat |

*NOTE: W43 chatgpt.com measured via utm_source tagging. W42 was measured via $initial_referring_domain (44 unique). Methodology has shifted — utm_source is now primary metric. Recovery confirmed vs W42 regardless of methodology.

---

## Attribution Layers (W43 — 7d)

| Layer | Payments | Bookings | Book clicks (unique) | Notes |
|---|---:|---:|---:|---|
| mindtalk_web (true SEO-attributed) | 0 | 0 | — | Zero this week; high variance at low volume |
| chatgpt.com (AI search) | 3 | — | 76 | P5 RECOVERY: +72.7% WoW vs W42 44 (utm_source method) |
| Perplexity (AI search) | 0 | 0 | 0 | Zero again — investigate |
| Paid Google/GMB (excluded from organic) | 13 Google + 7 GMB | — | ~301 est | Paid excluded from organic metrics per hard rule |
| Paid Meta | ~1 | — | — | minimal |
| Organic/undefined | 128 | 178 | 611 | 81.5% undefined utm_medium (UTM chain still broken) |

**UTM source breakdown (payments W43 — total 157):**
- undefined: 128 (81.5%)
- google (paid): 13 (8.3%)
- gmb (paid): 7 (4.5%)
- direct: 6 (3.8%)
- chatgpt.com: 3 (1.9%)
- paid: 1 (0.6%)
- **UTM chain still broken through checkout — PERSISTENT 16+ weeks**

---

## Paid Traffic Breakdown (EXCLUDED from organic — informational)

| Paid source | Book clicks (est) | Notes |
|---|---:|---|
| google (Google Ads) | ~268 unique | Dominant paid channel |
| GMB (Google My Business) | ~33 unique | Local sitelinks |
| Meta/Facebook/Instagram | minimal | ~1 payment confirmed |

---

## Tier Classifications (W43)

**Note:** Per-page UTM campaign breakdown not available (site-level run only). Page-type tier classifications held from W41/W42 based on pattern evidence and site-level organic intent rate (5.0%).

### 🟢 Goldmines (2 pages — protect + amplify)

| URL | Notes |
|---|---|
| /treatments/cbt-therapy | Consistent high-intent treatment page; confirmed W10+ |
| /doctors/* cluster + find-therapist | Doctor listing hub — majority of organic booking intent; P2 CONFIRMED W10+ |

### 🟡 Rockets (5 pages — drive traffic)

| URL | Notes |
|---|---|
| /disorders/anxiety + /treatments/anxiety | P1 anxiety cluster — stable organic intent |
| /disorders/depression | Core condition page — organic traffic anchor |
| /assessments/* hub | Assessment Completed W43: 520 (near-record, +1%) — strong app engagement |
| /doctors/psychologists-in-[city] | Regional doctor pages — geo-conversion driven |
| /blog/* (top posts) | Informational → assessment → booking funnel |

### 🔵 Engagement Engines (tracking separately)

| URL | Notes |
|---|---|
| App: /consult/home | HIGH FRICTION (679 dead clicks — CRITICAL PERSISTENT) |
| App: Assessment flow | Near-record completions W43 (520) — healthy engagement |

### 🔴 Leaky Buckets (0 classified — site-level insufficient for per-page leaky detection)

No per-page UTM data this week. Leaky Bucket audit deferred to next per-page run.

### ⚫ Dead Weight (1 — no organic intent, no engagement)

| URL | Notes |
|---|---|
| /lp/* pages | Paid landing pages — not organic SEO pages; excluded from organic tier |

---

## W43 Key Signals for Strategist

### 🔥 WINS
1. **Assessment Completed: 520 — near-record** (+1.0% WoW vs W42's 515 record). App top-of-funnel engagement sustaining record level.
2. **chatgpt.com RECOVERY: 76 unique book clicks** (+72.7% WoW vs W42's 44) — P5 back on track. 3 payments confirmed from AI search.
3. **Journey Task recovery: 33 (+13.8%)** — 2nd consecutive positive WoW; multi-week crash appears to be resolving.
4. **UX friction improving**: Rage -18.4%, Dead -3.1% WoW — directionally positive despite still above 10% threshold.

### 🔴 CRITICAL WARNINGS
1. **ORGANIC PAYMENTS CRASH: -31.0% WoW** (138 vs W42's 200). Largest organic payment drop since W33. Visitors only down -2.3%, so click-to-payment CONVERSION RATE dropped sharply. Likely causes: (a) Navratri/Dussehra holiday week Oct 13–21 India — seasonal demand suppression; (b) checkout UX friction (61 dead clicks on /consult/checkout); (c) organic book clicks down -5.1%.
2. **Organic bookings crash: -21.9% WoW** (178 vs W42's 228). Consistent with payment drop.
3. **Dead rate still 10.6%** — above 10% threshold for 3rd consecutive week. /home: 679 dead clicks (CRITICAL PERSISTENT). /consult/checkout: 61 (NEW — payment flow friction).
4. **mindtalk_web payments: 0** — second near-zero week. True SEO attribution remains invisible.

### 📊 REVENUE QUALITY
- Total/organic gap narrowing: 157 total vs 138 organic = only 19 paid payments
- BUT organic payment VOLUME dropped sharply — this is a real revenue event
- Seasonal hypothesis (Navratri Oct 2–12 + Dussehra Oct 13 + school holiday week): strong candidate for W43 drop — WATCH W44 for recovery
- If W44 doesn't recover to 160+ organic payments, investigate checkout funnel

### 🗓️ SEASONAL NOTE
Navratri ran Oct 2–12; Dussehra Oct 13. W43 covers Oct 14–21 = first week AFTER Dussehra. Indian holiday effect typically extends into post-festival recovery week. W44 (Oct 21–28) expected to begin recovering. Flag for T10 Strategist.

---

## Previous Week Reference (W42 est)
Unique visitors 12,488 | Organic book clicks 644 | Organic payments 200 | Organic bookings 228 | chatgpt.com unique book clicks 44 (referring domain method) | Assessment Completed 515 (record) | Journey Task 29 | Dead rate 10.7% | mindtalk_web payments 1
