# TRAJECTORY — Weekly Progress vs GOALS.md

**Read by:** Strategist (T10) every day, Learner (T12) Sunday before weekly digest.
**Written by:** Learner only — Sunday 6 PM weekly run.
**Purpose:** Single rolling view of how the system is performing relative to its targets.

---

## Headline metrics — weekly

| Week | Clicks | Δ | Impr | Δ | CTR | Pos | Pages | Inv % | YTD path to 12mo goal |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|
| 2026-06-08 to 06-14 | 1,785 | -13.2% | 289K | -32% | 0.6% | 13.6 | 691 | 27% | Baseline (DataForSEO source) |
| 2026-06-15 to 06-21 | 2,302 * | +15.3% * | 290,898 * | +14.2% * | 0.8% | 11.3 | 691 | 27% | * GSC figures from Mon 06-22 report covering wk 06-13→06-19. True 06-15→06-21 data approximated here; Δ vs prior GSC report. Clicks/impr both climbing (2nd straight green week). Position slipped 10.1→11.3 — new impressions skew page-2 (life-coach + counselling surges, near-zero CTR). |
| 2026-06-22 to 06-28 | 2,243 | -2.6% | 296,598 | +2.0% | 0.8% | 10.5 | 691 | 27% | Back-filled 07-05 from `weekly-summary-2026-06-29.txt`. Biggest drop: burnout treatment (pos 6.8→85.9, confirmed QDF normalization + tracker error). Biggest rise: REBT cluster +316.7%. Sprint A recovery rate: 1/6 = 17%. 0 NEW / 0 refresh shipped (ALGO_WATCH hold). W18 online-therapy authored pending push. |
| 2026-06-29 to 07-05 | 2,603 | +16.0% | 304,380 | +2.6% | 0.9% | 10.5 | 691 | 27% | Back-filled 07-12 from `weekly-summary-2026-07-06.txt` (GSC Jun 27–Jul 3, Mon-start ±2d). ✅ **CTR 0.9% — Q3 target (0.85%) first exceeded.** Clicks gap -7.2% vs Q3 target (was -18%). Impr gap -27.5% (lagging axis). Production: 0 live (push failure Day 5+; 4 pages stuck at 404: dbt/play/rebt/emdr). DataForSEO 4/5 API failures (07-02 clean only). W17 closed (gate watch, not merit). ALGO_WATCH cleared 07-02. |
| 2026-07-06 to 07-12 | — ‡ | — | — ‡ | — | — ‡ | — ‡ | 778 | 27% | ‡ GSC Jul 6–12 lands Mon 07-13. **Production UNBLOCKED 07-10:** 87 pages LIVE (77 assessments + 10 stuck pages). Pages 691→778 (+12.6%). Q3 assessment target 80 EXCEEDED (98 MDXes live). T9: 6 blogs authored 07-07/08 — LOCAL ONLY (not pushed yet). Revenue breakout W28 (trailing 7d as of 07-08): Payments 118 (+25.5% WoW), Bookings 107 (+33.8% WoW). June Core Update ACTIVE through 07-17; ALGO_WATCH NOT triggered (0 confirmed drops). STUB-PILOT-TRIAGE-01 URGENT: Kushal decision required before 07-17. |

(Learner fills new row every Sunday)

> ⚠ **Source caveat:** the baseline row (289K impr / 13.6 pos) is DataForSEO-sourced; subsequent rows are GSC-sourced, so cross-row deltas prior to 06-15 are NOT apples-to-apples. Within GSC, the trend is clear: clicks 1,785 → 1,997 → 2,302 = consistent weekly growth. The 06-22→06-28 row will be back-filled on Monday 06-30 when the GSC weekly report runs. **Key verdict from this Learner run (06-28):** Sprint A YMYL reviewer playbook confirmed as insufficient alone for top-20 YMYL pages (AP9 codified). Content-depth batch #18 is the primary recovery lever; fire eligibility 07-02.

