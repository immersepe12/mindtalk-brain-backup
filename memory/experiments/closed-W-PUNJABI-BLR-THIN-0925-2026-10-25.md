# Experiment Log: W-PUNJABI-BLR-THIN-0925
**Closed:** 2026-10-25  
**Evaluated by:** T12 (LEARNER)  
**Verdict:** 🔴 STALLED → ARCHIVE BOTH PAGES + CANCEL MUMBAI BRIEF

---

## Hypothesis
Bangalore Punjabi-speaking doctors page published with a thin roster. Watch monitored for organic signal at Day-30. If 0 impressions AND roster holds 1 Punjabi profile, archive both this page AND the Delhi page (W-PUNJABI-DELHI-THIN-0922) AND cancel the Mumbai brief.

---

## Baseline
New content, no prior data. `baseline_type: NEW_CONTENT_NO_PRIOR`

---

## Check Window: Oct 15–22, 2026 (Day ~30 from ship date ~Sep 25)
| Metric | Current (Oct 15–22) | Prior (Oct 8–15) |
|---|---|---|
| Impressions | 0 | 0 |
| Clicks | 0 | 0 |
| Position | — | — |

Both windows: 0 impressions, 0 clicks. Not a GSC pull bug (yoga: 1,531 impr from same pull session).

---

## Watch Condition Met
Watch spec verbatim: *"if both show ~0 impressions and roster holds one Punjabi profile, archive BOTH pages and the Mumbai brief"*
- Bangalore impressions: 0 ✅
- Delhi (companion watch W-PUNJABI-DELHI-THIN-0922): 0 ✅ (also closed 🔴 STALLED today)
- Roster: 1 Punjabi profile each ✅
- Both conditions met for trigger

---

## Verdict
🔴 STALLED — Zero organic signal at Day-30. Both Punjabi thin-page watches close 🔴.

**Action required (T10/Strategist):**
1. Archive `/doctors/punjabi-speaking-doctors-in-bangalore`
2. Archive `/doctors/punjabi-speaking-doctors-in-delhi` (companion, also closed today)
3. Cancel the Mumbai Punjabi-speaking doctors brief (do not build a Mumbai page)
4. Reassess entire Punjabi vertical — requires ≥3 profiles per city minimum before building any city page

---

## Pattern Signal (companion to W-PUNJABI-DELHI-THIN-0922)
Two thin Punjabi location pages = 2 consecutive 🔴 failures. This is a replication of the thin-page pattern. A 3rd failure would trigger AP write. For now: thin location pages with 1 profile + low keyword demand generate 0 impressions even at Day-30+. Roster depth is the prerequisite, not page quality.

---

## Status
CLOSED. T10 must action all three items above.
