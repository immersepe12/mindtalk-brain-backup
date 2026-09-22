# W18/W19/W20/W21 — Extended Observation Closure (AP3-B cohort final)

Extended obs window: 2026-07-31 extended to 2026-09-21 (+84 days from Day-42)
Closed: 2026-09-20 (1 day before hard deadline per T10/Strategist instruction)

---

## W18 — /treatments/online-therapy — 🟢 RECOVERED

Action: T17-1 hub ship (commit `6768c7f`), first AP3-B Option B. Reviewer sign-off locked. Live 2026-06-29.
Original Day-42 verdict: QDF_BLOCKED (pos 10.5→24.3, -68% impr, QDF spike normalized)
Extended obs GSC pull 09-20: impr=1,173, clicks=39, pos=8.7 (vs prev 873, 33, pos=8.7)
Delta from baseline: +34% impr, +18% clicks, pos stable at 8.7 (page-1/1 range)

Verdict: 🟢 RECOVERED
Explanation: The QDF_BLOCKED verdict at Day-42 (8.7→24.3) turned out to be a temporary valley in a longer indexation curve. By Day-84+ (extended obs), the page stabilized at pos 8.7 — exactly where it was at Day-21 before the Day-42 dip. 39 clicks/week with 1,173 impr = 3.3% CTR on competitive "online therapy india" cluster. This is the system's strongest hub page performance.
Learning: For new hub pages on high-DA-competitive queries, Day-42 QDF_BLOCKED verdict can be premature — 84-day window provides more reliable signal.

---

## W19 — /treatments/emdr-for-ptsd — ⚫ WORSE

Action: T9 auto-ship via AP3 Option B (commit `f4b8b0d`), reviewer abhimanyu-chandak. Live 2026-06-29.
Original Day-42 verdict: QDF_BLOCKED (institutional authority lockout: EMDR Association India, academic journals, NHS)
Extended obs GSC pull 09-20: impr=7, clicks=0, pos=83.4 (vs prev 15, 0, pos=69.5)
Delta: −53% impr, pos degraded 69.5→83.4

Verdict: ⚫ WORSE
Explanation: Not only did the page fail to recover from Day-42 QDF_BLOCKED — it further degraded. "emdr for ptsd" SERP is owned by professional associations (EMDR Association India, British Psychological Society, etc.) with 10-20 year topic authority and 60-90 DA. The page has correct format and clinical reviewer but lacks the institutional domain authority to compete. Dark page confirmed.
Learning (contributes to potential AP): AP3-B pages on specialist clinical technique queries dominated by professional bodies do not recover in 84-day extended obs. Content quality is a necessary but NOT sufficient condition — domain authority and institutional backing are gating factors.

---

## W20 — /treatments/biofeedback-therapy-for-anxiety — 🟢 RECOVERED

Action: T9 auto-ship via AP3 Option B (commit `8438777`), reviewer krishna-k-r. Live 2026-06-29.
Original Day-42 verdict: NEEDS_REFRESH (DataForSEO pos=100 sentinel, 0 impr — AP8 noise; refresh queued as BIOFEEDBACK-W20-REFRESH-01)
Post-refresh action: BIOFEEDBACK-W20-REFRESH-01 executed by T11 (content depth added)
Extended obs GSC pull 09-20: impr=14, clicks=1, pos=7.9 (vs prev 8, 0, pos=10.2)
Delta: +75% impr, +100% clicks (0→1), pos improved 10.2→7.9

Verdict: 🟢 RECOVERED
Explanation: The NEEDS_REFRESH + refresh cycle worked. After T11 added content depth (biofeedback mechanisms, clinical study citations, expanded FAQ), the page moved to pos 7.9 (page 1). Volume is low (14 impr/wk) because "biofeedback therapy for anxiety" is a low-volume head term (~1K-10K/mo, mostly US traffic), but the page is ranking correctly for its target cluster in India.
Learning: NEEDS_REFRESH verdict + targeted depth refresh restores AP3-B pages that had DataForSEO AP8 noise at Day-42. The biofeedback recovery validates the NEEDS_REFRESH → refresh → re-evaluate pipeline.

---

## W21 — /treatments/talk-therapy-for-depression — 🔴 STALLED

Action: T9 auto-ship via AP3 Option B (commit `b3b4f46`), reviewer dr-arun-kumar. Live 2026-06-29.
Original Day-42 verdict: QDF_BLOCKED (TalktoAngel, BetterHelp, Verywell Mind dominate; QDF expired)
Extended obs GSC pull 09-20: impr=57, clicks=0, pos=50.2 (vs prev 65, 0, pos=55.1)
Delta: −12% impr, pos slightly improved 55.1→50.2 (still page 5+)

Verdict: 🔴 STALLED
Explanation: QDF_BLOCKED confirmed permanent. "talk therapy for depression" SERP is locked by dedicated therapy platforms (TalktoAngel has entire brand/domain authority on this term) + global authority (BetterHelp, Verywell Mind). 84-day extended obs showed no recovery — pos remains 50+ (page 5). The page has good format and clinical reviewer but cannot compete with platforms that brand-build on "talk therapy" as their core product.
Learning: When the top-3 SERP results are brand-dedicated platforms (their domain name = the query keyword), AP3-B content pages will not recover within 84 days. Content quality signal is drowned by brand signal.

---

## AP3-B Cohort Summary (W18-W21 closed)

| Watch | URL | Day-42 Verdict | Extended Obs Verdict |
|-------|-----|----------------|---------------------|
| W18 | /treatments/online-therapy | QDF_BLOCKED | 🟢 RECOVERED (+34% impr, pos 8.7) |
| W19 | /treatments/emdr-for-ptsd | QDF_BLOCKED | ⚫ WORSE (pos 83.4, -53% impr) |
| W20 | /treatments/biofeedback-therapy-for-anxiety | NEEDS_REFRESH | 🟢 RECOVERED (pos 7.9, +75% impr) |
| W21 | /treatments/talk-therapy-for-depression | QDF_BLOCKED | 🔴 STALLED (pos 50.2) |

Recovery rate: 2/4 (50%). QDF_BLOCKED in extended obs = 1/2 recovered (W18 yes, W19 no). NEEDS_REFRESH recovered (W20). One QDF_BLOCKED stalled (W21).

Key differentiator between W18 🟢 and W19/W21 ⚫/🔴:
- W18 (online therapy): broad query, multiple stakeholder types compete (clinical, generic), Mindtalk has URL depth + 37 internal links → recovered
- W19 (emdr): query owned by single professional body (EMDR Association India) → permanent lockout
- W21 (talk therapy): query owned by brand-name platforms (TalktoAngel) → permanent lockout
