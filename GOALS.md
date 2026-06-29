# GOALS — Mindtalk.in North Star + Quarterly Milestones

**Read by:** Strategist (T10) before every decision.
**Updated by:** Kushal (manual edit) when strategic priorities shift. Meta-Learner can propose adjustments via 7-day preview.
**Last updated:** 2026-06-15

---

## North Star (12-month horizon — by 2027-06)

**One sentence:** Become the #1 organic search destination for mental health in India, with Mindtalk's app as the default free-self-help-to-paid-consult funnel.

### 12-month numeric targets

| Metric | 2026-06 baseline | 2027-06 target | Stretch |
|---|---:|---:|---:|
| Weekly clicks | 1,785 | **10,000** | 15,000 |
| Weekly impressions | 289,315 | **1.2M** | 1.8M |
| Avg CTR | 0.6% | **1.5%** | 2.0% |
| Avg position | 13.6 | **8.0** | 6.0 |
| Pages live | 691 | **1,200** | 1,500 |
| Top-3 ranking queries | ~5,706 | **12,000** | 18,000 |
| Inventory coverage (Track B) | 27% (64/240) | **90%** (216/240) | 100% |
| Brand search volume (mindtalk + variants) | TBD | +200% | +400% |
| Weekly book_appointment_clicked (T15) | 745 unique (W26, 06-24) | **4,000** | 6,000 |
| Weekly UTM-attributed payments (T19, organic) | 15 (W26) | **150** | 250 |
| Weekly Payment Successful (T19, all channels) | 104 (W26, 100% organic) | **800** | 1,200 |
| Doctor-card → booking attribution share | 66.7% (W26) | maintain ≥50% | maintain ≥60% |
| Backend lead_create_failed rate | 0% (since 06-25 fix) | **≤2%** | 0% |

(Conversion KPIs above are LIVE — populated by Task 15 Mixpanel Conversion Monitor on the unified project id 4011856 (marketing site + consult web app + Mindtalk mobile app, merged 2026-06-17). T15 writes weekly to `logs/conversion-intelligence-YYYY-MM-DD.md`; T19 W26 (2026-06-25) added UTM attribution + revenue dimension. Strategist scoring now includes conversion lift as a primary input — see HIGH-CONVERTER-PATTERNS.md, PAGE-CONVERSION-MAP.md, GEO-CONVERSION-MAP.md.)

**Activated 2026-06-29:** the four "TBD" rows that existed in this section before today have been replaced with the live W26 baseline figures. The historical phrasing was "Mixpanel MCP access enabled" — that gate cleared 2026-06-17 when the Mindtalk mobile-app token landed in the same project as marketing + consult. Three rows worth of conversion KPI optimisation now feed Strategist.

---

## Quarterly milestones

### Q3 2026 (Jul–Sep) — "Stabilise + Multiply"
- Weekly clicks: **2,800** (+57% from June baseline)
- Weekly impressions: **420K**
- Avg CTR: **0.85%**
- Pages live: **800**
- Inventory coverage: **45%** (108/240)
- AI Overview citation rate (mindtalk.in cited in AI snippets): **measure baseline first**
- All YMYL pages: 100% reviewer coverage (already done)
- 14-day recovery rate on refresh sprints: **>70%**

### Q4 2026 (Oct–Dec) — "Topical Authority + Bilingual"
- Weekly clicks: **5,000**
- Weekly impressions: **700K**
- Avg CTR: **1.1%**
- Pages live: **950**
- Inventory coverage: **65%** (156/240)
- Bilingual pages (Hindi + Tamil pilots): **20**
- Featured snippet owns: **30** queries (currently ~5)
- Auto-ship success rate: **>85%** of NEW briefs auto-ship cleanly

### Q1 2027 (Jan–Mar) — "Programmatic Scale"
- Weekly clicks: **7,500**
- Weekly impressions: **950K**
- Avg CTR: **1.3%**
- Pages live: **1,100**
- Inventory coverage: **80%**
- Programmatic SEO pages (city × condition matrix): **150 net new**
- Top-3 query count: **9,000**

### Q2 2027 (Apr–Jun) — "12-Month Mark"
- Weekly clicks: **10,000** (North Star)
- Avg CTR: **1.5%** (North Star)
- Avg position: **8.0** (North Star)
- Pages live: **1,200**
- Inventory coverage: **90%**

