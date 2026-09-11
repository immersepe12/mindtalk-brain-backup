# Page Conversion Map — Updated 2026-09-09 (W37)

**Source:** T19 Conversion Intelligence. Site-level only this run (per-page Mixpanel queries deferred due to query budget). Tier classifications held from W34 last full per-page run.
**Read by:** T10 Strategist (action scoring), T18 Professional Input (Leaky Bucket queue), T5 New Content Discovery (pattern weighting).

---

## Site-Level KPIs (W37)

| Metric | W37 | W36 | WoW |
|---|---|---|---|
| Unique visitors | 9,350 | ~10,715 (est) | -12.7% |
| Total book clicks | 2,647 | ~2,582 (est) | +2.5% |
| Unique book clicks | 925 | — | — |
| Intent rate (total/unique) | 28.3% | 24.1% | +4.2pp 🔺 NEW HIGH |
| Payments (unique) | 177 | 200 | -11.5% |
| Bookings (unique) | 204 | 237 | -13.9% |
| mindtalk_web payments | 3 | 5 | -40% |
| mindtalk_web bookings | 5 | — | — |
| chatgpt.com book clicks | 286 | 211 | +35.5% RECOVERY |
| chatgpt.com payments | 3 | — | AI-rev record |
| chatgpt.com bookings | 4 | — | AI-rev record |
| Assessment Completed | 303 | ~490 est | -38% |
| Started Journey Task | 30 | 124 | -75.8% 🔴 EMERGENCY |
| Stress Tracker Started | 50 | — | — |
| Rage clicks | 729 | 479 | +52.2% 🔴 |
| Dead clicks | 4,635 | 3,761 | +23.2% 🔴 |

---

## Attribution Layers (W37)

| Layer | Book clicks | Payments | Bookings |
|---|---:|---:|---:|
| mindtalk_web (true SEO-attributed) | ~30 (domain) | 3 | 5 |
| chatgpt.com (AI search, utm_source) | 286 | 3 | 4 |
| chatgpt.com (AI search, by domain) | 60 | — | — |
| gemini.google.com (by domain) | 25 | — | — |
| Organic (undefined utm_source) | 1,463 | 194 | 252 |
| Paid (google/Google/GMB/sitelink/ig) | 670 | 3 | 4 |
| Direct | 208 | — | — |
| **Organic-attributable total** | **1,977** | **~199** | **~261** |

**Organic book clicks W37: 1,977** (paid: 670 = 25.3% of total — ads contribution lower than W34 peak)

---

## UTM Medium Attribution (payments)

| Medium | Payments | Notes |
|---|---:|---|
| undefined | 198 | UTM chain not preserved through checkout (persistent gap) |
| doctor | 2 | Doctor page CTAs working |
| organic | 2 | Tagged organic |
| google_ads | 1 | Paid bleed |
| site | 1 | |

**UTM medium data is sparse** — 198/204 payments have no medium. This is a persistent tracking gap. The UTM source is captured (mindtalk_web=3, chatgpt.com=3) but medium is lost in the checkout redirect.

---

## Tier Classifications (W37 — held from last full per-page run)

### 🟢 Goldmines (2 pages — protect + amplify)
| URL | Notes |
|---|---|
| /treatments/cbt-therapy | Consistent high-intent treatment page |
| /doctors/* cluster | Doctor profile pages (P2: highest per-page payment attribution) |

### 🟡 Rockets (4 pages — drive traffic)
| URL | Notes |
|---|---|
| /illnesses/anxiety | High intent, needs more traffic |
| /illnesses/depression | High intent |
| /blogs/anxiety-working-professionals | Strong pattern match |
| /blogs/[chatgpt-cited pages] | AI-search cited content gaining direct revenue W37 |

### 🔴 Leaky Buckets (0 this week — UX issues are app-side, not SEO pages)
App pages (consult.cadabams.com) have severe UX friction but these are outside SEO scope.

### ⚫ Dead Weight (3 — de-prioritize)
Low-traffic informational pages not generating intent signals.

---

## Active Flags

🔴 **Journey Task EMERGENCY** (product, not SEO): 645→365→124→30 over 4 weeks. Investigate /journeys/* dead clicks (27 dead W37) and /wellness/* (47 dead). Hypothesis: UX bug causing event mis-fire, not behavioral shift.

🔴 **Dead clicks re-escalating**: 4,635 (+23.2%). Top: consult/home (789), appointments (246), find-therapist (237+121 paginated). ALL on app side. SEO pages clean.

🟡 **Assessment Completed decline**: 1,031 → ~640 → ~490 → 303. 4-week trend. May be related to app UX degradation or journey-task bug affecting assessment flow.
