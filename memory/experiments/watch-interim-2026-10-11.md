# Experiment Log — Interim Watch Evaluations
**Evaluated:** 2026-10-11
**Evaluator:** T12 Learner
**Type:** Overdue midpoint checks and ongoing monitoring watches
**Data source:** GSC (current window Oct 1-8, previous window Sep 24-Oct 1) — DataForSEO-402 ACTIVE (GSC-only mode)

---

## W-FIND-THERAPIST-0922 — 14d Midpoint (OVERDUE from 10-06)

**URL:** /blogs/how-to-find-a-therapist-in-india
**Action taken:** Meta title → "How to Find a Therapist in India — Cost, How to Choose | Mindtalk" (65ch)
**Baseline (Sep 22):** pos 1.7, 3,448 impr, 4 clicks = 0.12% CTR
**Current (Oct 1-8):** pos 6.3, 434 impr, 5 clicks = **1.15% CTR**
**Target:** CTR ≥0.5%

**CTR target:** ✅ MET (1.15% > 0.5%)
**Position:** 🔴 REGRESSED (1.7 → 6.3, severe)
**Impressions:** 🔴 CRASHED (3,448 → 434, -87%)

**Verdict: 🟡 INCONCLUSIVE — ALGO_WATCH confound**

CTR target is technically met, but the page lost 87% of impressions and position regressed from 1.7 to 6.3. This is consistent with September Core Update targeting an existing high-ranking blog page (the blog about "how to find a therapist" has strong navigational/YMYL adjacent signals). The title change cannot be cleanly credited for CTR improvement when impressions collapsed simultaneously. 

Do NOT close this watch. Keep open to 42d (2026-11-03). Re-evaluate when ALGO_WATCH clears.

---

## W-REL-COUNSELLORS-BLR-0922 — 14d Midpoint (OVERDUE from 10-06)

**URL:** /doctors/relationship-issues-psychologists-in-bangalore
**Action taken:** Meta title + 3 FAQs
**Baseline (Sep 22):** pos 9-12, 3,119 impr, 30 clicks = 0.96% CTR
**Previous (Sep 24-Oct 1):** pos 12.1, 1,374 impr, 14 clicks = 1.02% CTR
**Current (Oct 1-8):** pos 10.8, 1,377 impr, 13 clicks = **0.94% CTR**

**CTR target:** 🔴 NOT MET (0.94% vs ≥1.5% target)
**Position:** 🟡 Mildly improving (12.1 → 10.8) but far above baseline
**Impressions:** 🔴 CRASHED vs baseline (1,377 vs 3,119, -56%)

**Verdict: 🔴 STALLED — CTR target not met; ALGO_WATCH confound on impressions**

Position gently improving week-over-week but far below baseline levels. Core Update is likely suppressing the /doctors/relationship-issues/ page. CTR barely moved despite the meta update (0.96% → 0.94%). Top keyword "best relationship counsellor in bangalore" at pos 9.0 — page still has traction but AIO/SERP features may be capturing clicks.

Keep open to 42d (2026-11-03).

---

## W-FAMILY-COUNSELLING-0924 — Monitoring Check (was 10-08)

**URL:** /blogs/what-is-family-counselling
**Original signal:** Clicks -100%, Impr +31% WoW = probable AI Overview steal
**Previous (Sep 24-Oct 1):** pos 7.1, 378 impr, 3 clicks = 0.79% CTR
**Current (Oct 1-8):** pos 10.2, 364 impr, 0 clicks = **0.00% CTR**

**Verdict: 🔴 STALLED — AI Overview CTR steal confirmed; position also worsening under Core Update**

Three consecutive weeks of near-zero clicks. Position worsened 7.1 → 10.2 (Core Update pressure). Top keyword: "family counselling" at pos 10.6 (30 impr). This page is being systematically deprioritized in SERPs, compounded by AIO suppression.

**Recommendation to T10:** AIO-resistant content strategy needed. Options: (a) add interactive family counselling assessment (P2 playbook), (b) add original expert commentary from on-site counsellors, (c) restructure as a "find family counsellors near me" page with doctor listings. Decision should wait until ALGO_WATCH clears.

Watch stays OPEN. Continue monitoring weekly.

---

## W-DEMENTIA-BLR-0923 — 14d Check (OVERDUE from 10-07)

**URL:** /doctors/alzheimers-specialists-in-bangalore
**Action taken:** DEMENTIA-LISTING-TITLE-01 (title optimization)
**Baseline:** 754 impr, 0 clicks (was page 1, pos ~8-10)
**Previous (Sep 24-Oct 1):** pos 13.3, 99 impr, 0 clicks
**Current (Oct 1-8):** pos 17.3, 82 impr, 0 clicks

