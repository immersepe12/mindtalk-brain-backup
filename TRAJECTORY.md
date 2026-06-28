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
| 2026-06-22 to 06-28 | — †† | — | — †† | — | — | — | 691 | 27% | †† GSC wk 06-22→06-28 not yet available (lands Mon 06-30 after GSC lag). TRAJECTORY snapshot: production velocity 0 NEW / 0 refresh / 3 investigations / 6 formal watch closes (Sprint A W1-W6). Sprint A recovery rate: 1/6 = 17% (well below 60% target). W18 online-therapy hub authored pending push. Posture: hold + reinforce. |

(Learner fills new row every Sunday)

> ⚠ **Source caveat:** the baseline row (289K impr / 13.6 pos) is DataForSEO-sourced; subsequent rows are GSC-sourced, so cross-row deltas prior to 06-15 are NOT apples-to-apples. Within GSC, the trend is clear: clicks 1,785 → 1,997 → 2,302 = consistent weekly growth. The 06-22→06-28 row will be back-filled on Monday 06-30 when the GSC weekly report runs. **Key verdict from this Learner run (06-28):** Sprint A YMYL reviewer playbook confirmed as insufficient alone for top-20 YMYL pages (AP9 codified). Content-depth batch #18 is the primary recovery lever; fire eligibility 07-02.

---

## Production velocity — weekly