---

## Production velocity targets (per week)

| Output | Floor | Target | Ceiling (cap) | Auto-shippable? |
|---|---:|---:|---:|---|
| NEW blogs published | 3 | **7-10** | 20 | ✅ Task 9 |
| Refresh shipments | 2 | **5-8** | 20 | ✅ Task 11 (non-YMYL) |
| YMYL refreshes | 0 | 1-3 | 5 | ❌ Manual sign-off |
| Sprint launches | 0 | 1 per 2 weeks | 1/week | ⚠ Drafted auto, fired by human |
| Stub pages (Track B coverage) | 0 | 10-15 | 30 | ✅ Once strategy ratified |
| Investigations completed | 1 | 3 | 8 | ✅ Auto |
| Meta-Learner proposals | 0 | 2-3 | 5 | ⚠ 7-day preview |

If actual velocity stays in **Floor** for 2+ consecutive weeks → Meta-Learner flags as "system underutilised" and proposes either (a) loosen safety filters or (b) discover more opportunities.

If actual velocity hits **Ceiling** consistently → raise the cap (Meta-Learner proposes config update).

---

## Quality bars (every page must meet)

Strategist + Executor + Auto-Ship validate against these before shipping or refreshing:

| Quality bar | Requirement | Verification |
|---|---|---|
| **Reviewer coverage** | Every YMYL page has named clinical reviewer | grep frontmatter `reviewer:` |
| **JSON-LD reviewedBy** | YMYL pages emit Physician schema | curl + grep `"reviewedBy":` |
| **Quick Answer block** | Every blog/illness/treatment page has 50-60 word definitional answer above the fold | Component check |
| **Key Takeaways block** | 4-bullet summary below Quick Answer | Component check |
| **FAQ schema** | ≥5 questions per blog, ≥3 per other YMYL page | YAML frontmatter `faqs:` |
| **Internal links** | ≥3 contextual links to related content | grep MDX body |
| **Meta title** | ≤65 chars, includes brand suffix `| Mindtalk` | char count |
| **Meta description** | ≤160 chars, intent-aligned | char count |
| **Indian English** | "behaviour", "organisation", "counselling", "centre" | scan for US spellings |
| **Mobile-friendly** | Lighthouse mobile ≥90 | Site audit (Task 7) |
| **Build clean** | `npm run build` passes | Auto-ship + Executor gate |

Pages failing any bar are flagged for refresh. Pages can't go live until all bars met.

---

## Quality KPIs (weekly tracking)

| KPI | Current | Target | Strategy lever |
|---|---:|---:|---|
| Avg CTR | 0.6% | 1.5% (12mo) | Meta-rewrite sprints, AI Overview defense |
| Avg position | 13.6 | 8.0 (12mo) | Refresh sprints, internal linking, schema |
| Pages w/ reviewer | 100% (post Sprint A) | 100% | maintain |
| Pages w/ Quick Answer | ~35% | 100% (Q4) | Bulk template sprint |
| Pages w/ FAQ schema | ~40% | 100% (Q4) | Bulk template sprint |
| Pages w/ ≥3 internal links | ~70% (estimate) | 95% (Q4) | Internal-link audit task (proposed) |
| Cluster coverage gaps | TBD | <5 critical gaps | Topical authority audits |
| Stale pages (>180 days no refresh) | TBD | <50 (Q4) | Auto-refresh queue |
| Broken internal links | TBD | 0 | Site audit (Task 7) |
| Pages with schema errors | TBD | 0 | Site audit |

---

## Conversion KPIs (Mixpanel + Freshsales — needs Kushal to plumb)

| KPI | Current | Target |
|---|---|---|
| Organic → consult booking rate | TBD | TBD |
| Organic → app download rate | TBD | TBD |
| Organic → lead form submit rate | TBD | TBD |
| Bounce rate (organic landing) | TBD | <50% |
| Avg session duration | TBD | >2 min |
| Pages per session | TBD | >2 |
| Top converting blogs / illness / treatment pages | TBD | Top 20 list |

Once tracked: Strategist will prioritise refreshes on top-converting pages over high-traffic-but-low-converting ones.

---

## Risk caps (hard limits — autonomous loop NEVER exceeds)

