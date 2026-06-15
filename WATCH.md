# WATCH — Active Observations

**Owner:** Strategist adds; Learner closes.
**Format:** One row per page/query under observation. Stale entries (>60 days) auto-pruned.

| Watch ID | URL | Query | Type | Opened | Action that triggered watch | Expected outcome | Check on | Status |
|---|---|---|---|---|---|---|---|---|
| W1 | /illnesses/dementia | dementia treatment | YMYL_recovery | 2026-06-09 | Sprint A (commit `270cf0c`) | impressions +15-25% | 2026-06-23 | open |
| W2 | /illnesses/alzheimers | alzheimers treatment | YMYL_recovery | 2026-06-09 | Sprint A | +15-25% | 2026-06-23 | open |
| W3 | /illnesses/posttraumatic-stress-disorder-ptsd | ptsd | YMYL_recovery | 2026-06-09 | Sprint A | +15-25% | 2026-06-23 | open |
| W4 | /illnesses/drug-addiction | drug addiction | YMYL_recovery | 2026-06-09 | Sprint A | +15-25% | 2026-06-23 | open |
| W5 | /treatments/eclectic-therapy | eclectic therapy | YMYL_recovery | 2026-06-09 | Sprint A | +15-25% | 2026-06-23 | open |
| W6 | /treatments/biofeedback-therapy | biofeedback therapy | YMYL_recovery | 2026-06-09 | Sprint A | +15-25% | 2026-06-23 | open |
| W7 | /blogs/understanding-dominant-personality-and-dominating-nature | dominant personality | AI_overview_defense | 2026-06-09 | Sprint B/1 (commit `aa5e3b9`) | impressions 1.3k → 3.5k | 2026-06-23 | open |
| W8 | /blogs/20-quotes-to-inspire-healthy-relationships | relationship quotes | AI_overview_defense | 2026-06-09 | Sprint B/2 (`5dfe080`) | 1.7k → 4k | 2026-06-23 | open |
| W9 | /blogs/emotional-distress-all-you-need-to-know | emotional distress | AI_overview_defense | 2026-06-09 | Sprint B/3 (`c1e0d67`) | 2.2k → 5k | 2026-06-23 | open |
| W10 | top 20 pages from W12 analyst | (multiple) | CTR_metarewrite | 2026-06-09 | Sprint C (`7c3c2c4`) | +2,180 clicks/wk total | 2026-06-23 | open |
| W11 | / (homepage) | mindtalk | conversion_redesign | 2026-06-12 | Homepage app-first (merge `c35193f`) | "Get the App" becomes #1 hero CTA | 2026-06-19 | open |

## Closing rules

- Open watch ≥ check date → Learner runs evaluation
- 🟢 RECOVERED (within target) → log to PRINCIPLES.md, close watch
- 🟡 PARTIAL → extend 14 more days, note in BRAIN.md
- 🔴 FAILED → log to ANTI-PATTERNS.md or add follow-up brief to BACKLOG.md
- ⚫ WORSE → URGENT alert + escalate to manual review
