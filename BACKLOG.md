# BACKLOG — Strategist action queue

**Updated:** 2026-08-31 — T10 Strategist 8 PM IST, then **T20 Auto-Remediation 9 PM IST (B1, B2, B4 CLOSED against live ground truth; B3 premise corrected)**
**ALGO_WATCH:** ACTIVE — settle check 2026-09-10 (re-anchored 2026-08-28)

| ID | Action type | Target | Why | Impact estimate | Confidence | Risk | When ready |
|---|---|---|---|---|---|---|---|
| ~~B1~~ | ~~flag_for_human~~ | ✅ **CLOSED 2026-08-31 by T20 — RESOLVED, NOT A DEV TASK.** All 8 pages are LIVE 200 on www.mindtalk.in with real unique content and each appears once in sitemap.xml (902 locs, was 842). Do **not** send this to dev. | The "7 blogs 404 / Vercel webhook / unpushed commit" diagnosis was wrong on every count. MDX reached origin/main in `93769ed` (08-26) and `9d4a4fd` (08-28); production could not serve it until a build fix landed this morning. The 404s were a **build failure**, not a deploy failure. Yesterday's "nothing reached origin" reading was an artifact of a corrupt local checkout (142 behind) plus status checks against the apex host, which 307s *everything*. | — | — | — | **CLOSED** |
| ~~B2~~ | ~~investigate_regression~~ | ✅ **CLOSED 2026-08-31 by T20 — FAILS AP8.** Fresh GSC pull today on /doctors/therapists-in-bangalore: **signal = NOISE**. clicks 8→8 (0.0%), impressions 1,185→1,235 (**+4.2%**), avg position 17.8→18.0 (−0.2). | The page-level premise is not supported. The head query carrying ~85% of the page (`therapist near me`, 985→1,044 impr) is flat at 13.5→13.7. The two cited movers are noise: `bangalore therapist` has 4 impressions in *both* windows at 0 clicks. Caveat: measured with the known-defective `get_comparison_windows()` (see GSC-MEASUREMENT-INTEGRITY-01) — but a 0% click delta on +4% impressions is nowhere near flip-able by a 1-day window overlap. | — | — | — | **CLOSED** |
| B3 | draft_sprint_prompt | ⚠️ **PREMISE CORRECTED — RE-BASE BEFORE DRAFTING.** /doctors/ listing pages thin-content sprint | **The "406 words" figure measures the MDX source, not the page.** T20 measured the *rendered* body today: psychologists-in-mysore **~989 words**; therapists-in-delhi ~1,406; counsellors-in-pune ~1,426; psychiatrists-in-chennai ~1,219; urdu-speaking-doctors-in-bangalore ~867. None is thin. The "thin content + Spam Update = confirmed mechanism" confidence rating is **not supported by rendered-page evidence** and the sprint should not be drafted on it. Re-base on a real cause or drop. | unknown — prior estimate rested on the corrected premise | **L** (was H) | L | RE-BASE — do not draft on the 406-word figure |
| ~~B4~~ | ~~flag_for_human~~ | ✅ **FIXED 2026-08-31 by T20 (both halves).** (1) `tracking-db.json` → primary_keyword `"hyperactive vs inattentive adhd"` set from GSC ground truth (top-impression query, ties slug + live `<title>`). (2) **`keyword-map.json` → entry added.** | Half-fixing this would have been invisible: `rank-pull.py` reads **keyword-map.json**, not tracking-db, and the URL was absent there — the Day-42 pull on 09-04 would have printed "Checking 0 keywords" with tracking-db looking correct. Functionally re-tested: `--keyword 'hyperactive vs inattentive adhd'` now matches 1 target. 8 more live-but-unmapped URLs were added in the same pass. | P12 data point preserved | H | L | **DONE** |
| B5 | flag_for_human | ALGO_WATCH pipeline unlock — 6 confirmed drops (chronic-stress CRITICAL, drug-addiction CRITICAL, ACT CRITICAL, CBT MAJOR, conduct-disorder MAJOR, psychologists-in-mysore MODERATE) + CHATGPT-AEO-SPRINT-REVIEW-01 + PTSD-CLUSTER-DROP-01 all held to 09-10 | Settle check 09-10; need Kushal priority order when ALGO_WATCH clears: (1) doctor listing depth sprint, (2) chronic-stress refresh, (3) drug-addiction, (4) ACT/CBT | +100-200 clicks/wk pipeline unlock across 6 CRITICAL/MAJOR drops | H | L | 09-10 settle check |

---

## Completed / Closed

