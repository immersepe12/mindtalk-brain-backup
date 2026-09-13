# BACKLOG — Strategist action queue

**Updated:** 2026-09-13 — T10 Strategist 8 PM IST
**ALGO_WATCH:** ✅ CLEARED 2026-09-10. No September Core Update.
**DataForSEO:** PARTIAL 09-11 — 36/299 KWs (12%); 3 CRITICAL pos→100 drops → VERIFIED NOISE by T20 09-12 (B21 CLOSED). /blogs/ cap resets 09-15.
**Site posture:** GROWTH. Q3 targets exceeded (clicks 3,735 vs 2,800 ✅; CTR 1.0% vs 0.85% ✅; pages ~870 vs 800 ✅). Meta-Learner apply-pass 09-13: t12-stub-pilot-qdf-guard APPLIED ✅; t9-doctors-cluster-cap-separation → NEEDS_HUMAN (B23); t17-tabs-create-fallback → MISMATCH-SKIP (target file wrong in proposal — T13 fix needed).
**Day-42 finals:** 4 URLs due 2026-09-15 (drug-addiction-symptoms, intellectual-disability-symptoms, signs-of-adhd, narrative-therapy) — T12 to evaluate.

| ID | Action type | Target | Why | Impact estimate | Confidence | Risk | When ready |
|---|---|---|---|---|---|---|---|
| B23 | flag_for_human | t9-doctors-cluster-cap-separation — Kushal confirm spec-vs-script cap enforcement | Verifier NEEDS_HUMAN: 14 Tier A /doctors/ briefs blocked for weeks; spec change is a no-op if cap logic lives in scripts/*.py. One confirmation call unblocks them all. | +200–500 clicks/wk Tier A (14 briefs × avg Tier A) | H | L | IMMEDIATE — Kushal decision |
| B24 | schedule_watch_check | Day-42 finals 2026-09-15 — /blogs/drug-addiction-symptoms, /blogs/intellectual-disability-symptoms, /blogs/signs-of-adhd, /treatments/narrative-therapy | 4 Aug-04 cohort pages hit Day-42 in 2 days; T12 must run evaluations | Pipeline maintenance | H | L | 2026-09-15 (T12) |
| B8 | investigate_regression (RE-SCOPED by T20 2026-09-12 — Verifier reversed T20's own false-positive closure) | /doctors/therapists-in-bangalore + /doctors/therapists-in-hyderabad — query "therapist near me" (Tier A, INTENT-PRIORITY §5 pos 8–11 cliff) | **VERIFIED REAL at query level.** GSC page-attributed, query = "therapist near me": wk 07-11→07-18 vs 09-02→09-09 — `/doctors/therapists-in-bangalore` pos **9.3 → 16.2** (856→1,167 impr, 7→4 clicks); `/doctors/therapists-in-hyderabad` pos **10.1 → 49.5** (294→205 impr, crash); `/doctors/therapists` 11.5→12.3 (stable). Property-level pos 11.9 → 27.0 (impr-weighted), 11→7 clicks/wk; 90d query-level pos 27.3 on 18,888 impr / 78 clicks. Part of the property slide is mix dilution (new /doctors/ URLs appearing at pos 130–220: psychologists-in-bangalore, mental-health-professionals-in-bangalore, english-speaking-doctors-in-bangalore — likely the 08-31 de29c86 batch) but the primary page's own 9.3→16.2 slide and the Hyderabad crash are real. Secondary signals also real at query level: "counselling psychologist near me" 1,100 impr / pos 22.5 (90d), "talk therapy" 1,363 / 28.4. T20's earlier 2-window closure compared adjacent 7/8-day windows and missed the 8-week trend — do not repeat. Verify MDX exists before queuing each URL. | +200–400 clicks/wk Tier A | H (query-level + page-attributed) | L | IMMEDIATE — T11 investigate_regression on the 2 URLs; T12 site-level mix watch on the query |
| B12 | draft_sprint_prompt (fire — Kushal) | therapy-near-me hub page | Pos 32→52 (largest single weekly drop Q3). Amaha pos 3. 60.5K/mo Tier A gap. Prompt at `prompts/auto-drafted-sprint-therapy-near-me-hub-2026-09-04.md`. T11 flagged to Kushal 09-11. | +80–150 clicks/wk Tier A | H | L | IMMEDIATE — awaiting Kushal fire |
| B18 | investigate_regression + internal_link | online-psychiatrist hub momentum (pos 20.7→9.6) | Approaching page 1 organically without dedicated hub. W43-1 psychiatrist-online-consultation-india LIVE 08-31 as foundation. Internal link injection from high-traffic illness pages could lock top-5. Verify MDX exists first. | +30–60 clicks/wk Tier A | M | L | IMMEDIATE (MDX confirmed live) |
| B7 | ship_REFRESH_brief | REVIEWER-NEVER-ASSIGNED-01 — Batch 3 (next 10 blogs) | Batch 2 shipped 09-09 (commit 8f7617bb ✅). AP1 7-day rule → batch 3 eligible 2026-09-16. W-B7-REVIEWER-BATCH2 check 09-16. | M (ranking protection + E-E-A-T) | H | L | 2026-09-16 |
| B22 | flag_for_human (T20 2026-09-12, Verifier NEEDS_HUMAN) | /blogs/therapist-for-depression — REVIEWER-SLUG-ORPHAN-02 recurrence | Shipped 09-09 (commit 4c8e02e) with `reviewer: santanu-tripathy` — a 301 orphan (`/doctors/santanu-tripathy` → 301 → /doctors, no -L). Live page emits **no `reviewedBy` node**; byline falls back to generic "Mindtalk Medical Team". Same defect class escalated 08-31 (D1), reproduced 9 days later because the reviewer pool still listed the slug — T20 removed santanu-tripathy + dr-akanksha-bhor from `logs/reviewer-load-state.json` tonight so T9 cannot pick them again. **Pre-written fix (dev/T9 path, T20 may not touch src/**):** in `src/content/blogs/therapist-for-depression.mdx` change `reviewer: santanu-tripathy` → `reviewer: dr-sneha` (MD Psychiatry, live load 3, /doctors/dr-sneha 200) and set `lastReviewed` only when she has actually reviewed. **Kushal decision:** apply now (page is inside its Day-42 window to 2026-10-21 — AP12 perturbation is one frontmatter field) or hold to 10-21. | E-E-A-T on a Tier B booking spoke | H | L | Kushal decision |
| B15 | flag_for_human | STUB-PILOT-CONVERSION-VERDICT-01 — Kushal decision (a)/(b)/(c) | 30+ days pending. Verdict delivered 08-14: 5/7 strong indexation, CTR bottleneck (breathing pos 2.6, 0% CTR), conversion NIL. Recommend (b) 10-item gated pilot. mindtalk-stub-pilot-batch task has no-op'd 6+ Fridays. | Unblocks next inventory-gap pilot | H | L | Immediate — Kushal decision |
---

## Completed / Closed

- ~~B21~~ **CLOSED FALSE POSITIVE 2026-09-12 T20** — GSC page-dimension (non-overlapping windows 08-26..09-01 = 7d vs 09-02..09-09 = 8d; per-day averages in brackets): /illnesses/personality-disorder 169→267 impr [24→33/day, +38%], pos 24.6→15.8 (09-09: 71 impr pos 8.0); /illnesses/postpartum-depression-ppd 59→50 impr [8.4→6.3/day], pos 66→55; /illnesses/stress-disorder 104→99 impr [14.9→12.4/day], pos 29.5→23.8. All three impressing every day through 09-10 — nothing deindexed. The tracked queries "personality/postpartum/stress disorder treatment bangalore" rank pos 7.8 / 11 / 9 via /doctors/*-specialists-in-bangalore (domain-matched — DataForSEO's "not in top 100" is API noise, 14/36 = 39% sentinel rate). AP8 fired correctly. No T2 action needed. Evidence: brain/memory/remediation-log.md 2026-09-12.
- ~~B8 closure~~ **WITHDRAWN 2026-09-12 T20 (Verifier VETO of the closure).** T20 had closed B8 as a false positive on two adjacent 7/8-day page-row windows; the Verifier showed the query-level series (10.9 → 52.0 over 8 weeks) reproduces the alert, and T20's page-attributed re-pull confirmed the primary page slid 9.3 → 16.2 and the Hyderabad page 10.1 → 49.5. **B8 is re-opened above, re-scoped with the evidence.** Lesson filed: a query-level alert cannot be closed with page-row evidence or with a 2-window comparison that ignores the alert's baseline.
- ~~B19~~ **CLOSED 2026-09-12 T20 — no action (Tier C / AP11), not "nothing dropped".** Page-dimension truth: /blogs/domineering-vs-dominating 6→9 clicks, 6,446→11,841 impr (+84%), pos 8.6→8.5 — the page is growing, and T2's "clicks −50% / impr −94%" is not reproducible at page dimension (most likely a rowLimit-truncated query-dimension pull; GSC-MEASUREMENT-INTEGRITY-01, still unfixed). **The query-level rank drop IS real and GSC-corroborated:** "domineering meaning" pos 2.4→10.3 (DataForSEO) ≈ 3.9→9.7 (GSC, 15→754 impr, 0 clicks in both windows). No action follows because this is a Tier C vocabulary query with 0 clicks at pos 2 AND at pos 10 (INTENT-PRIORITY §1 proven-dead family; AP11), and "keyword 0 occurrences" measured the literal phrase — the body carries "domineering" ×34 under a definitional H2. Refresh brief archived (briefs/archive/domineering-vs-dominating-brief.md), tracking-db → MONITOR. W37 professional-input hold untouched.
- ~~B20~~ **CLOSED FALSE POSITIVE 2026-09-12 T20** — live JSON-LD on /worksheets/values-clarification-act ALREADY emits HowTo (6 HowToStep) + FAQPage (6 Q&A) + reviewedBy + BreadcrumbList (curl, canonical host). "HowTo + FAQ schema needed" is false; nothing for Kushal to approve. (Also: Google retired HowTo rich results 2023-09 and restricts FAQ rich results to gov/health-authority sites — a schema sprint could not recover CTR.) tracking-db status → MONITOR with note. Filed to T13: T4's SCHEMA_OPTIMIZATION_NEEDED verdict must read the live JSON-LD before it fires (registry rule 1).

- ~~B5~~ DONE 2026-09-11 T11 — ALGO_WATCH cleared priority sequence flagged to Kushal. Sprint prompts at prompts/auto-drafted-sprint-aeo-perplexity-2026-09-08.md + prompts/auto-drafted-sprint-therapy-near-me-hub-2026-09-04.md awaiting human fire.
- ~~B14~~ DONE 2026-09-11 T11 — form_submitted crash + backend fail rate (13.7%) flagged to engineering. Claude Code prompt at reports/lead-create-failed-diagnosis-2026-09-03.md.
- ~~B17~~ CLOSED 2026-09-07 (DataForSEO 402 resolved)
- ~~B10~~ DONE 2026-09-08 T11 — Chrome stall + GSC OAuth Slack posted
- ~~B13~~ DONE 2026-09-08 T11 — AEO Perplexity sprint prompt saved
- ~~B1~~ CLOSED 2026-08-31
- ~~B2~~ CLOSED 2026-08-31
- ~~B3~~ CLOSED 2026-09-01
- ~~B4~~ CLOSED 2026-08-31
- ~~B6~~ DONE 2026-09-02
- ~~B11~~ CLOSED 2026-09-04
- ~~T14-CWV-01~~ DONE 2026-09-09 T11
- ~~T14-CWV-02~~ DONE 2026-09-09 T11
- ~~T14-SCHEMA-01~~ DONE 2026-09-09 T11

## Awaiting professional input — W37 (2026-09-07)

| Page | Reviewer | Brief | Hold until |
|------|----------|-------|------------|
| /illnesses/learning-disability | Dr. Akanksha Kashinath Bhor | briefs/professional-input/2026-W37/learning-disability-brief.md | recording received OR 2026-09-28 |
| /illnesses/gender-identity-disorder | Sufia Nusrat | briefs/professional-input/2026-W37/gender-identity-disorder-brief.md | recording received OR 2026-09-28 |
| /illnesses/dual-diagnosis | Dr. Vishal Kasal | briefs/professional-input/2026-W37/dual-diagnosis-brief.md | recording received OR 2026-09-28 |
| /treatments/transcranial-direct-current-stimulation-tdcs-therapy | Dr. Arun Kumar V | briefs/professional-input/2026-W37/tdcs-therapy-brief.md | recording received OR 2026-09-28 |
| /treatments/art-therapy | Ms. Navyashri S | briefs/professional-input/2026-W37/art-therapy-brief.md | recording received OR 2026-09-28 |
| /blogs/domineering-vs-dominating | Ms. Suhita Saha | briefs/professional-input/2026-W37/domineering-vs-dominating-brief.md | recording received OR 2026-09-28 |

*Do not refresh any of these pages until recording is received or the 21-day hold expires (2026-09-28).*

---
## T17 Entries — 2026-09-10

| ID | Action | Type | Priority | Notes |
|---|---|---|---|---|
| T17-9-DEPRESSION-AI-CITATION | "Depression Treatment Online India" AEO page | draft_sprint_prompt | HIGH | Absent from Perplexity Q9 3+ weeks. Sprint prompt at prompts/auto-drafted-sprint-aeo-perplexity-2026-09-08.md covers this. Fire post ALGO_WATCH. |
| T17-8-THERAPY-HUB | Therapy-near-me hub (60.5K/mo) | draft_sprint_prompt | CRITICAL | Merged into B12. Prompt drafted 09-04. Fire NOW. |
| T17-COUNSELLING-HUB | Counselling hub (90.5K/mo) | draft_sprint_prompt | HIGH | YourDOST pos=2, MT absent. 6th+ week flagged. Next sprint after therapy-near-me. |
| T17-ADHD-THERAPIST | ADHD therapist hub (9.9K×2) | draft_sprint_prompt | MEDIUM | Check existing ADHD-therapist MDX first. |
