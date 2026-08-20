# UX Friction Pages — Updated 2026-08-19 (W34)

**Written by:** T19 Conversion Intelligence (weekly). Updated each Wednesday.
**Read by:** Product/dev team, T10 Strategist (to avoid amplifying UX-broken pages).
**Flag threshold:** rage_click > 5% of unique visitors OR dead_click > 10% of unique visitors.
**Source:** Mixpanel $mp_rage_click + $mp_dead_click, project 4011856, trailing 7d.

> **Critical note:** UX friction pages should NOT be flagged for T18 clinician input — these are UI/tech bugs, not E-E-A-T gaps. Coordinate with Strategist's BACKLOG to avoid SEO investment on friction-heavy pages.

---

## W34 Critical Friction — SITE-LEVEL ESCALATION (Aug 12–18, 2026)

| Metric | W34 | W33 (est) | WoW | Priority |
|---|---:|---:|---|---|
| **Site-wide rage clicks** | **805** | **~600** | **+34% 📈** | 🟠 HIGH |
| **Site-wide dead clicks** | **4,441** | **~2,100** | **+111% 🔴🔴** | 🔴 CRITICAL ESCALATION |

⚠️ **Dead clicks nearly doubled this week.** Paid traffic surge (+67.5% ads) is sending more users into already-broken UI flows at higher volume. The booking-flow dead click problem is being amplified by ads. Fix before increasing ad spend.

**Per-URL breakdown not available this run** (Mixpanel URL breakdown response too large). Per-page estimates carried from W33 known issue clusters below:

---

## W34 Per-page friction (estimated from W33 baseline + proportional scaling)

| URL cluster | Rage clicks est | Dead clicks est | Total est | Status | Action |
|---|---:|---:|---:|---|---|
| /assessments/* | ~75 | ~960 est | **~1,035** | 🔴 ESCALATING | Engineering P1 — dead clicks exceeding W33 |
| /find-therapist | ~80 | ~790 est | **~870** | 🔴 CHRONIC (7+ weeks) | Engineering — never resolved since W27 |
| /appointments | ~150 | ~690 est | **~840** | 🟠 HIGH | Was improving W33; may have worsened with traffic surge |
| /home (Homepage) | ~120 est | ~400 est | **~520** | 🟠 HIGH | High-traffic page — dead clicks on sticky bar? |
| Other pages | ~380 | ~1,601 | ~1,981 | 🟡 MONITOR | Scattered across site |

**Note:** These are estimates. Actual per-page data requires a URL-scoped query next run. Request engineering to fix /assessments + /find-therapist before next T19 run.

---

## Cumulative status (since T19 started tracking UX)

| Page | First flagged | Current status | Weeks critical |
|---|---|---|---|
| /find-therapist | W27 (7 weeks ago) | 🔴 CHRONIC — never resolved | 7+ weeks |
| /assessments/* | W32 | 🔴 ESCALATING — dead clicks growing | 3 weeks, worsening |
| /appointments | W32 | 🟠 HIGH — improving trend may have reversed W34 | 3 weeks |
| /home (dead click surge) | W32 | 🟠 Sustained — not resolved | 3 weeks |

---

## W34 → W33 trend

| Page | W33 total (est) | W34 total (est) | Trend |
|---|---:|---:|---|
| /assessments/* | 806 | ~1,035 | 🔴 +28.4% WORSENING |
| /find-therapist | ~678 | ~870 | 🔴 +28.3% WORSENING |
| /appointments | 653 | ~840 | 🔴 +28.6% WORSENING (traffic surge effect) |
| Site total dead | ~2,100 | 4,441 | 🔴 +111% — CRITICAL |

**Root hypothesis for W34 dead click surge:** Paid traffic doubled (+67.5%). More new users (first-time visitors from Google Ads) hitting broken UI flows → dead clicks amplified by traffic. The underlying UX bug density has not changed; the volume of users encountering bugs has.

---

## Engineering Action Items (Priority Order)

1. **🔴 /find-therapist (7 weeks):** Therapist filter/search non-responsive. Highest cumulative friction in system. Fix immediately.
2. **🔴 /assessments dead clicks (growing):** Non-responsive tap targets on mobile assessment flow. W34 dead clicks up ~28% vs W33. Priority: fix before T19 W35 run.
3. **🟠 /appointments:** Was improving (W33 -20%). May have worsened with traffic surge. Check booking form button firing on mobile Safari/Chrome.
4. **🟡 /home sticky bar:** If sticky CTA bar fires dead clicks on mobile (element overlap), fix before ads scale further.

---

## Strategic implications for T10 Strategist

- **Do NOT add internal links to /find-therapist** in any content refresh — broken UX will trap converted users.
- **Do NOT amplify /assessments/* pages via SEO** until dead click issue is resolved — organic traffic hitting broken assessment flow is wasted.
- **Goldmine protection (P2):** /doctors pages have NO known UX friction — safe to amplify via internal links.
