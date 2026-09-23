# Page Conversion Map — Updated 2026-09-23 (W39)

**Source:** T19 Conversion Intelligence. Site-level run (W39). Per-page UTM campaign breakdown used for page-type tier inference. Tier classifications held from W34 last full per-page run; updated where W39 data gives clear signal.
**Read by:** T10 Strategist (action scoring), T18 Professional Input (Leaky Bucket queue), T5 New Content Discovery (pattern weighting).

---

## Site-Level KPIs (W39)

| Metric | W39 | W37 | WoW (vs W37) |
|---|---|---|---|
| Unique visitors | 10,324 | 9,350 | +10.4% 🟢 |
| Total book clicks | 2,697 | 2,647 | +1.9% |
| Unique book clicks | 959 | 925 | +3.7% |
| Intent rate (total/visitors) | 26.1% | 28.3% | -2.2pp 🔴 (lower-intent traffic returning) |
| form_submitted | 113 | — | — |
| whatsapp_clicked | 93 | — | — |
| call_clicked | 51 | — | — |
| Payments (unique) | 202 | 177 | +14.1% 🟢 RECORD-TIED (=W36) |
| Bookings (unique) | 230 | 204 | +12.7% 🟢 |
| mindtalk_web payments | 0 | 3 | ↓ (UTM chain still sparse) |
| mindtalk_web bookings | 1 | 5 | ↓ |
| chatgpt.com book clicks | 354 total / 91 unique | 286 total | +23.8% 🔥 P5 W8 |
| Assessment Completed | 367 | 303 | +21.1% 🟢 RECOVERY |
| Started Journey Task | 27 | 30 | -10% (still at emergency low) |
| Stress Tracker Started | 51 | 50 | flat |
| Rage clicks | 750 total / 247 unique | 729 / 479 | stable |
| Dead clicks | 4,883 total / 1,141 unique | 4,635 / — | +5.3% (persistent) |

**Note:** W38 had no data (Mixpanel billing block). W39 is compared to W37 (2-week gap).

---

## Attribution Layers (W39)

| Layer | Book clicks (total) | Book clicks (unique) | Payments | Notes |
|---|---:|---:|---:|---|
| mindtalk_web (true SEO-attributed) | — | 0 | 0 | UTM chain still not flowing |
| chatgpt.com (AI search, utm_source) | 354 | 91 | — | P5 W8, growing |
| Paid Google Ads (named campaigns) | ~578 est | ~294 unique | 1 | NND+FTA Bangalore campaigns |
| Organic/undefined (no utm_campaign) | 2,118 | ~665 est | 201 | 78.5% of all book clicks |
| Direct / Other | — | — | — | — |
| **Organic-attributable total** | **2,118** | **~665 est** | **~201** | Paid excluded |

**UTM medium breakdown (payments):**
- undefined: 196/202 = 97% (UTM chain broken through checkout — persistent gap)  
- organic: 5
- google_ads: 1
- **UTM content: 100% undefined** (CTA position tracking completely absent)

---

## UTM Campaign Attribution (book clicks — page-type inference)

| Campaign type | Total clicks | % of total | Source |
|---|---:|---:|---|
| Undefined (no campaign) | 1,822 | 67.5% | Organic SEO / direct |
| Empty string | 296 | 11.0% | Organic GMB / no-tag |
| NND + FTA Bangalore (Google Ads) | ~578 | 21.4% | Paid campaigns |
| Organic illness pages (anxiety/depression/burnout) | ~47 | 1.7% | anxiety_center(14)+anxiety_treatment(9)+depression_treatment(18)+burnout(6) |

---

## Tier Classifications (W39)

### 🟢 Goldmines (2 pages — protect + amplify)

| URL | Notes |
|---|---|
| /treatments/cbt-therapy | Consistent high-intent treatment page; depression_treatment campaign (18 clicks organic) |
| /doctors/* cluster + find-therapist | Doctor listing hub — majority of organic booking intent flows here; P2 CONFIRMED 8 WEEKS |

### 🟡 Rockets (5 pages — drive traffic)

| URL | Notes |
|---|---|
| /illnesses/anxiety | 14+9=23 organic clicks from anxiety campaigns — high intent, needs traffic |
| /illnesses/depression | 18 organic clicks (depression_treatment) — high intent |
| /blogs/chatgpt-cited pages | AI-search cited content (chatgpt.com 354 book clicks); real revenue emerging |
| /illnesses/burnout | 6 organic clicks from burnout campaign; small but consistent |
| /doctors/therapists-in-delhi | Delhi NCT 214 book clicks (+43% vs W37) — P15 re-emerging strong |

### 🔴 Leaky Buckets (0 organic SEO pages — app UX issues tracked separately)

App UX pages (consult.cadabams.com) have severe dead-click rates but outside organic SEO scope.

### ⚫ Dead Weight

/lps/* — paid landing pages; exclude from organic SEO analysis.

---

## UX Friction Summary (W39)

- **Rage rate:** 2.4% (247 unique / 10,324 visitors) — below 5% threshold ✅
- **Dead rate:** 11.1% (1,141 unique / 10,324 visitors) — ABOVE 10% threshold 🔴
- Dead clicks total: 4,883 (persistent; slight +5.3% from W37)
- Rage clicks total: 750 (stable; slight +2.9% from W37)
- **Action:** Product/dev flag maintained — see brain/UX-FRICTION-PAGES.md