---

## Production velocity — weekly

| Week | NEW shipped | Refresh shipped | YMYL refresh | Sprints fired | Stubs | Investigations | Total |
|---|---:|---:|---:|---:|---:|---:|---:|
| 2026-06-08 to 06-14 | 6 (manual sprint) | 3 | 0 | 4 (A, B×3, C) | 0 | 1 | 14 |
| 2026-06-15 to 06-21 | 3 (`549dac3`) | 1 (W15 anxiety-neurosis CTR meta, `579bb7c`) | 0 | 0 fired (2 drafted: #8 / #8R conversion-reorientation) | 0 | 4 (sleep-cluster, life-coach, W16 pos-100, 06-19 pos-100) | 8 |
| 2026-06-22 to 06-28 | 0 (T9 vetoed all 4 YMYL briefs; AP3 Option B signed-off but ship pending 06-30) | 0 (ALGO_WATCH hold, 3rd wk below floor) | 0 | 0 fired; #8R conversion sprint flagged to human (human-gated) | 0 | 3 (#19 cannibalization diagnostic, #8R flag_for_human, tech-health batch flag) + 6 formal watch closes (W1-W6 Sprint A Learner close) | 3 (+6 closes) |
| 2026-06-29 to 07-05 | 0 (4 authored 06-30 — BLOCKED: git push auth failure Day 5+; all at 404) | 0 (all blocked; ALGO_WATCH cleared 07-02 but push frozen) | 0 | 0 (git push failure blocks all; #18 YMYL eligible but unexecutable) | 0 | 1 (W17 gate watch close) | 0 LIVE ⚠⚠ |
| 2026-07-06 to 07-12 | 0 LIVE (6 authored by T9 07-07/08 — LOCAL ONLY; PAT push pending) | 0 | 0 | 0 (assessments = one-time batch event, not sprint) | 0 (STUB-PILOT-TRIAGE-01 — pilot BLOCKED pending Kushal decision) | 1 (ILLNESS-CLUSTER-01 → Core Update noise confirmed 07-10) | **87 LIVE from 07-10 batch** (77 assessments + 10 stuck pages); T9 blogs LOCAL ONLY ⚠ |

---

## Quality KPI tracking

| KPI | Last week | 4-week avg | Q3 target | Status |
|---|---:|---:|---:|---|
| Avg CTR | 0.9% (GSC) | ~0.75% | 0.85% | 🟢 **EXCEEDED** — Q3 target first met wk 06-29→07-05; hold for 2nd consecutive week to confirm trend |
| Avg position | 10.5 (GSC) | ~11.2 | (no specific target) | 🟢 improving trend (was 13.6); minor regression from 10.1 expected as impressions-heavy assessment cluster indexes |
| % pages with reviewer | 100% (YMYL) | 100% | 100% | 🟢 met |
| % pages with Quick Answer | ~35% | — | 100% (Q4) | 🟠 in progress |
| % pages with FAQ schema | ~40% | — | 100% (Q4) | 🟠 in progress |
| Top-3 ranking queries | 5,706 (no fresh count) | — | 7,500 (Q3) | 🟡 baseline |
| Pages live | 778 (691 + 77 assessments + 10 stuck → live 07-10) | — | 800 (Q3) | 🟢 -2.8% gap (was -13.5%); assessment Q3 target 80 EXCEEDED ✅ (98 live) |
| Inventory coverage (Track B) | 27% | 27% | 45% (Q3) | 🟡 baseline — STUB-PILOT-TRIAGE-01 blocking progress |

---

## Conversion KPIs — weekly (Mixpanel T15 / project 4011856)

_Maintained by T15 Conversion Monitor (Wed) — first full reading 2026-06-17 (inaugural 06-15 was access-blocked, so no true WoW baseline yet)._

| Week (7d) | Page views | book CTA clicks | form_submitted | lp_form_submitted | lead_create_failed | Doctor→book CTA % | Flags |
|---|---:|---:|---:|---:|---:|---:|---|
| 2026-06-17 | 3,805 | 1,620 | 8 | 130 | 70 | 69% | lp:form 16x ⚠; on-site booking funnel ~0%; backend fail ~34% ⚠; riya(5)+where-to-start(3) invisible |
| 2026-06-24 | 5,941 | 745 | 6 | 136 | 79 | 69% | Page views +56%✅; book_click -54%⚠⚠ (intent dilution — SEO/blog surge, not commercial pages); LP form +5% (136, leads stable); backend fail ~36% (stable⚠); where-to-start +367%✅ (3→14); riya 10 (doubled, still tiny) |
| 2026-07-01 | 6,397 | 764 | 4 | 151 | 17 | 66% | Page views +8%✅; **backend fail -78%✅✅✅** (35.7%→9.9% — possible engineering fix deployed); LP form +11%✅ (136→151); call_clicked +38%✅ recovery; book CTA stable (+3%); lp:form ratio 38x⚠ (on-site form irrelevant); riya 6⚠ (tiny, still invisible) |
| 2026-07-08 | 6,342 | 784 | 5 | 129 | 2 | 73% | Page views stable (-1%); **backend fail -88%✅✅✅** (9.9%→1.5% — continued recovery, now negligible); **riya +133%✅✅** (6→14, first real break from invisibility); illness -27%⚠ (161→118); lp_form -15%⚠ (151→129); doctor→book CTA 73% (new high✅✅); lp:form=25.8x |

**Variance > 20% WoW (2026-07-08 reading):**
- lead_create_failed: **-88%** ✅✅✅ (17→2) — backend fail rate 9.9%→1.5%. Recovery holding and deepening. Verify in Freshsales that ~129 LP leads are arriving.
- riya_page_viewed: **+133%** ✅✅ (6→14) — first meaningful break from invisibility (was stuck at 5-10 for 4 weeks). Still tiny absolute, but directionally positive.
- doctor→book CTA: **+10.6%** ✅✅ (66%→73%) — new high. Doctor pages are the strongest conversion path.
- illness_page_viewed: **-26.7%** ⚠ (161→118) — high-intent pages losing traffic. Check illness-cluster rankings.
- lp_form_submitted: **-14.6%** (151→129) — marginal dip, watch for next week. May be production freeze effect (0 pages shipped 4 consecutive weeks).

**Variance > 20% WoW (2026-07-01 reading — archived):**
- lead_create_failed: **-78%** ✅✅✅ (79→17) — backend fail rate 35.7%→9.9%. Strongest signal in 3 weeks. Possible engineering fix. Verify in Freshsales: are ~136 LP leads actually arriving?
- lp_form_submitted: **+11%** ✅ (136→151) — absolute lead volume growing
- call_clicked: **+38%** ✅ (39→54) — recovery after last week's -32% drop
- where_to_start_page_viewed: **+21%** ✅ (14→17)
- form_submitted: **-33%** ⚠ (6→4) — tiny sample (noise likely)
- riya_page_viewed: **-40%** ⚠ (10→6) — tiny absolute; more blog traffic diluting discovery rate

**Variance > 20% WoW (2026-06-24 reading — archived):**
- book_appointment_clicked: **-54%** ⚠⚠ (1,620→745) — page views surged +56% simultaneously; new traffic is low-intent SEO/blog content. Sequential funnel rate: 17%→13%. LP form absolute stable — actual leads not impacted.
- Page views: **+56%** ✅ — SEO traffic growing strongly
- form_submitted rate (/ page views): -52% (0.21%→0.10%) — denominator inflation; absolute leads stable
- lp_form_submitted rate (/ page views): -33% (3.42%→2.29%) — same; absolute +5% (130→136)
- call_clicked: **-32%** ⚠ (57→39)
- where_to_start discovery: **+367%** ✅ (3→14) — internal linking improvement working
- riya_page_viewed: +100% (5→10) — still effectively invisible

**Standing conversion concerns for Strategist (updated 2026-07-08):**
- Real lead capture = landing-page forms (129/wk, -15% this week — watch), not the on-site multi-step booking form (5/wk; sequential conversion ~0%).
- Backend fail rate: **1.5%** (was 9.9%, was 35.7% — recovery appears complete). Verify with Freshsales that ~129 LP leads are arriving cleanly. If confirmed, this is a resolved issue.
- Doctor-profile path is the strongest intent signal (**73% profile→book CTA, new high**) — doctor page SEO is the highest-leverage conversion lever.
- illness_page_viewed -27% this week (161→118) — high-intent traffic class dropping. Check illness-cluster rankings urgently; may be linked to production freeze (0 pages shipped 4 weeks).
- riya_page_viewed: 14 this week (+133% WoW) — first real jump. Still tiny (~0.22% discovery rate) but directional signal. Continue internal linking to riya page.
- lp_form -15% (151→129): marginal dip, likely noise or production freeze effect. If it persists next week, investigate LP landing page changes.

**T19 W26 Addendum (2026-06-25) — Paid/Organic separation + revenue layer:**
- Organic book_appointment_clicked: 1,026 (57.6% of 1,781 total). 42.4% was GMB/residual tags (ads paused — not active paid traffic).
- UTM attribution (first full week): 15 payments + 15 appointment-bookings confirmed from mindtalk.in CTAs via mindtalk_web utm_source. Doctor card CTAs = 66.7%; Homepage hero = 20%; Global CTAs = 13.3%.
- Revenue baseline W26: Payment Successful 104, Appointment Booked 87 — both 100% organic (ads paused since May 26).
- UX friction (consult.cadabams.com): booking/53196 = 444 rage+dead clicks (CRITICAL). find-therapist wizard = 293 (HIGH). These are downstream conversion blockers post-mindtalk.in referral.
- AI search: chatgpt.com = 57 book intent events (3.2% of total) — new organic channel, week 1 of tracking.
- See PAGE-CONVERSION-MAP.md + UX-FRICTION-PAGES.md for full tier data.

**T19 W28 Addendum (2026-07-08) — REVENUE BREAKOUT WEEK + Pattern 5 confirmed:**
- **Organic revenue (W28):** Payment Successful 118 (+25.5% WoW), Appointment Booked 107 (+33.8% WoW). Best combined revenue week in 4 weeks of tracking.
- **UTM attribution (week 4):** mindtalk_web-attributed payments = 22 (+83% WoW from 12). Doctor card = 13 payments (+44%); Homepage hero = 9 payments (+200% — accelerating fast). Cumulative 4-week confirmed: 57 mindtalk_web-attributed payments.
- **Organic intent share milestone:** book_appointment_clicked organic = 60.5% of total (first week organic share exceeded paid residual signal — milestone).
- **AI search channel CONFIRMED (3 weeks):** chatgpt.com = 155 book clicks (+40.9%). 7.5% of ALL organic clicks. T5 unlock: AI-citable content angles (India MH stats, structured expert profiles, FAQ schema).
- **Tier classification unchanged (4 weeks):** Goldmines = /doctors/* + /experts/*; Rockets = /doctors/telugu-speaking + tamil-speaking; Engagement Engine = /blogs/*; Leaky Buckets = 0; Tracking Gap = homepage (hero confirmed converting but book_click instrumentation missing).
- **UX friction W28:** NEW CRITICAL — checkout dead clicks = 68 (payment flow, direct revenue impact). booking/8796 (aparna-rani) = 183 total events (+444% dead clicks). find-therapist improving (481→371). **Dev team priority: fix checkout dead clicks before W29.**
- **Geo concentration:** Bengaluru 60.2% of intent. Karnataka 61.6% share. New markets: Kerala +191% (week 1 — watch W29), Pune +213% (week 1). AP/Vijayawada crash confirmed W27 anomaly.
- See PAGE-CONVERSION-MAP.md + GEO-CONVERSION-MAP.md + HIGH-CONVERTER-PATTERNS.md for full data.

---

## Adaptive learning — monthly rollup

| Month | Principles added | Anti-patterns added | Watches opened | Watches closed | Recovery rate | Notes |
|---|---:|---:|---:|---:|---:|---|
| 2026-06 (closed) | 9 (+1 AP9) | 9 (+1 AP9) | 18 | 13 (W1-W10, W15-W18 + W16 data-quality + W11 deferred) | 17% (Sprint A: 1/6; Sprint B: 2/3 on merit; Sprint C: 0/1 disconfirmed) | AP9 added 06-28 (YMYL reviewer-only fails top-20 YMYL). Sprint A YMYL recovery 1/6 = below target. Sprint B AI-overview defense confirmed (P2/P10). Sprint C CTR bulk-rewrite disconfirmed (P11). Watch recovery across all types = 3 🟢 + 1 🟡 + 4 🔴 + 1 ⚫ = 9 closed on merits (excl. noise/deferred). |
| 2026-07 (in progress) | 0 (3+ rule; 0 merit closes Wk 1-2) | 0 (3+ rule) | 4 (W18-W21 assessments day-7 = W22 — fires 07-17) | 0 merit (W17 gate watch only 07-05; W10-D28 sub-check 07-07 — no rank data captured) | N/A (0 merit closes) | Learner 07-05: W17 STALLED (gate, not merit). Learner 07-12: 0 merit (W10-D28 no capturable data; May-28 cohort = CANNIBAL-BLOG-01, Strategist-captured). Next merit closes: W18-W21 check 07-13; assessments Day-7 (W22) 07-17. |

---

## Action distribution — last 4 weeks

| Action class | Count | Avg outcome | Confidence going forward |
|---|---:|---|---|
| YMYL reviewer fix | 55 pages (Sprint A) | 14d check fires 06-23 | High (logged P1) |
| AI Overview defense | 3 pages (Sprint B) | 14d check fires 06-23 | Medium (novel) |
| CTR meta-rewrite | 21 pages (Sprint C 20 + W15 anxiety-neurosis) | Sprint C 06-23; W15 06-30 | High (logged P4) |
| Homepage redesign | 1 page | ⏸ deferred — Mixpanel blocked | Unmeasured (logged P9) |
| NEW blog ships | 9 pages (6 manual + 3 auto-ship `549dac3`) | W12-W14 indexation 07-01 | High |
| Refresh ships | 4 pages (3 prior + W15) | 14d watches open | Medium |
| Manual investigations | 6 (Reduce Stress, sleep-cluster, life-coach, W16, 06-19 pos-100, +earlier) | All resolved as noise/non-regression | High (logged AP5, AP8) |

---

## Risk caps — current usage

| Cap | This week usage | Limit | Status |
|---|---|---|---|
| NEW blogs auto-shipped | 3 (`549dac3`) | 20 | 15% — healthy headroom |
| Refresh auto-shipped | 1 (W15) | 10 | 10% — well under |
| % pages refreshed (rolling 30d) | ~5% | 20% | 25% of cap — fine |
| % pages auto-modified (rolling 7d) | ~0.6% | 5% | 12% of cap — fine |
| Build failures | 0 | 0 | 🟢 |
| Watches simultaneously open | 15 | 50 | 30% of cap — fine |
| Sprints fired | 0 (target 1/2wk; 2 drafted, human-gated post-06-23) | 1/wk | under — intentional (ALGO_WATCH hold) |

---

## Variance flags (where actual diverges materially from target)

| Metric | Target | Actual | Variance | Recommended action |
|---|---|---|---|---|
| Weekly clicks | 2,800 (Q3) | 2,603 (GSC, wk 06-29→07-05) | -7.2% | Gap narrowed significantly (was -18%). Assessments cluster (98 MDXes live 07-10) should add indexation signal from 07-17+. #18 YMYL recovery + #12 online-therapy hub + sustained T9 throughput are next levers. |
| Avg CTR | 0.85% (Q3) | 0.9% (GSC) | ✅ +5.9% EXCEEDED | Q3 target first exceeded wk 06-29→07-05. Monitor wk 07-06→07-12 GSC (lands 07-13) to confirm sustained vs one-week spike. Assessment pages indexing may temporarily dilute site CTR (new pages start at low CTR). |
| Pages live | 800 (Q3) | 778 | -2.8% | Assessment cluster batch (77 pages) + stuck-page unblock (10 pages) closed most of the gap. T9 6 blogs local-only — next Mac Mini push brings ~784. On track to hit 800 by late July. |
| Inventory coverage (Track B) | 45% (Q3) | 27% | -18pp | **Highest-priority variance flag.** STUB-PILOT-TRIAGE-01 is blocking all stub progress (Batch 2 fires 07-17 with identical structural blockers). Kushal decision (Options A-D) required before 07-17. |
| Production velocity (T9 blogs) | 7-10/wk | 6/wk (LOCAL ONLY) | at floor | T9 operational (6 blogs authored 07-07/08) but sandbox push gap means blogs remain local until Mac Mini push or PAT fallback fires. PAT fallback now wired per 07-10 workflow hardening. |

---

## Trajectory verdict (Learner's weekly write-up)

**Most recent week (Learner fills weekly):**

> **Week of 2026-06-15 → 06-21 (Learner run 06-21):** A disciplined holding week. The system shipped 3 NEW blogs (`549dac3`, backlog now fully drained), one CTR meta-refresh (W15 anxiety-neurosis, live + ticking to 06-30), and resolved 4 investigations — all confirmed as DataForSEO noise or non-regressions, none requiring content action. The standout outcome is **what the loop correctly did NOT do**: it held the ALGO_WATCH refresh queue and kept both commercial-intent sprints (#12 online-therapy hub, #8R conversion-reorientation) drafted-and-human-gated rather than firing into the core-update rebound. The latest GSC week is up on both clicks (+9.5%) and impressions (+4.9%) with best-in-trend position (10.1) — the late-May pullback has reversed and the clicks/CTR variance gaps narrowed materially (-36%→-29% clicks, -29%→-6% CTR). **No watch closed on the merits** (W11 deferred — Mixpanel blocked; W16 already closed as noise), so recovery rate is still N/A. New learning: codified **AP8** (the exact-position-100 DataForSEO sentinel, 3rd+ confirmation). **Everything now hinges on the 2026-06-23 Sprint A/B/C 14-day checks** — the first real evidence that the reviewer-fix / AI-Overview-defense / CTR-rewrite playbooks move rankings at scale. Next focus: evaluate those reads next Sunday, and if Sprint C is 🟢, green-light the post-06-23 held-refresh resume + the two staged commercial sprints.

> **Week of 2026-06-22 → 06-28 (Learner run 06-28):** A consolidation week with a hard lesson locked in. The system closed Sprint A (W1-W6) formally: **1/6 RECOVERED, 1/6 PARTIAL, 3/6 STALLED, 1/6 WORSE** — a 17% recovery rate against a 60% target. The verdict is clear: **reviewer + JSON-LD alone is not a recovery sprint for YMYL pages already in top-20 positions** (AP9 codified). Production velocity hit zero for the 3rd consecutive week (T9 vetoed all YMYL briefs pre-AP3 Option B; refresh queue intentionally on ALGO_WATCH hold) — this is now an underutilisation flag. The system is in a well-structured hold, but the hold ends 07-02. **Next week's pivots:** (1) 06-30 triple-check (PTSD re-verify + W15 CTR verdict + Jun-9 cohort midpoint) sets direction; (2) 07-02 ALGO_WATCH clears → #18 content-depth YMYL recovery batch fires + held-refresh queue resumes; (3) T9 should ship the 4 Option-B YMYL briefs 06-30 (first T9 delivery in 10 days). The clicks trajectory is healthy (1,785 → 2,302, +29% over 4 weeks); the system just needs to convert its backlog into live pages to sustain it.

> **Week of 2026-06-29 → 07-05 (Learner run 07-05):** The system's most constrained week since launch — **0 live pages shipped** for the 4th consecutive week due to a git push auth failure that has frozen all production since 06-30 (Day 5+). Four pages (what-is-dbt-therapy, what-is-play-therapy, what-is-rebt-therapy, emdr-for-anxiety) were authored and are ready, but stuck at 404. The ALGO_WATCH cleared on schedule (07-02), so the strategy is correctly unblocked; the blocker is purely infrastructure. DataForSEO API also failed on 4/5 days this week, leaving the system flying blind on rank signals. On the positive side: D9-execute delivered doctor briefs (kannada-speaking-doctors + psychiatrists-in-hyderabad), the Sprint C day-28 check task was created for 07-07, and 3 Meta-Learner proposals apply tonight via Strategist. **Single next action that unblocks everything: Kushal runs `git push origin main` from Mac Mini.** Until then, no PRINCIPLES/ANTI-PATTERNS update is possible (0 merit watch closes), no content reaches production, and no recovery hypothesis can be tested.

> **Week of 2026-07-06 → 07-12 (Learner run 07-12):** The infrastructure break-free week. Kushal's 07-10 push sent **87 pages live in a single deployment** (77 assessments + 10 previously-stuck pages), lifting the site from 691 to 778 pages and exceeding the Q3 assessment target (98 live vs 80 target). Interlinking across the 37-hub assessment structure was hardened the same day (commit 868f2f7 — all category grids dynamic, siblings surfaced). Revenue continued its breakout trend (W28: Payments +25.5% WoW, Bookings +33.8% WoW, doctor→book CTA 73% all-time high). The prior week's CTR 0.9% reading exceeded the Q3 target for the first time — the GSC read for this week (lands 07-13) will confirm if it holds. T9 shipped 6 clean blogs (07-07/08) but all remain LOCAL ONLY due to sandbox push limitations. **0 formal merit watches closed by Learner** this week: W10-D28 sub-check fired 07-07 but produced no capturable rank data (DataForSEO reliability); W18-W21 check dates fire TOMORROW 07-13 (not yet due). The emerging structural gap: **STUB-PILOT-TRIAGE-01 must be resolved by Kushal before 07-17** (Batch 2 fires identically broken — all 20 picks are redundant or crash). June Core Update remains ACTIVE through 07-17; ALGO_WATCH NOT triggered (0 confirmed YMYL drops confirmed).

---

## How TRAJECTORY.md gets updated

Every Sunday 6 PM, Learner:

1. Reads `reports/weekly-summary-{YESTERDAY}.txt` for headline metrics
2. Reads `logs/auto-ship-*.txt` and Executor logs from the past week
3. Counts watches opened/closed/recovered from `brain/WATCH.md` + closed experiments
4. Computes 4-week rolling averages
5. Compares actual vs Q3 targets in GOALS.md
6. Adds row to "Headline metrics — weekly" table
7. Adds row to "Production velocity — weekly" table
8. Updates "Quality KPI tracking" status emojis
9. Recomputes "Variance flags" — if any metric is >30% off target, propose adjustment
10. Writes "Most recent week" verdict in 2-3 sentences
11. Includes TRAJECTORY snapshot in Sunday Slack digest

Strategist reads this every day before deciding actions — knows where the gaps are.

---

## Conversion KPIs (T19-owned — Conversion Intelligence, Wed weekly)

> Written by T19, not Learner. Source: Mixpanel 4011856, trailing 7d.

| Week | Site intent rate | Median page intent | 🟢 Goldmines | 🟡 Rockets | 🔴 Leaky | ⚫ Dead | Top geo (share) | Revenue-validated bookings | Notes |
|---|---:|---:|---:|---:|---:|---:|---|---:|---|
| 2026-06-15 to 06-21 | 42% | 39.6% | 2 | 2 | 1 | 6 | Bengaluru (65%) | n/a (3986277 unavailable) | INAUGURAL · LIMITED_BASELINE · vol gates scaled · book_appointment-only intent |

**Geographic concentration metric:** Bengaluru = 65% of all booking intent (high single-market dependence).
**Tier movement:** n/a (no prior week).

---

## AI Search Citation KPIs (T17-owned — Competitive + AI Monitor, Thursday weekly)

> Written by T17, not Learner. Source: live queries vs Perplexity / ChatGPT / Claude / Google AI Overview, 10 priority queries.

| Week | Confirmed citations | Perplexity | ChatGPT | Claude | Google AI OV | Commercial-query citations (1-5) | Notes |
|---|---:|---|---|---|---|---:|---|
| 2026-06-18 | 3 / 40 cells | 2/10 (branded only) | SKIPPED (logout) | 0 clean (3 tested; branded contaminated) | 1/10 (AI OV present on only 1 query) | 0 | INAUGURAL BASELINE · Amaha = most-cited competitor · ChatGPT login needed · AI OV detection unreliable |
| 2026-06-25 | 4 / 25 cells tested | 2/10 (branded only — unchanged) | 1/3 sampled (NEW — login restored) | 0/2 commercial (cites group hospital, not MT) | 1/10 (ocd-specialist, MT #3 — unchanged) | 1 (ChatGPT "online therapy bangalore" → Cadabam's Mindtalk) | +1 citation WoW · ChatGPT now ACCESSIBLE · first commercial-intent citation · brand-fragmentation finding (group domain wins Cadabams citations) · Amaha still #1 competitor |
| 2026-07-02 | 3 / 25 cells tested (Perplexity 2 + Google 1) | 2/10 (unchanged) | ⬜ not tested | ⬜ not tested | 1/10 (Q8 cadabams app GAINED · Q10 ocd LOST · net 0) | 0 | 5 new AI OV blocks appeared on MH queries (Q1,Q4,Q5,Q8,Q9) — Mindtalk absent from all commercial ones; Amaha cited in Q1+Q9 |
| 2026-07-09 | 4 confirmed | 2/10 (unchanged, Q6+Q8) | 1/3 tested (Q8 🟢 GAINED) | ⬜ not tested | 1/10 (Q10 ocd 🟢 REGAINED + 4 centers named) | 0 | 🚨 ADHD cluster collapsed for both Amaha+Mindtalk (algo update) · 🟢 MT now #2 on "psychiatrist near me" (110k vol) · Google AI OV rendering intermittent — track rolling avg · ChatGPT Q8 branded citation confirmed |

**AI Overview citation share:** Unchanged — 1 of 10 priority queries rendered a Google AI Overview ("ocd specialist bangalore"); Mindtalk cited #3 (mindtalk.in/Doctors). All 9 others: no AI OV block.
**This week's gain:** ChatGPT login restored → first-ever commercial-intent citation ("online therapy bangalore" → Cadabam's Mindtalk, via local-results). Commercial-query citations 0→1.
**Strategic finding:** brand fragmentation — for commercial/condition queries, AI engines cite cadabamshospitals.com (group) or the Google business listing, NOT the mindtalk.in domain. AEO entity-consolidation needed to route Cadabams AI citations to mindtalk.in.
**Tier movement:** baseline → +1 confirmed citation (3→4); commercial bucket 0→1. Amaha remains the most-cited competitor across all engines.