- THERAPIST-NEAR-ME-CRITICAL-02 — 2026-08-17 (flag_for_human, T2 identification)
- CLINICAL-FAQ-SIGN-OFF-01 — 2026-08-17 (164 Q&As staged)
- SCHEMA-MEDICAL-TYPES-01 — CONFIRMED RESOLVED 2026-08-17 (PR #23 FAQPage + MedicalWebPage)
- T5-REFILL — multiple carries (brief queue now 131 BRIEF_CREATED — adequate)
- PSYCHOLOGISTS-BANGALORE-REFRESH-01 — carried through, on ALGO_WATCH hold 09-10
- COUNSELLORS-BANGALORE-THIN-01 — on ALGO_WATCH hold 09-10
- DELHI-NCT-T5-BRIEF-URGENT-01 — T5 priority (brief queue has Delhi NCT entries)
- ACES-TEST-DROP-01 — investigation completed (assessment cluster Day-42 batch 08-21)
- DEAD-CLICKS-W34-CRITICAL-01 — flagged to dev (doctor_card attribution bleed)
- CHATGPT-AEO-FAQ-EXPANSION-01 — HELD to 09-10 (ALGO_WATCH)
- PTSD-CLUSTER-DROP-01 — HELD to 09-10 (ALGO_WATCH)
- ONLINE-THERAPY-W18-DROP-HIGH-01 — under W18 extended obs (09-21)
- BIOFEEDBACK-W20-REFRESH-01 — eligible post ALGO_WATCH clear (09-10)

---
## T10 Strategist Stamp — 2026-09-01

**Run time:** 2026-09-01 20:00 IST
**Site posture:** CONSERVATIVE — ALGO_WATCH ACTIVE (settle check 2026-09-10; Core Update Aug 22–Sep 7 confirmed)
**T9 pipeline:** FLOWING — 1 blog today (psychiatrist-vs-psychologist), 8 live yesterday (08-31 cohort). Week cap 1/20.
**flagged-drops.json:** EMPTY (0 confirmed drops today — all 3 flags resolved as NOISE/IMPROVING/AP7)

**B3 → CLOSED:** Doctor listing sprint premise was wrong — rendered pages are 989–1,406 words (not thin). Spam Update may have hit /doctors/psychologists-in-mysore for other reasons (algo confound during ALGO_WATCH). Investigation re-queued as B8 post-09-10 settle check.

**Updated pending BACKLOG:**

| ID | Action type | Target | Why | Impact estimate | Confidence | Risk | When ready |
|---|---|---|---|---|---|---|---|
| B5 | flag_for_human | ALGO_WATCH pipeline unlock — priority sequence for 09-10 | 6 confirmed drops (chronic-stress CRITICAL, drug-addiction CRITICAL, ACT CRITICAL, CBT MAJOR, conduct-disorder MAJOR, psychologists-in-mysore MODERATE) + CHATGPT-AEO-SPRINT + PTSD-CLUSTER all held to 09-10. Priority order: (1) doctor listing depth / E-E-A-T, (2) chronic-stress, (3) drug-addiction, (4) ACT/CBT | +100–200 clicks/wk | H | L | 2026-09-10 settle check |
| ~~B6~~ | ~~flag_for_human~~ | ✅ **DONE 2026-09-02 by T11.** Slack posted (ts: 1788347291.686409). Kushal must fix Chrome session (Option A) or authorize API-based AI querying (Option B). Next T17 run 2026-09-04 will stall again without action. | — | — | — | **COMPLETE** |
| B7 | ship_REFRESH_brief | REVIEWER-NEVER-ASSIGNED-01 — 52 live blogs missing reviewer field (5 shipped 2026-09-02, 47 remaining) | Core Update active (Aug 22–Sep 7) targets E-E-A-T signals. Staged batch 1 (5 blogs, reviewer=sucheta-saha) committed `17e974a2e9`, pending HTTP verify. Remaining 47 to ship post-ALGO_WATCH settle 09-10 OR in next eligible T11 run per AP1 7-day stability wait. | M (ranking protection during Core Update) | H | L | Next batch after 09-09 (7-day stability check) |
| B8 | flag_for_human | Position slide investigation — /doctors/ + service cluster | Avg position 9.9 (Jul 4) → 14.2 (Aug 28) = −4.3 positions over 8 weeks. Top drops this week: therapist in bangalore (−9.0 pos), counselling psychologist near me (−6.5), talk therapy (−6.3). Likely causes: (1) Core Update E-E-A-T targeting on service pages, (2) Spam Update thin-listing risk, (3) Tier C drag from life-coach cluster. Cannot investigate cleanly during ALGO_WATCH. Queue: T2 identify all service/doctor URLs dropping ≥5 pos → investigate_regression for each post-09-10. | +200–400 clicks/wk (Tier A service queries) | M (Core Update confound) | L | 2026-09-10 after settle check |

**Step 10 — Meta-Learner proposals:** 3 proposals in proposed-changes/ (ap12-url-locked-violation, t12-gsc-zero-data-guard, t14-cwv-multisample-gate) — all Apply on: 2026-09-06T20:00:00+05:30 (FUTURE — 5 days). **NO-OP today.** No stale proposals (none overdue >14 days). Apply pass runs 2026-09-06.


## T14 Tech Health Stamp — 2026-09-02

**Score: 82/100** (Δ +6 vs last week 76/100) — Baseline run 11.

**Open tech-health flags (T14 only, max 3/week):**

| ID | Type | Target | Detail | Priority |
|---|---|---|---|---|
| CWV-REGRESSION-06 | flag_for_human | /assessments + /journeys lab LCP | Lab LCP: assessments 1.8s→9.9s (+449%); journeys 2.4s→10.1s (+322%). CrUX p75 = 1.52s (fast) on both — real users unaffected. Same feature-hub lazy-load pattern as 07-15/07-22/08-19 regressions. 5th recurrence on assessments. Dev needs permanent fix: SSR above-fold hero content OR eager-load LCP element (not lazy). | HIGH — pattern recurring |

**Healthy axes:** Sitemap/Robots ✅, Internal Links ✅ (0 broken/15 sampled), HTTPS/Canonical ✅

**Ongoing open (pre-existing):** SCHEMA-MEDICALWEBPAGE-RESIDUAL-01 (MedicalWebPage absent on illness+treatment templates — wk 4 open), CHROME-STALL-2026-08-28 (Chrome extension stall wk 6 — blocking AI OV tracking), GSC OAuth expired (wk 10 — critical blind spot).

Full report: reports/technical-health-2026-09-02.md

---
## T10 Strategist Stamp — 2026-09-02

**Run time:** 2026-09-02 20:00 IST
**Site posture:** CONSERVATIVE — ALGO_WATCH ACTIVE (settle check 2026-09-10). Core Update Aug 22–~Sep 7 active.
**T9 pipeline:** FLOWING — 1 blog today (psychiatrist-vs-psychologist). Week cap 2/20 (includes 2026-09-01).
**Rank signals:** CRITICAL guide-to-easy-anxiety-kids pos 11→100 (genuine, AP8 not triggered). MODERATE psychology-of-love pos 3→7 + social-media-trap pos 6→10.
**Step 10 — Meta-Learner proposals:** 3 proposals (ap12-url-locked-violation, t12-gsc-zero-data-guard, t14-cwv-multisample-gate) — all Apply on 2026-09-06 (FUTURE — 4 days). NO-OP today. No stale proposals.

**Updated pending BACKLOG:**

| ID | Action type | Target | Why | Impact estimate | Confidence | Risk | When ready |
|---|---|---|---|---|---|---|---|
| B5 | flag_for_human | ALGO_WATCH pipeline unlock — priority sequence for 09-10 | 6 confirmed drops (chronic-stress CRITICAL, drug-addiction CRITICAL, ACT CRITICAL, CBT MAJOR, conduct-disorder MAJOR, psychologists-in-mysore MODERATE) + CHATGPT-AEO-SPRINT + PTSD-CLUSTER all held to 09-10. Priority order: (1) doctor listing depth / E-E-A-T, (2) chronic-stress, (3) drug-addiction, (4) ACT/CBT | +100–200 clicks/wk | H | L | 2026-09-10 settle check |
| B7 | ship_REFRESH_brief | REVIEWER-NEVER-ASSIGNED-01 — 47 remaining blogs missing reviewer field | Batch 1 (5 blogs) committed `17e974a2e9` 2026-09-01. Next batch eligible after 2026-09-09 stability check (AP1 7-day rule). Core Update E-E-A-T window makes reviewer assignment high-value. | M (ranking protection during Core Update) | H | L | Next batch after 2026-09-09 |
| B8 | flag_for_human | Position slide investigation — /doctors/ + service cluster post-09-10 | Avg pos 9.9 (Jul 4) → 14.2 (Aug 28) = −4.3 pos over 8 weeks. therapist in bangalore −9.0, counselling psychologist near me −6.5, talk therapy −6.3. Cannot investigate cleanly during ALGO_WATCH. | +200–400 clicks/wk (Tier A service queries) | M | L | 2026-09-10 after settle check |
| B9 | investigate_regression | /blogs/guide-to-easy-anxiety-coping-techniques-for-kids | CRITICAL pos 11→100 (+89). MDX confirmed exists in src/content/blogs/. AP8 did NOT trigger — genuine drop, not data artefact. Core Update confound flag required in investigation. Read-only — safe during ALGO_WATCH. | +15–30 clicks/wk (Tier B parenting) | M (Core Update confound) | L | Immediate — Executor T11 next run |
| B10 | flag_for_human | Chrome stall (T17 6 weeks blind) + GSC OAuth expired (10 weeks) | Chrome stall since 2026-08-28: AI citation sweep missing 200+ data points across 6 Thursdays. GSC OAuth expired 10 weeks: rank-pull.py cannot do fresh GSC cross-checks. Both require Kushal manual action (Option A: restart Chrome/extension OR Option B: authorize API-based citation querying). | Infrastructure — blocks measurement | H | L | Immediate |