| Risk | Cap | Why |
|---|---|---|
| Max NEW blogs auto-shipped per week | 20 | Brief generation capacity + indexation budget |
| Max refreshes auto-shipped per week | 10 | Blast radius — too many simultaneous changes muddy attribution |
| Max % of pages refreshed in any rolling 30 days | 20% | Don't refresh more than 138 pages of 691 in any month |
| Max % of pages auto-modified in any rolling 7 days | 5% | ~35 pages/week ceiling on autonomous changes |
| Build failures tolerated per week | 0 | Each failure pauses Auto-Ship until human review |
| DataForSEO API spend per month | $200 (~17k INR) | Cap exists; raise via Meta-Learner proposal if needed |
| Watches simultaneously open | 50 | Beyond this Learner can't reliably evaluate weekly |
| Pages touching same cluster within 14 days | 3 | Otherwise can't isolate which change worked |
| Auto-modified files outside `brain/`, `cowork-tasks/`, `config.json`, Cowork SKILL.md | 0 | Production code stays human-controlled |

If any cap is hit, Strategist freezes that action class for 7 days and escalates to Kushal via Slack `⚠ CAP HIT`.

---

## Adaptive learning targets (system intelligence)

| Metric | Target | What it means |
|---|---|---|
| New principles in PRINCIPLES.md per month | 3-5 | Learner extracting durable patterns |
| New anti-patterns per month | 1-3 | Learner identifying harmful patterns |
| Closed watches per week | 5-10 | Action throughput is healthy |
| Watch recovery rate (🟢 verdict) | ≥60% | Strategy playbooks are working |
| Strategist decision confidence avg | rising over time | System reads accumulated memory effectively |
| Meta-Learner proposals applied | 2-3/month | System auto-improves modestly |
| Auto-ship success rate | ≥85% | NEW briefs cleanly convert to live pages |
| Refresh recovery rate (14-day) | ≥70% | Refresh playbook is reliable |

If watch recovery rate drops <40% for 2 weeks → Learner flags playbook failure → Meta-Learner proposes strategy update.

---

## Strategic priorities (Q3 2026 — current quarter)

In order:

1. **Drain the 51-brief backlog** via auto-ship (T9) + refresh ship (T11)
2. **Close the 185-item inventory gap** via stub-page sprint (drafted by Meta-Learner, fired by human)
3. **Hit 100% Quick Answer + Key Takeaways coverage** on all YMYL pages (auto-sprint)
4. **Recovery validation** on Sprints A/B/C (watch checks 2026-06-23)
5. **Auto-Ship pipeline validation** (target 85% success rate by end of July)
6. **Cadabams.org workflow stabilisation** (4 weeks of stable cron runs)
7. **Begin bilingual pilot** (Hindi expansion for top 20 traffic pages)
8. **Begin programmatic SEO pilot** (top 5 city × condition pages)

---

## Anti-goals (things the system MUST NOT prioritise)

- ❌ Optimising for vanity metrics (impressions without clicks)
- ❌ Shipping content for cap-fill (always quality > velocity)
- ❌ Refreshing recently-touched pages (let them settle)
- ❌ Targeting branded queries that already convert well (waste)
- ❌ Chasing every CRITICAL alert (some are false positives — Strategist uses spike-detection)
- ❌ Trying to outrank Cadabams Hospitals on their own brand
- ❌ Expanding to topics outside mental health (stay focused)

---

## Direct-to-Strategist instructions

When you decide today's actions:

1. Read this file
2. Compute: which axis is the site WEAKEST on relative to target?
3. Choose actions that move that axis the most
4. But never violate Anti-goals or Risk caps
5. Log your goal-alignment reasoning in `brain/memory/decisions/{TODAY}.md`

Example: if CTR is at 0.6% target 1.5%, and pages live is at 691 target 800 (Q3), CTR is the bigger gap (60% improvement needed vs 16% for pages). So prioritise meta-rewrite sprints over NEW content shipping this week.

---

## How GOALS.md evolves

- **Kushal** edits this file when strategic priorities shift (e.g., new business goal, new market, conversion KPI plumbed)
- **Meta-Learner** can propose updates via 7-day preview if data suggests targets are mis-calibrated (e.g., Q3 click target was 2,800 but actual run-rate by August suggests 3,500 — propose raise)
- **Learner** updates TRAJECTORY.md weekly with progress; never modifies GOALS.md directly
- **Strategist** never modifies GOALS.md, just reads + optimises toward