| Week | NEW shipped | Refresh shipped | YMYL refresh | Sprints fired | Stubs | Investigations | Total |
|---|---:|---:|---:|---:|---:|---:|---:|
| 2026-06-08 to 06-14 | 6 (manual sprint) | 3 | 0 | 4 (A, B×3, C) | 0 | 1 | 14 |
| 2026-06-15 to 06-21 | 3 (`549dac3`) | 1 (W15 anxiety-neurosis CTR meta, `579bb7c`) | 0 | 0 fired (2 drafted: #8 / #8R conversion-reorientation) | 0 | 4 (sleep-cluster, life-coach, W16 pos-100, 06-19 pos-100) | 8 |
| 2026-06-22 to 06-28 | 0 (T9 vetoed all 4 YMYL briefs; AP3 Option B signed-off but ship pending 06-30) | 0 (ALGO_WATCH hold, 3rd wk below floor) | 0 | 0 fired; #8R conversion sprint flagged to human (human-gated) | 0 | 3 (#19 cannibalization diagnostic, #8R flag_for_human, tech-health batch flag) + 6 formal watch closes (W1-W6 Sprint A Learner close) | 3 (+6 closes) |

---

## Quality KPI tracking

| KPI | Last week | 4-week avg | Q3 target | Status |
|---|---:|---:|---:|---|
| Avg CTR | 0.8% (GSC) | ~0.7% | 0.85% | 🟡 in-range (up from 0.6%; -6% to target) |
| Avg position | 10.1 (GSC) | ~11.7 | (no specific target) | 🟢 best-in-trend (was 13.6) |
| % pages with reviewer | 100% (YMYL) | 100% | 100% | 🟢 met |
| % pages with Quick Answer | ~35% | — | 100% (Q4) | 🟠 in progress |
| % pages with FAQ schema | ~40% | — | 100% (Q4) | 🟠 in progress |
| Top-3 ranking queries | 5,706 (no fresh count) | — | 7,500 (Q3) | 🟡 baseline |
| Pages live | 691 (+3 NEW shipped, count not re-measured) | — | 800 (Q3) | 🟡 baseline |
| Inventory coverage | 27% | 27% | 45% (Q3) | 🟡 baseline |

---

## Conversion KPIs — weekly (Mixpanel T15 / project 4011856)

_Maintained by T15 Conversion Monitor (Wed) — first full reading 2026-06-17 (inaugural 06-15 was access-blocked, so no true WoW baseline yet)._

| Week (7d) | Page views | book CTA clicks | form_submitted | lp_form_submitted | lead_create_failed | Doctor→book CTA % | Flags |
|---|---:|---:|---:|---:|---:|---:|---|
| 2026-06-17 | 3,805 | 1,620 | 8 | 130 | 70 | 69% | lp:form 16x ⚠; on-site booking funnel ~0%; backend fail ~34% ⚠; riya(5)+where-to-start(3) invisible |
| 2026-06-24 | 5,941 | 745 | 6 | 136 | 79 | 69% | Page views +56%✅; book_click -54%⚠⚠ (intent dilution — SEO/blog surge, not commercial pages); LP form +5% (136, leads stable); backend fail ~36% (stable⚠); where-to-start +367%✅ (3→14); riya 10 (doubled, still tiny) |

**Variance > 20% WoW (2026-06-24 reading):**
- book_appointment_clicked: **-54%** ⚠⚠ (1,620→745) — page views surged +56% simultaneously; new traffic is low-intent SEO/blog content. Sequential funnel rate: 17%→13%. LP form absolute stable — actual leads not impacted.
- Page views: **+56%** ✅ — SEO traffic growing strongly
- form_submitted rate (/ page views): -52% (0.21%→0.10%) — denominator inflation; absolute leads stable
- lp_form_submitted rate (/ page views): -33% (3.42%→2.29%) — same; absolute +5% (130→136)
- call_clicked: **-32%** ⚠ (57→39)
- where_to_start discovery: **+367%** ✅ (3→14) — internal linking improvement working
- riya_page_viewed: +100% (5→10) — still effectively invisible

**Standing conversion concerns for Strategist:**
- Real lead capture = landing-page forms (136/wk), not the on-site multi-step booking form (6/wk; sequential conversion ~0%).
- ~36% backend lead-creation failure (lead_create_failed 79 / ~221 form attempts) — persistent 3+ weeks. Engineering issue; escalate to Kushal.
- Doctor-profile path is the strongest intent signal (69% profile→book CTA, stable) — prioritize doctor page SEO/coverage.
- Traffic growth outpacing commercial engagement — new visitors land on blog/SEO content, not booking pages. Add CTAs on high-traffic content pages OR focus acquisition toward commercial-intent queries.
- where_to_start internal linking worked (3→14 viewers). Apply same treatment to riya_page.

**T19 W26 Addendum (2026-06-25) — Paid/Organic separation + revenue layer:**
- Organic book_appointment_clicked: 1,026 (57.6% of 1,781 total). 42.4% was GMB/residual tags (ads paused — not active paid traffic).
- UTM attribution (first full week): 15 payments + 15 appointment-bookings confirmed from mindtalk.in CTAs via mindtalk_web utm_source. Doctor card CTAs = 66.7%; Homepage hero = 20%; Global CTAs = 13.3%.
- Revenue baseline W26: Payment Successful 104, Appointment Booked 87 — both 100% organic (ads paused since May 26).
- UX friction (consult.cadabams.com): booking/53196 = 444 rage+dead clicks (CRITICAL). find-therapist wizard = 293 (HIGH). These are downstream conversion blockers post-mindtalk.in referral.
- AI search: chatgpt.com = 57 book intent events (3.2% of total) — new organic channel, week 1 of tracking.
- See PAGE-CONVERSION-MAP.md + UX-FRICTION-PAGES.md for full tier data.

---

## Adaptive learning — monthly rollup

| Month | Principles added | Anti-patterns added | Watches opened | Watches closed | Recovery rate | Notes |
|---|---:|---:|---:|---:|---:|---|
| 2026-06 (closed) | 9 (+1 AP9) | 9 (+1 AP9) | 18 | 13 (W1-W10, W15-W18 + W16 data-quality + W11 deferred) | 17% (Sprint A: 1/6; Sprint B: 2/3 on merit; Sprint C: 0/1 disconfirmed) | AP9 added 06-28 (YMYL reviewer-only fails top-20 YMYL). Sprint A YMYL recovery 1/6 = below target. Sprint B AI-overview defense confirmed (P2/P10). Sprint C CTR bulk-rewrite disconfirmed (P11). Watch recovery across all types = 3 🟢 + 1 🟡 + 4 🔴 + 1 ⚫ = 9 closed on merits (excl. noise/deferred). |

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
| Weekly clicks | 2,800 (Q3) | 2,302 (GSC, wk 06-13→06-19) | -18% | Gap narrowing (was -36% in June baseline). YMYL recovery (#18 batch 07-02) + CTR v2 (#17 staged) + online-therapy hub (#12 push) are the next levers. W15 anxiety-neurosis CTR verdict (06-30) unlocks or gates #17. |
| Avg CTR | 0.85% (Q3) | 0.8% (GSC) | -6% | Nearly on target. Sprint C disconfirmed bulk approach (P11). W15 verdict 06-30 determines if staged P11 approach is viable. If yes: #17 2-page CTR sample unlocks. If no: hold CTR lever, focus on content-depth + commercial-intent pages (P9). |
| Inventory coverage | 45% (Q3) | 27% | -18pp | Pilot 20 plan at `dev-specs/2026-06-22-stub-page-pilot-20.md` awaiting Kushal sign-off. Earliest fire 06-30. Gap wide; this is the most behind metric. |
| Production velocity (NEW) | 7-10/wk | 0/wk (this week) | below floor (3rd wk) | **⚠ UNDERUTILISATION FLAG.** 3 consecutive weeks below floor (GOALS rule: 2 wks → flag). Root: T9 vetoed all YMYL briefs (old AP3); AP3 Option B now unlocks them. Expected: 4 YMYL blogs ship 06-30 (first T9 delivery since 06-17). If T9 ships cleanly, floor met again next week. |
| Production velocity (refresh + sprints) | refresh 5-8/wk, 1 sprint/2wk | 0 refresh, 0 sprints (this week) | below floor (3rd wk) | **⚠ UNDERUTILISATION FLAG.** 3rd consecutive zero-refresh week. ALGO_WATCH hold justified through 07-02. After 07-02: #18 YMYL-recovery batch + held-refresh queue must resume immediately. If not, escalate as system underutilisation to Kushal. |

---

## Trajectory verdict (Learner's weekly write-up)

**Most recent week (Learner fills weekly):**

> **Week of 2026-06-15 → 06-21 (Learner run 06-21):** A disciplined holding week. The system shipped 3 NEW blogs (`549dac3`, backlog now fully drained), one CTR meta-refresh (W15 anxiety-neurosis, live + ticking to 06-30), and resolved 4 investigations — all confirmed as DataForSEO noise or non-regressions, none requiring content action. The standout outcome is **what the loop correctly did NOT do**: it held the ALGO_WATCH refresh queue and kept both commercial-intent sprints (#12 online-therapy hub, #8R conversion-reorientation) drafted-and-human-gated rather than firing into the core-update rebound. The latest GSC week is up on both clicks (+9.5%) and impressions (+4.9%) with best-in-trend position (10.1) — the late-May pullback has reversed and the clicks/CTR variance gaps narrowed materially (-36%→-29% clicks, -29%→-6% CTR). **No watch closed on the merits** (W11 deferred — Mixpanel blocked; W16 already closed as noise), so recovery rate is still N/A. New learning: codified **AP8** (the exact-position-100 DataForSEO sentinel, 3rd+ confirmation). **Everything now hinges on the 2026-06-23 Sprint A/B/C 14-day checks** — the first real evidence that the reviewer-fix / AI-Overview-defense / CTR-rewrite playbooks move rankings at scale. Next focus: evaluate those reads next Sunday, and if Sprint C is 🟢, green-light the post-06-23 held-refresh resume + the two staged commercial sprints.

> **Week of 2026-06-22 → 06-28 (Learner run 06-28):** A consolidation week with a hard lesson locked in. The system closed Sprint A (W1-W6) formally: **1/6 RECOVERED, 1/6 PARTIAL, 3/6 STALLED, 1/6 WORSE** — a 17% recovery rate against a 60% target. The verdict is clear: **reviewer + JSON-LD alone is not a recovery sprint for YMYL pages already in top-20 positions** (AP9 codified). Production velocity hit zero for the 3rd consecutive week (T9 vetoed all YMYL briefs pre-AP3 Option B; refresh queue intentionally on ALGO_WATCH hold) — this is now an underutilisation flag. The system is in a well-structured hold, but the hold ends 07-02. **Next week's pivots:** (1) 06-30 triple-check (PTSD re-verify + W15 CTR verdict + Jun-9 cohort midpoint) sets direction; (2) 07-02 ALGO_WATCH clears → #18 content-depth YMYL recovery batch fires + held-refresh queue resumes; (3) T9 should ship the 4 Option-B YMYL briefs 06-30 (first T9 delivery in 10 days). The clicks trajectory is healthy (1,785 → 2,302, +29% over 4 weeks); the system just needs to convert its backlog into live pages to sustain it.

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

**AI Overview citation share:** Unchanged — 1 of 10 priority queries rendered a Google AI Overview ("ocd specialist bangalore"); Mindtalk cited #3 (mindtalk.in/Doctors). All 9 others: no AI OV block.
**This week's gain:** ChatGPT login restored → first-ever commercial-intent citation ("online therapy bangalore" → Cadabam's Mindtalk, via local-results). Commercial-query citations 0→1.
**Strategic finding:** brand fragmentation — for commercial/condition queries, AI engines cite cadabamshospitals.com (group) or the Google business listing, NOT the mindtalk.in domain. AEO entity-consolidation needed to route Cadabams AI citations to mindtalk.in.
**Tier movement:** baseline → +1 confirmed citation (3→4); commercial bucket 0→1. Amaha remains the most-cited competitor across all engines.