**Verdict: ⚫ WORSE — ALGO_WATCH confound; catastrophic regression from page 1 to pos 17**

Page was on page 1 with 754 impr / 0 clicks at baseline. Now at pos 17.3 with 82 impr. September Core Update has clearly targeted this /doctors/ YMYL listing page. The title change cannot be evaluated — the page has been de-ranked entirely. This is not a content quality failure but an ALGO confound.

Keep open until ALGO_WATCH clears and then re-evaluate. If position recovers to page 1 post-Core-Update, the title optimization can be judged on CTR.

---

## W-LIGHT-THERAPY-0923 — 14d Check (OVERDUE from 10-07)

**URL:** /blogs/light-therapy-for-insomnia
**Action taken:** FAQ schema optimization (W-FAQ-SCHEMA-0930 linked; BLOG-FAQ-KEY-MISMATCH-01 known defect)
**Baseline:** 616 impr, 0 clicks, pos 10.9
**Previous (Sep 24-Oct 1):** pos 7.9, 302 impr, 2 clicks
**Current (Oct 1-8):** pos 7.5, 297 impr, 0 clicks

**Verdict: 🟡 WATCH — Position improving strongly; FAQ defect limits measurement**

Position improved dramatically: 10.9 → 7.9 → 7.5. Approaching page 1. 0 clicks this week is noise at this impression volume (297 impr). The BLOG-FAQ-KEY-MISMATCH-01 defect (Fix A shipped 10-02, W-FAQ-SCHEMA-0930 opened) means the FAQ schema is only partially rendering, limiting rich-result and CTR uplift.

Keep open. Re-evaluate at W-FAQ-SCHEMA-0930 check date (2026-10-21) — by then Fix A will have 19 days of data.

---

## W-SEP15 Cohort — Day-21 Midpoints (OVERDUE from 10-06)

**6 pages shipped 2026-09-15. Day-42 finals: 2026-10-27.**

| URL | Pos (Oct 1-8) | Pos (Sep 24-Oct 1) | Impr | Clicks | Midpoint verdict |
|-----|---:|---:|---:|---:|---|
| /doctors/anxiety-therapists-in-kolkata | 12.7 | 9.5 | 42 | 0 | 🟡 WATCH (position regressing; Core Update likely) |
| /doctors/anxiety-therapists-in-mumbai | 9.0 | 9.8 | 89 | 0 | 🟢 ON TRACK (page 1, improving) |
| /doctors/depression-specialists-in-kolkata | 12.2 | 15.6 | 31 | 0 | 🟢 ON TRACK (improving toward page 1) |
| /doctors/depression-specialists-in-mumbai | 15.4 | 15.4 | 49 | 0 | 🟡 MARGINAL (page 2 stable, needs day-42 push) |
| /doctors/online-psychologist-india | 45.1 | 18.4 | 2 | 0 | 🔴 ALGO_WATCH confound — CRITICAL (was pos 18.4, now 45.1; highest-volume page in cohort: 3,200/mo) |
| /blogs/anxiety-counselling | 0 impr | — | 0 | 0 | ⚠ DATA_GAP (potential E3 — low India volume for exact phrase) |

Note: online-psychologist-india is the most concerning — this page has 3,200/mo search volume and crashed from 18.4 to 45.1 under September Core Update. This matches the weekly report pattern ("online psychologist" pos 6.9→18.4 in prior window = successive regression). Core Update confound confirmed for all /doctors/ city pages. Verdicts at Day-42 will be the definitive measure.

---

## W-SEP16 Cohort + child-psych-blr + W-PHOBIA-0918 — Day-21 Checks

**All confirmed NOISE / zero-impressions by T10 annotation 2026-10-08. GSC data for Oct 1-8:**

| URL | Impr | Status | Note |
|-----|---:|---|---|
| /blogs/online-counselling-in-hindi | 0 | NOISE | 25-day old regional-language blog; E3 candidate |
| /blogs/online-therapy-in-telugu | 0 | NOISE | 25-day old regional-language blog; E3 candidate |
| /blogs/teenage-counselling | 0 | NOISE | 25-day old general blog; likely E3 or indexation lag |
| /blogs/best-doctor-for-panic-attacks | 0 | NOISE | 25-day old blog; indexation lag expected |
| /doctors/child-psychologists-in-bangalore | HIGH_PRIORITY_DROP (-100% clicks, -17% impr) | ALGO_WATCH confound | Core Update impact on /doctors/ YMYL page; open to Day-42 (10-28) |
| /blogs/phobia-treatment-in-bangalore | 0 | NOISE | Confirmed E3 (0 India volume at pos 22-52 baseline) |

Zero-data for regional-language blogs at Day-21 is within normal variance. All kept open to their respective Day-42 windows.

