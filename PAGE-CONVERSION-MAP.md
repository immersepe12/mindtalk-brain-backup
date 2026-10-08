# Page Conversion Map — Updated 2026-10-07 (W41)

**Source:** T19 Conversion Intelligence. Site-level run (W41). 14-day aggregate: Sep 24 – Oct 7, 2026 (covers W40+W41; W40 previously logged as MCP_BLOCKED but data confirmed present in Mixpanel). Per-page UTM campaign breakdown used for page-type tier inference. Organic vs paid HARD SEPARATION applied per 2026-06-22 rule.
**Read by:** T10 Strategist (action scoring), T18 Professional Input (Leaky Bucket queue), T5 New Content Discovery (pattern weighting).

---

## Site-Level KPIs (W41 — 14d aggregate, /week est in brackets)

| Metric | W41 (14d total) | /week est | vs W39 (7d) |
|---|---|---|---|
| Unique visitors | 24,210 | ~12,105 | +17.3% 🟢 |
| Total book clicks (unique) | 1,895 | ~948 | 959 (-1.2%) |
| Organic book clicks (unique) | 1,240 | ~620 | — |
| Organic payments | 360 | ~180 | 202 (-10.9%) 🔴 |
| Organic bookings | 405 | ~203 | 230 (-11.7%) 🔴 |
| Total payments | 369 | ~185 | 202 |
| Total bookings | 417 | ~209 | 230 |
| mindtalk_web payments | 5 | ~2.5 | 0 (RECOVERY 🟢) |
| mindtalk_web bookings | 7 | ~3.5 | 1 |
| chatgpt.com book clicks (total) | 615 | ~307 | 354 (-13.3%) |
| chatgpt.com book clicks (unique) | 167 | ~84 | 91 (-7.7%) |
| chatgpt.com payments | 8 | ~4 | — |
| chatgpt.com bookings | 9 | ~4.5 | — |
| Perplexity book clicks | 8 | ~4 | 1 (growing 🟢) |
| Assessment Completed | 889 | ~445 | 367 (+21.3% 🔥 ALL-TIME HIGH) |
| Started Journey Task | 35 | ~18 | 27 (-33% 🔴) |
| Stress Tracker Started | 108 | ~54 | 51 (+6%) |
| Rage clicks (unique) | 490 | ~245 | 247 (flat ✅) |
| Dead clicks (unique) | 2,372 | ~1,186 | 1,141 (+3.9%) |
| Rage rate | — | ~2.0% | 2.4% (improving ✅) |
| Dead rate | — | ~9.8% | 11.1% (improving, near threshold 🟡) |
| Median intent rate | — | ~7.8% | 9.3% (-1.5pp 🔴) |

**Note:** W38 + W40 both had no data (Mixpanel billing blocks). W40 data now confirmed present (192 payments, 2,705 book clicks that week). W41 is compared to W39 (last clean week). 14-day window captures both W40+W41.

---

## Attribution Layers (W41 — 14d)

| Layer | Book clicks (unique 14d) | /week est | Payments (14d) | Notes |
|---|---:|---:|---:|---|
| mindtalk_web (true SEO-attributed) | — | — | 5 | UTM chain recovering (+2.5/week vs W39 0) |
| chatgpt.com (AI search, utm_source) | 167 | ~84 | 8 | P5 W9 sustained; weekly rate -8% vs W39 |
| Paid Google Ads (estimated) | ~655 | ~328 | ~9 | NND+FTA campaigns; excluded from organic |
| Organic/undefined (no utm_paid) | 1,240 | ~620 | 360 | 98% undefined utm_medium |
| Perplexity | 8 | ~4 | — | Growing AI channel; 4x W39 rate |

**UTM medium breakdown (organic payments 14d):**
- undefined: 353/360 = 98% (UTM chain still broken through checkout — PERSISTENT)
- doctor: 3
- homepage: 1
- google_ads: 2
- site: 1
- **UTM content: 100% undefined** (CTA position tracking completely absent)

---

## UTM Campaign Attribution (book clicks — page-type inference)

| Campaign type | Total clicks (14d) | Notes |
|---|---:|---|
| Undefined (no campaign) | 3,609 | Organic SEO / direct |
| Empty string | 546 | Organic GMB / no-tag |
| NND sitelink (Google Ads) | 9 | Paid (excluded from organic) |
| burnout (organic illness) | 17 | anxiety_center + burnout signals |

---

## Tier Classifications (W41)

### 🟢 Goldmines (2 pages — protect + amplify)

| URL | Notes |
|---|---|
| /treatments/cbt-therapy | Consistent high-intent treatment page; confirmed W9 |
| /doctors/* cluster + find-therapist | Doctor listing hub — majority of organic booking intent; P2 CONFIRMED W9 |

### 🟡 Rockets (5 pages — drive traffic)

| URL | Notes |
|---|---|
| /illnesses/anxiety | Persistent organic signal; burnout campaign 17 clicks |
| /illnesses/depression | High intent organic; needs traffic |
| /blogs/chatgpt-cited pages | chatgpt.com 307 book clicks/week; revenue generating (8 payments/14d) |
| /illnesses/burnout | burnout campaign 17 organic clicks; consistent |
| /doctors/therapists-in-delhi | Delhi NCT 124/week organic (P15 WATCH — organic share lower than W39 total) |

### 🔵 Engagement Engine (NEW CATEGORY — W41)

| URL | Notes |
|---|---|
| Assessment landing pages | 445/week Assessment Completed — ALL-TIME HIGH; Journey Task still low (18/week) |

### 🔴 Leaky Buckets (0 organic SEO pages)

App UX pages (consult subdomain) have dead-click issues but outside organic SEO scope.

### ⚫ Dead Weight

/lps/* — paid landing pages; exclude from organic SEO analysis.

---

## UX Friction Summary (W41)

- **Rage rate:** ~2.0% (245 unique/week / 12,105 visitors) — BELOW 5% threshold ✅ (improving from W39 2.4%)
- **Dead rate:** ~9.8% (1,186 unique/week / 12,105 visitors) — near 10% threshold 🟡 (improving from W39 11.1%)
- Dead clicks total: 2,372 / 14d (persistent; slight improvement trend)
- Rage clicks total: 490 / 14d (stable/improving)
- **Trend:** UX friction improving week-over-week. If W42 dead rate stays <10%, can de-escalate product flag.
- **Action:** Continue monitoring. See brain/UX-FRICTION-PAGES.md for page-level breakdown.

---

## W40 Data Recovery Note

W40 (Sep 28 – Oct 4) was logged as "MCP_BLOCKED" in page-conversion-history.md, but Mixpanel line chart confirmed: **192 unique payments + 2,705 total book clicks** that week. The billing block prevented T19 from running, but data ingestion continued normally. W41 14d aggregate captures both W40+W41 data. W40 classifications held from W39 are still valid.
