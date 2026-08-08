# UX Friction Pages — Updated 2026-08-05 (W32)

**Written by:** T19 Conversion Intelligence. **Action required from:** Dev/App team (NOT T18).
**Source:** Mixpanel $mp_rage_click + $mp_dead_click, consult.cadabams.com, Jul 29–Aug 4.

---

## 🚨 W32 CRITICAL ESCALATIONS — TWO NEW PAGES

### Severity 1: CRITICAL (requires immediate dev review)

| URL | Rage | Dead | Total | WoW | Action |
|---|---:|---:|---:|---|---|
| consult.cadabams.com/consult/appointments | 52 | 762 | 814 | Dead: 160→762 (+376%) 🚨 | Was IMPROVING in W31, now exploded. Something broke this week. |
| consult.cadabams.com/assessments/* | 78 | 725 | 803 | Dead: ~52→725 (+1,294%) 🚨 | New CRITICAL. Assessment interactive elements broken. |
| consult.cadabams.com/consult/find-therapist | 59 | 570 | 629 | Dead: 372→570 (+53%) | PERSISTENT 5 WEEKS. Still not fixed. |
| consult.cadabams.com/home | 16 | 564 | 580 | Dead: 673→564 (-16%) | Slightly improving but still critical. |

### Severity 2: MEDIUM-HIGH (persistent but not escalating)

| URL | Rage | Dead | Total | WoW | Action |
|---|---:|---:|---:|---|---|
| consult.cadabams.com/prescriptions | 54 | 338 | 392 | Total: 1,014→392 (-61%) ✅ | IMPROVING. Was W31 #1 critical — recovering. |
| consult.cadabams.com/consult/checkout | 3 | 67 | 70 | 73→70 (-4%) | Flat. Persistent low-level friction. |

---

## Weekly trend tracking

| Week | /appointments Dead | /assessments Dead | /find-therapist Dead | /home Dead | /prescriptions Total |
|---|---:|---:|---:|---:|---:|
| W26 | ~50 est | ~20 est | ~200 est | ~400 est | N/A |
| W27 | ~100 est | ~30 est | ~293 | ~500 est | N/A |
| W28 | ~237 | ~52 | 319 | ~500 est | N/A |
| W31 | 160 ✅ | ~52 | 372 | 673 | 1,014 🔴 |
| W32 | 762 🔴🔴 | 725 🔴🔴 | 570 🔴 | 564 🟡 | 392 🟡 |

---

## Escalation note to app team (W32)

**IMMEDIATE**: /consult/appointments and /assessments/* both spiked catastrophically this week after /appointments was showing improvement. This pattern (simultaneous spike in 2+ pages) strongly suggests a **deploy regression** rather than organic growth in UX problems. Check:
- What deployed to consult.cadabams.com between Jul 28 and Aug 4
- Interactive elements: buttons, sliders, input fields, navigation
- /appointments: calendar component, appointment card click targets
- /assessments: question answer buttons, progress indicators, submit buttons
