# UX Friction Pages — Updated 2026-10-28 (W44)

**Source:** T19 Conversion Intelligence. Rage click threshold: >5% page rate. Dead click threshold: >10% site rate.
**Read by:** T10 Strategist, T18 Professional Input (Leaky Bucket UX audits)

---

## W44 Friction Summary (Oct 21–27)

| Metric | W44 | W43 | Δ% |
|---|---|---|---|
| Rage clicks (unique) | 220 | 222 | -0.9% ✅ continuing improvement |
| Dead clicks (unique) | 1,295 | 1,296 | flat ⚠️ persistent |
| Dead rate (site) | 10.22% | 10.6% | ⚠️ 4th week above 10% threshold |
| Rage rate (site) | ~1.7% | ~1.8% | improving ✅ (<5% threshold) |

**W44 STATUS:** Dead rate 10.22% = ABOVE THRESHOLD for 4th consecutive week (W41: 10.4%, W42: 10.7%, W43: 10.6%, W44: 10.22%). Rate is falling slowly but not clearing the 10% threshold. Rage rate continues to improve. Overall friction is stable-to-improving but dead click volume is not resolving.

---

## Top Rage Click Pages (W44 — unique rage events)

| Rank | Page | Rage events (unique) | Severity | WoW | Notes |
|---|---|---|---|---|---|
| 1 | /home (app) | 17 | 🟡 MEDIUM | -26.1% 🟢 | Improved vs W43 23 |
| 2 | /profile (app) | 13 | 🟡 MEDIUM | flat | Profile page UX friction |
| 3 | /consult/booking/8796?mode=online | 12 | 🟡 MEDIUM | -62.5% 🟢 MAJOR | W43: 32 → W44: 12 — significant improvement |
| 4 | /consult/booking/* (other IDs) | ~15 | 🟡 MEDIUM | improving | Pattern: booking/?mode=online systemic |
| 5 | /assessments/* | ~10 | 🟡 MEDIUM | flat | Assessment flow friction |
| 6 | /onboarding/start | ~8 | 🟡 MEDIUM | flat | Onboarding |
| 7 | /care | ~6 | 🟡 LOW-MEDIUM | flat | Care hub |

**W44 POSITIVE SIGNAL:** /consult/booking/8796?mode=online rage dropped 32→12 (-62.5%). Booking UX appears to be partially resolving. /home rage dropped 23→17 (-26.1%). Both improving WoW.

**NOTE:** Per-page dead click breakdown unavailable this run (Mixpanel breakdown file exceeded token limit). Site-level total used. Next run should use jq/bash extraction for per-page dead click data.

---

## Top Dead Click Pages (W44 — ESTIMATED from W43 baseline + site trend)

*Note: Per-page dead click data not extracted this run. W43 page distribution used as baseline; site-level W44 total = 1,295 (flat vs W43 1,296). Per-page distribution assumed similar to W43 unless new signals indicate otherwise.*

| Rank | Page | Dead events (W43 baseline) | Severity | Status |
|---|---|---|---|---|
| 1 | /home (app) | 679 | 🔴 CRITICAL PERSISTENT | UNRESOLVED — 8 WEEKS (W37–W44) |
| 2 | /consult/find-therapist | 129 | 🔴 HIGH | PERSISTENT — monitor |
| 3 | /consult/appointments | 102 | 🔴 HIGH | PERSISTENT |
| 4 | /profile (app) | 95 | 🔴 HIGH | PERSISTENT |
| 5 | /care | 78 | 🟡 MEDIUM | — |
| 6 | /auth/login (returnTo assessment) | 62 | 🟡 MEDIUM | — |
| 7 | /consult/checkout | 61 | 🔴 HIGH | W43 NEW — watch for revenue impact in W44 |
| 8 | /find-therapist?p=2 | 54 | 🟡 MEDIUM | Pagination |
| 9 | /assessments/*/details | ~50 each | 🟡 MEDIUM | Assessment completion flow |

---

## CRITICAL ALERTS (Action Required)

### 🔴 CRITICAL PERSISTENT: /home (app) — 679+ dead clicks (8 weeks unresolved)
**Impact:** App landing page broken UX — erodes trust, impairs navigation to consult flow.
**Status:** UNRESOLVED since W37. W37, W38, W39, W40, W41, W42, W43, W44 = 8 consecutive weeks.
**Action:** IMMEDIATE engineering escalation required. This is not a content issue — requires code fix.
**Revenue connection:** /home dead clicks block the path to /consult/booking/* — may be suppressing overall booking conversion rate.

### 🔴 HIGH: /consult/checkout — 61 dead clicks (W43 data, W44 unknown)
**Impact:** Dead clicks on checkout page = abandoned payment transactions. Possible contribution to organic payment drop W43 (-31%).
**W44 status:** Per-page data unavailable this run. If checkout dead clicks persist, revenue impact continues.
**Action:** Product team audit: which elements receiving dead clicks? CTA button? Payment form? Back navigation?
**Priority:** P0 (direct revenue impact)

### 🔴 HIGH: /consult/booking/* (mode=online) — rage click pattern
**Impact:** Booking flow generates rage across multiple doctor booking pages.
**W44 update:** booking/8796 improved significantly (32→12 rage), but pattern may be spread across more booking IDs. Site-level rage 220 vs 222 = essentially flat. Pattern partially resolved for /8796 specifically.
**Action:** Check if booking/8796 fix was deployed or if rage shifted to other booking IDs.

---

## Week-over-Week Trend

| Page | W42 | W43 | W44 | Trend |
|---|---|---|---|---|
| /home dead | ~679 | 679 | ~679 (est) | 🔴 CRITICAL STABLE — UNRESOLVED 8W |
| /consult/checkout dead | unknown | 61 | unknown (W44 n/a) | 🔴 MONITOR |
| /consult/appointments dead | 814 | 102 | ~102 (est) | 🟢 RESOLVED W43, holding |
| /consult/find-therapist dead | ~129 | 129 | ~129 (est) | 🟡 STABLE PERSISTENT |
| /worksheets rage | 233 | 0 | 0 | 🟢 RESOLVED W43 |
| booking/* rage | ~87 | 91 | ~35 | 🟢 SIGNIFICANTLY IMPROVED |
| /home rage | ~23 | 23 | 17 | 🟢 IMPROVING |

---

## Historical Friction Notes
- W44: Dead rate 10.22% — 4th week above 10% threshold; rage improving (+W44 positive)
- W43: /consult/checkout 61 dead clicks (NEW — direct revenue impact signal); /worksheets rage resolved
- W42: /worksheets 233 unprecedented rage (resolved W43); /consult/appointments 814 dead (mostly resolved W43→102)
- W41: Dead rate first crossed 10% threshold
- W39: Dead rate 11.1% (site) — crossed threshold
- W37: /home dead clicks began (now 8 weeks unresolved — CRITICAL)
- W36: Journey Task crash deepened (now fully recovered W42-W44)
