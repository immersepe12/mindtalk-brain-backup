# UX Friction Pages — Updated 2026-08-12 (W33)

**Written by:** T19 Conversion Intelligence (weekly). Updated each Wednesday.
**Read by:** Product/dev team, T10 Strategist (to avoid amplifying UX-broken pages).
**Flag threshold:** rage_click > 5% of unique visitors OR dead_click > 10% of unique visitors.
**Source:** Mixpanel $mp_rage_click + $mp_dead_click, project 4011856, trailing 7d.

> **Critical note:** UX friction pages should NOT be flagged for T18 clinician input — these are UI/tech bugs, not E-E-A-T gaps. Coordinate with Strategist's BACKLOG to avoid SEO investment on friction-heavy pages.

---

## W33 Critical Friction Pages (Aug 5–11, 2026)

| URL cluster | Rage clicks | Dead clicks | Total | vs W32 | Priority | Likely cause |
|---|---:|---:|---:|---|---|---|
| /assessments/* | 56 | 750 | **806** | +0.4% 🔴 ESCALATING | 🔴 CRITICAL | Dead clicks growing despite rage stable — broken UI element, non-responsive tap targets on mobile assessment flow |
| /find-therapist | 63 | 615 | **678** | stable est | 🔴 CRITICAL (long-standing, 5+ weeks) | Filter/search UI non-responsive; therapist card buttons not firing |
| /appointments | 118 | 535 | **653** | -19.8% 🟡 IMPROVING | 🟠 HIGH (improving) | Appointment management UI partially fixed — rage dropping, dead still high |

---

## W33 vs W32 trend

| Page | W32 total | W33 total | Trend |
|---|---:|---:|---|
| /appointments | 814 | 653 | -19.8% ✅ IMPROVING |
| /assessments/* | 803 | 806 | +0.4% 🔴 STAGNANT/ESCALATING |
| /find-therapist | ~678 | ~678 | flat 🔴 CHRONIC |
| /prescriptions | ~392 (W31) | est ~300 (from combined query) | possibly improving |
| Homepage (/home) | ~580 | not isolated this week | — |

---

## Cumulative status (since T19 started tracking UX)

| Page | First flagged | Status | Weeks critical |
|---|---|---|---|
| /find-therapist | W27 (6+ weeks ago) | 🔴 CHRONIC — never resolved | 6+ weeks |
| /appointments | W32 (NEW escalation) | 🟠 IMPROVING — first improvement W33 | 2 weeks critical |
| /assessments/* | W32 (NEW escalation) | 🔴 ESCALATING — dead clicks not improving | 2 weeks, worsening |
| /prescriptions | W31 | Status unknown this week | 3+ weeks, unclear |

---

## Escalation log

| Date | Page | Event | Action |
|---|---|---|---|
| 2026-07-22 (W31) | /prescriptions | NEW CRITICAL: 1,014 friction events | Flagged to Kushal |
| 2026-08-05 (W32) | /appointments | ESCALATED: 814 friction events (+376% vs W31) | Flagged to eng |
| 2026-08-05 (W32) | /assessments/* | ESCALATED: 803 friction events (+1,440% vs W31) | Flagged to eng |
| 2026-08-12 (W33) | /appointments | IMPROVING: 653 (-19.8%) — fix partially working | Still critical but trend positive |
| 2026-08-12 (W33) | /assessments/* | STAGNANT: 806 (+0.4%) — fix not working on dead clicks | ESCALATE again |

---

## Action required from dev team

1. **PRIORITY 1 — /assessments/* dead clicks (750 W33):** Whatever fix was applied to /appointments has NOT been applied to /assessments. Dead clicks on 750+ events/week means a button, link, or interactive element is visually present but not clickable (likely z-index/overlay issue in assessment flow). Fix urgently.
2. **PRIORITY 2 — /find-therapist (678 W33, 6+ weeks):** Longest-running friction. Filter/search component not responding to taps on mobile. Escalate to mobile team.
3. **WATCH — /appointments (653, improving):** Continue current fix trajectory. Do not regress.
