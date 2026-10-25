# Experiment Log: W-PUNJABI-DELHI-THIN-0922
**Closed:** 2026-10-25 (retroactive — check date was 2026-10-22)  
**Evaluated by:** T12 (LEARNER)  
**Verdict:** 🔴 STALLED → ARCHIVE PAGE

---

## Hypothesis
Delhi Punjabi-speaking doctors page published with a thin roster (1 profile). Watch monitored whether the page generates any organic demand despite thin content. If 0 impressions at Day-30+ and roster still holds 1 profile, archive the page.

---

## Baseline
New content, no prior data. `baseline_type: NEW_CONTENT_NO_PRIOR`

---

## Check Window: Oct 15–22, 2026 (Day ~33 from ship date ~Sep 20)
| Metric | Current (Oct 15–22) | Prior (Oct 8–15) |
|---|---|---|
| Impressions | 0 | 0 |
| Clicks | 0 | 0 |
| Position | — | — |

**Both windows: 0 impressions, 0 clicks.** Not a GSC pull bug — same pull session returned non-zero for yoga-for-anxiety (1,531 impr) and anxiety-therapists-in-kolkata (140 impr).

---

## Watch Condition Met
Watch spec verbatim: *"if impressions ~0 AND roster still has one Punjabi profile, archive the page"*
- Impressions: 0 ✅ (condition met)
- Roster: 1 Punjabi profile (verified from tracking-db context) ✅ (condition met)
- Day: ~33 (well past reasonable indexation lag) ✅

---

## Verdict
🔴 STALLED — No organic signal at Day-33. Watch conditions for archive triggered.

**Action required (T10/Strategist):**
- Archive `/doctors/punjabi-speaking-doctors-in-delhi`
- Do NOT build a replacement page unless roster reaches ≥3 Punjabi-speaking profiles in Delhi

---

## Pattern Signal
Thin location pages (1 profile) without sufficient keyword demand generate 0 impressions even at Day-33. This confirms the existing thin-page ANTI-PATTERN. Roster threshold matters more than page quality.

---

## Status
CLOSED. Archive action pending T10 approval.
