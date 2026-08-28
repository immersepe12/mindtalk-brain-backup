# REMEDIATION LOG — Task 20 (Auto-Remediation, self-healing layer)

**Owner:** T20 (daily 8:45 PM IST, after T10 Strategist).
**Purpose:** the layer between "flagged" and "human". Verify every flag against ground truth, fix what is mechanical, escalate only what needs a human — and arrive with the fix pre-written.

---

## 2026-08-17 (Monday) — FIRST LOGGED RUN

**Inputs read:** `brain/BACKLOG.md` (top-5 + carry-forward), `brain/BRAIN.md`, `brain/WATCH.md`,
`brain/memory/decisions/2026-08-17.md`, `logs/{rank-summary,gsc-validation,new-content,briefs,observation,data-quality-suspect}-2026-08-17.*`,
`logs/ops-health-2026-08-16.log`, `flagged-drops.json`, `confirmed-drops.json`, `config.json`.

**Verifier sub-agent:** spawned adversarially against this run's own claims. Returned 2 VETOs and 5 corrections.
**All were honoured. The corrections are recorded below as first-class output, not footnotes.**

---

### A. FALSE POSITIVES CLOSED (Rule 1) — 29 total

#### A1. Rank-flag queue: `flagged-drops.json` 40 → 13 (27 closed)

`flagged-drops.json` was written at 11:07 today with 39 new `flagged_date: 2026-08-17` entries —
**after** T2's GSC validation ran at 09:42. So the entire queue reached the Strategist unvalidated.
All 40 were verified against GSC (current 2026-08-07→08-14 vs previous 2026-07-31→08-07).

| Closure basis | n | Evidence standard used |
|---|---|---|
| No visibility loss (impressions AND clicks both non-decreasing) | 19 | Average position fell only because additional URLs entered the impression pool. Impressions up or flat, clicks up or flat → no traffic was lost. |
| Below `config.json → thresholds.minor_drop_positions = 3` | 5 | Of these, **3 had GSC positions that IMPROVED**: `therapy counseling` −12.3, `mental health psychologist` −9.3, `biofeedback` −0.8. The rank tracker reported these as drops. |
| AP5 spike-normalisation | 2 | Prior week was 2.9x–3.9x *better* than the 4-week median → current value is a return to baseline. `mental peace` (3.5 vs median 10.0), `anxiety headache` (8.5 vs median 30.0). |
| AP11 Tier C permanent reject | 1 | `what do life coaches do` — INTENT-PRIORITY.md §0/§1 names "life coach" as proven-dead. T3 skipped it identically today. |

Closed set with per-entry evidence + 6-week position series: `alerts/flagged-drops-closed-by-T20-2026-08-17.json`
Pre-verification backup: `flagged-drops.backup-2026-08-17-pre-T20-verification.json`

**Scale check — the number that matters:** across all 13 *retained* flags, total weekly organic
clicks at stake is **~9**. Site-wide over the same week: **3,564 clicks (+7.7% WoW), CTR 0.85% (up),
average position 10.9 → 11.7**. The engine has been assigning P0/CRITICAL attention to the extreme
tail of a 21,436-query distribution while the aggregate grows.

**A site-wide-event hypothesis was raised and FALSIFIED, not assumed.** The 6-week per-query series
showed nearly every flagged query degrading in the same single window after 5 stable weeks, which
looked like one algorithmic/technical event. The site-wide weekly aggregate shows no step change
(position +0.8, clicks +7.7%, query count 20,811→21,436, pages 841→837). Conclusion: selection
effect from picking the worst ~40 of 21k queries in one 7-day window, not a shared cause.
`ALGO_WATCH` correctly stays FALSE.

#### A2. `SCHEMA-MEDICAL-TYPES-01` — PARTIALLY resolved (2 of 4 gaps), P0 hold on YMYL is lifted
Curled live and parsed JSON-LD across all 41 YMYL targets:
- `FAQPage` **41/41** ✅
- `MedicalCondition` **21/21** on `/illnesses/*` ✅ · `MedicalTherapy` **20/20** on `/treatments/*` ✅
- `MedicalWebPage` **0/41** ❌ still missing
- Homepage still emits no `ItemList` and no `BreadcrumbList` ❌

**Verifier correction honoured:** the original flag named **4** gaps, not 2. "Resolved" was overstated.
The 2 remaining gaps are `src/**` template changes → escalated as a dev spec (E3 below), not closed.
The consequence that matters: **the BACKLOG hold "DO NOT QUEUE more illness refreshes targeting
Bangalore intent until dev fixes schema templates (deadline 08-26)" rests on a satisfied premise
and no longer blocks.** See D1 for why the hold should nonetheless stay, on different grounds.

#### A3. `CWV-DOCTORS-PAGE-01` — REAL, and now FIXED (relabelled, not closed as a false positive)
Flag: `/doctors/psychiatrists-in-bangalore` LCP 8.95s, perf 56, dev deadline 2026-08-26.
Re-measured (PageSpeed Insights, mobile): **LCP 2.40s, perf 88, CLS 0, FCP 1.05s.**
CrUX field data (28-day): **LCP p75 1,535ms = FAST.**
Also re-measured: `/doctors/therapists-in-bangalore` LCP 2.3s perf 78 · `/assessments` LCP 2.3s perf 70
(flag had claimed assessments worsened to 7.34s).

**Verifier correction honoured:** this is **not** a false positive. T14's original row recorded the
identical FCP (1.05s) alongside LCP 8.95s — the signature of a lazy LCP element, which was real.
Live HTML now shows 3 `rel=preload as=image` links and the first 3 doctor cards without
`loading="lazy"` — an affirmative shipped fix. Calling it a false positive would wrongly discredit
the T14 CWV sensor. **Recorded as: flag was real, fix has landed, 08-26 deadline discharged.**
Residual: TBT 410ms / 900ms / 1,980ms is high (interactivity, not LCP) — logged as an observation,
not escalated, because the flag was scoped to LCP.

#### A4. Brief starvation / `T5-REFILL-CRITICAL-13` / `SYSTEM-UNDERUTILISED` — stale, closed
`logs/ops-health-2026-08-16.log` reports "Brief runway: 161 files, ~0 shippable /blogs/ briefs",
13th consecutive carry. Recounted today: **12 shippable `/blogs/` briefs** (has `intent_tier`
**and** slug returns 404). Floor is 6. The ops-health reading predates today's brief creation.
The 13-week starvation series is **closed on evidence**, not carried a 14th time.
*Verifier caveat recorded:* 2 of the 12 (`conduct-disorder-in-children`, `relationship-problems-and-solutions`)
still carry NEEDS_HUMAN / AP9 markers in BACKLOG, so effective runway is ~10 — still above floor.

#### A5. Mixpanel access block — stale memo
`brain/memory/mixpanel-access-blocked.md` documents project 4011856 as payment-blocked since
2026-07-22. Project is **queryable now**. The memo is stale and is flagged for correction (D3).

---

### B. AUTO-FIXES APPLIED — 6

| # | Fix | Before → After |
|---|---|---|
| B1 | **`brain/.git/index.lock` cleared** | Stale 23h lock; `rm` fails EPERM on the FUSE mount, and ops-health escalated it to Kushal as "Kushal must run: rm …". Cleared with `os.rename()` (documented FUSE workaround). `git status` now works, 43 files visible. **This was never a human task.** |
| B2 | **Paid search-term mining recovered** | T5 logged "PAID MINING SKIPPED — Supermetrics MCP authentication unavailable". Ran the registry-repointed `scripts/google-ads-search-terms.py` instead → **exit 0, 4,506 terms, 198 qualified**. Saved to `data/paid-mining/google-ads-search-terms-2026-08-17.json`. This produced the run's most valuable finding (C1). |
| B3 | **3 stale briefs archived** (never deleted) | Targets return HTTP 200 = already shipped: `NEW-handling-partners-anger-in-relationship`, `NEW-how-to-fix-ptsd` (→ `/blogs/how-to-fix-ptsd-recovery-steps`, filename ≠ target), `NEW-tamil-speaking-doctors-in-chennai`. `briefs/` 57 → 54. |
| B4 | **2 briefs had an unroutable URL prefix** | `NEW-online-psychiatry`, `NEW-therapists-for-anxiety-and-depression` specified `/doctors-listings/<slug>`. Verified live: `/doctors/psychiatrists-in-mumbai` = 200, `/doctors-listings/psychiatrists-in-mumbai` = **404**. Content in `src/content/doctors-listings/` serves at `/doctors/`. Corrected + route note added. Would have shipped 2 Tier A pages to a dead prefix. |
| B5 | **`flagged-drops.json` rewritten to verified state** | 40 → 13, each retained entry carrying its GSC window, 6-week position series, and clicks-at-stake. |
| B6 | **Stale discovery re-run attempted** | `DISCOVERY STALE` (cache 7.0d). Re-ran `new-content-discovery.py --all` → **timed out again (178s; prior attempts 120s + 180s)**. Fell back to cache per the T5 ladder. Cache age is inside the 21-day escalation threshold → logged, **not escalated**. Root cause is a script-level timeout needing a chunked/resumable mode; `scripts/*.py` is out of T20's scope → D2. |

**Standing job — brief-queue health: 12 shippable `/blogs/` briefs ≥ floor of 6. Starvation auto-fix
NOT fired (not needed). No new briefs generated, so no Verifier content gate was required.**
The Verifier sub-agent was instead pointed at this run's own verification claims.

---

### C. ESCALATED TO KUSHAL / DEV — 4 (each with the fix pre-written)

#### C1. `THERAPIST-NEAR-ME-CRITICAL-02` — reframed, and now carries a rupee value
**The headline number is wrong; the underlying problem is worse than "moderate".**

The flag reads "pos 13→79, −65.7% collapse on a 60.5K/mo Tier A query". Decomposition:
- GSC query-level: pos 12.78 → 74.46, **but impressions 1,579 → 2,302 (+46%) and clicks 6 → 8 (+33%)**.
- Page-level, filtered to the query: **8 URLs at position 153–254 contributed 730 impressions this
  window vs 21 the previous week** — that alone drags the impression-weighted average.
- **Excluding URLs beyond position 100: 12.64 → 25.69.**

So ~47 of the 62 positions are arithmetic dilution. The remaining **13.05 positions are a real
regression — and by `config.json → major_drop_positions: 11` that is MAJOR, not moderate**
(Verifier correction honoured). Per-hub, some of it is CRITICAL:

| URL | prev → cur | impressions |
|---|---|---|
| `/doctors/therapists-in-hyderabad` | 10.9 → **32.4** (−21.5, CRITICAL) | 273 → 332 |
| `/doctors/therapists` | 10.4 → 29.0 | 384 → 242 |
| `/doctors/therapists-in-bangalore` | 12.0 → 26.7 | 618 → 952 |
| `/doctors/psychologists-in-bangalore` | 24.0 → **152.7** | 113 → 307 (gaining impressions while collapsing) |

**Why this is now the highest-value item in the engine — paid data (B2), 30 days, account 2992649306:**

| Paid search term | clicks | conversions | spend |
|---|---|---|---|
| **therapist near me** | 260 | **38.5** | **₹11,263** |
| psychologist near me | 141 | 13.92 | ₹8,176 |
| psychologist bangalore | 95 | 11.17 | ₹6,257 |
| couple therapy bangalore | 45 | **14.99** (33% CVR) | ₹1,254 |

The single query whose organic position "collapsed" is the **#1 converting paid term in the account**.
Every other flag in today's queue is worth ~9 clicks/week combined; this cluster is worth 38.5
measured conversions/month at ₹11,263 of spend that organic could displace.

**Two decisions needed (both are judgement, which is why they escalate):**
1. **Cannibalization/consolidation call** — 8+ Mindtalk URLs compete for one query, several at pos 150+.
   Recommendation: canonicalise the near-me cluster onto `/doctors/therapists-in-<city>`, and stop
   `/centers/*` and `/doctors/mental-health-professionals-in-*` from surfacing for it.
2. **`/doctors/*` is programmatic React** (confirmed 2026-08-05: body content lives in `page.tsx`,
   MDX carries SEO fields only) → any fix is a `src/**` change. T20 cannot touch it.

#### C2. `CLINICAL-FAQ-SIGN-OFF-01` — **stays escalated, re-scoped UPWARD. My initial closure was wrong.**
I first closed this as a false positive on the grounds that FAQPage already emits on 41/41 pages,
so sign-off could not be "the blocker for schema". **The Verifier VETOED this, correctly.**

The count was right and the reasoning was wrong. The live FAQ text **is verbatim the
`PENDING_CLINICAL` draft** — `/illnesses/alzheimers` serves the exact 4 Q&As in
`faqs-pending-clinical-review/yaml/alzheimers.yaml`. Per `faqs-pending-clinical-review/SHIP-PROMPT-claude-code.md`
these shipped today under an owner override, marked
`clinical_review_status: owner_approved_pending_clinician_signoff`.

**So clinician sign-off is not a stale blocker — it is outstanding on YMYL content that is already
public.** That is a *higher*-risk state than when the flag was written, not a resolved one.
VERIFIER §5 requires `clinical_reviewer_signed_off` (named, ≤90d) for `/illnesses/*` and `/treatments/*`;
41 live pages currently carry FAQ content with no named reviewer. Closing this item would have
deleted the only tracker for an open AP3 exception.

**Escalation:** the docx is with the clinician (`faqs-pending-clinical-review/Mindtalk-FAQ-Clinical-Review.docx`).
Needed: a named reviewer + date, written back to the 41 pages' frontmatter. Urgency is now
**compliance**, not SEO. *(Noted in fairness: the run that shipped these explicitly refused to
fabricate a clinician name and recorded the override honestly — the right call.)*

#### C3. `SCHEMA-MEDICAL-TYPES-01` residual — dev spec, 2 remaining gaps
- Add `MedicalWebPage` to the illness/treatment JSON-LD graph (0/41 emit it today).
- Homepage: emit `ItemList` + `BreadcrumbList` (neither present).
Both are `src/**` template changes. The 2 already-fixed gaps (`FAQPage`, `MedicalCondition`/`MedicalTherapy`)
are verified live and need no further work.

#### C4. `/treatments/life-coach-therapy` — human decision, 3rd consecutive skip
Sole entry in `confirmed-drops.json`. T3 has skipped it twice for AP11 + `url_locked` + `algo_watch`
+ W23 informational closure. This is a strategic keep-or-retire call, not mechanics.
Options unchanged: (a) remove from `confirmed-drops.json` and archive the URL as Tier C permanent;
(b) explicitly override AP11 and brief it.

---

### D. NOT ESCALATED — routed to Learner / Meta-Learner instead

| # | Item | Why it is not Kushal's |
|---|---|---|
| D1 | **W36 🔴 STALLED / W37 ⚫ WORSE — the schema root cause is falsified; here is the real one.** Both pages shipped correctly (titles live). GSC: depression impressions **1,255 → 1,703 (+36%)**, anxiety **412 → 804 (+95%)**, position roughly flat — but clicks fell (3→2, 2→1) and CTR halved. The targeted Bangalore queries **do rank**: "depression treatment bangalore" pos 7.4, "…in bangalore" pos 12.2, "anxiety treatment in bangalore" pos 6.9. They generate **~9 impressions per 14 days each and 0 clicks**. Meanwhile both pages absorb large long-tail impression volume at pos 30–55 ("addicted to melancholy", "anxiolytic meaning", "$wmp depressed"), which craters CTR. **This is a demand problem, not a schema problem: the AP3-B refresh optimised for Bangalore geo-intent queries that are barely searched.** Recommendation: keep the "no more Bangalore-intent illness refreshes" hold, but change its stated reason from *schema-blocked* to *demand-unvalidated*, and validate volume before the next one. | A strategy input for T12/T10 |
| D2 | `new-content-discovery.py --all` times out on every invocation (120s / 180s / 178s). Needs a chunked or resumable mode. | `scripts/*.py` is the Strategist Verifier's; T20 must not edit it |
| D3 | `brain/memory/mixpanel-access-blocked.md` says project 4011856 is payment-blocked since 2026-07-22; it is queryable now. Memo needs correcting. | Housekeeping |
| D4 | `brain/.git/index.lock` recurs **nightly** — the directory holds ~50 `index.lock.*` aside-artifacts dating from 2026-06-15 to today. Every night a task renames it aside and (sometimes) escalates it. Permanent fix belongs in the T16 backup spec: use `os.rename()`, stop escalating. | Meta-Learner proposal |
| D5 | **Method correction for future runs (Verifier).** I attributed the small-sample closures to **AP8**; AP8 is specifically about the DataForSEO position-100 sentinel rotating between pulls — a different data source with no impressions concept. The apt pattern is **AP5**, whose prescribed test (prior week > 3× the 4-week median) I had not run. I ran it, and rebuilt every closure on config-backed thresholds, documented anti-patterns, or a visibility test (impressions **and** clicks non-decreasing). | Discipline note |
| D6 | **A 30-impression baseline floor I invented mid-run closed 16 of 40 flags and is now withdrawn.** `config.json` has no sample-size parameter. Sound at the extremes (`autism` 1 prior impression, `adverse childhood experiences test` 4, `aces test` 5) but undocumented as to *why 30*. If a minimum-impressions gate is wanted it belongs in `config.json` via a T13 proposal applied through T10 Step 10 — not inline in a run. Final closures use no such floor. | T13 proposal candidate |
| D7 | **2 entries I closed and the Verifier reopened.** `counseling services near me` — worst-in-six-weeks (25.3→37.4), AP5 ratio 0.73x so no spike, baseline 34 impressions, commercial intent; it met the survivors' own criteria. `how to fix your sleep cycle` — my "dilution" label masked live self-cannibalization: `/blogs/guide-to-reset-your-sleep-cycle` 3.2→10.6 while sibling `/blogs/how-to-fix-your-sleep-schedule-quickly` (T9 auto-ship, 2026-07-28) sits at pos 7.2. Both restored to `flagged-drops.json`. The second is a self-inflicted signal and the more important of the two. | Corrected in-run |
| D8 | The "clicks did not fall" leg of the no-visibility-loss test is **vacuous where both windows are 0 clicks** (5 of the closures), and 2 closures had *flat* rather than rising impressions (`sleep talking causes` 51→51, `how to fix your sleep cycle` 34→34). The test needs an explicit zero-click branch. | T13 proposal candidate |
| D9 | `/tmp` collisions are live in this environment — the Verifier's first pass silently grepped another user's stale file and inverted a result. Use unique temp paths. | Discipline note |

---

### E. STILL OPEN — verification not possible this run

**`BACKEND-FAIL-TREND-01` — NOT closed. Verifier VETO honoured.**
I first closed it on the weekly `lead_create_failed` counts (67, 56, 6, 5, 0, 4, 25, 10, 13, 3 for
weeks 06-15 → 08-17), concluding the upward trend had not continued. That is not a valid test:
**the flag is defined on a rate** ("7.5% this week… escalate if next week exceeds 10%"), and a
falling numerator is fully consistent with a rising rate if attempts fell faster. Two further
problems: the last two *complete* weeks are **10 → 13, i.e. rising**, and the terminal "3" is the
week of 08-17 — today — roughly one day of data.

I attempted the denominator: project 4011856 returns data for `lead_create_failed` only;
`lead_created`, `lead_create_success`, `lead_form_submit`, `form_submit` all return nothing, and an
`$all_events` breakdown by Event Name returned `undefined`. **The flag stays open.** To resolve it,
one input is needed: the denominator event name T19 used to compute 7.5% on 2026-08-05.

Provenance caveat (Verifier): if 4011856 really was payment-blocked from 2026-07-22 (per D3), then
the low post-07-22 counts may reflect degraded collection rather than genuine improvement. That
ambiguity is itself a reason not to close.

---

### RUN SUMMARY

| | |
|---|---|
| Flags collected | 46 (40 rank + 6 named backlog/ops items) |
| **False positives closed with evidence** | **29** (27 rank + brief-starvation + Mixpanel memo) |
| **Auto-fixed** | **6** (index.lock · paid mining recovered · 3 briefs archived · 2 unroutable brief URLs · flagged-drops rewritten · discovery re-run attempted) |
| **Escalated** | **4** (near-me cluster + paid value · clinical FAQ sign-off · schema dev spec ×2 gaps · life-coach keep/retire) |
| Routed to Learner/Meta-Learner instead of Kushal | 9 |
| Still open, verification blocked | 1 (`BACKEND-FAIL-TREND-01`) |
| Brief queue | **12 shippable `/blogs/`** (~10 effective) vs floor 6 → healthy, starvation fix not needed |
| Pages shipped | 0 (no shipping required; queue healthy) |
| Verifier sub-agent | 2 VETOs + 5 corrections — **all honoured; 2 closures reversed, 2 reopened** |

**Net:** 29 items stopped reaching Kushal. 6 fixed without him. The two items I initially got wrong
were caught in-run by the Verifier and corrected before delivery — which is the mechanism working
as designed, and the reason the digest reports 4 escalations rather than 2.

---

## 2026-08-21 (Friday) — RUN 2

**Inputs read:** `brain/BACKLOG.md`, `brain/BRAIN.md`, `brain/INTENT-PRIORITY.md`, `brain/VERIFIER.md`,
`logs/{auto-ship,stub-pilot,data-quality-suspect,rank-summary,rank,gsc-validation}-2026-08-21.*`,
`flagged-drops.json`, `confirmed-drops.json`, `config.json`, and the live website repo.

**Verifier sub-agent:** spawned adversarially against this run's own claims. Returned **6 VETOs and
11 corrections. All honoured.** Two of my conclusions were reversed outright (T17-7 closure; acrophobia
rejection) and two briefs were structurally broken until it caught them. The corrections are recorded
below as first-class output.

---

### A. FALSE POSITIVES CLOSED (Rule 1) — 2

#### A1. `CWV-ASSESSMENTS-CRITICAL-01` — CLOSED
Flagged 2026-08-19 (T14) as *"/assessments LCP 2.33s→10.93s, perf 86→59, NEW CRITICAL, P0, must be fixed
before the Day-42 assessment-cluster evaluation on 08-21."*

Re-measured today via PageSpeed Insights API (mobile, key from `config.json`, fetched 2026-08-21T15:29:44Z,
`finalUrl https://www.mindtalk.in/assessments`):

| Metric | 08-19 flag | 08-21 re-measure |
|---|---:|---:|
| Performance | 59 | **89** |
| LCP | 10.93s | **2,401ms** |
| FCP | — | 906ms |
| CLS | — | 0 |

The lab regression did not reproduce two days later. Closed on lab evidence.

*Verifier correction C1 (honoured):* I had also cited "assessments CrUX field LCP p75 1,542ms FAST" as
supporting evidence. That figure is **origin-level, not page-level** — `loadingExperience.id` is the bare
origin and carries `origin_fallback: True`, meaning CrUX has insufficient page-level samples for
`/assessments` and PSI substituted the sitewide aggregate. Evidence struck. The closure stands on the lab
re-measurement alone.

#### A2. `T17-24-CHROME-STALL-4TH-ESCALATION` — CLOSED as an infrastructure failure
Escalated four consecutive Thursdays (07-30, 08-06, 08-13, 08-20) as *"CRITICAL INFRASTRUCTURE: the
extension itself is disconnected; AI citations untested for 4 weeks; root cause likely the extension
losing its session during long Mac Mini runs."*

Verified today: `list_connected_browsers` returns a live macOS instance. Two AI-citation queries executed
**end to end** through the extension. The extension is not broken.

**Real root cause: a render-wait bug in the T17 procedure.** On a JS-rendered AI answer page, the first
`get_page_text` returns *"No text content found"* — the page has not hydrated. After a ~25s wait the full
answer is present. T17 has been reading the pre-hydration DOM and recording it as a stall.

This is a procedure fix (add a wait/retry loop before reading), i.e. a **T13 Meta-Learner proposal**, not
a Kushal escalation. Supersedes T17-18 and T17-19. Four weeks of escalation for a missing sleep().

**Bonus — 2 of 4 blind weeks partially recovered while proving the point:**
- Q1 `best mental health platform india` → **Mindtalk ABSENT.** Perplexity cites Amaha (first), Tele-MANAS,
  Wysa, TalktoAngel, Psyra, BetterLYF. T17-15's "monitor 2 more weeks before acting" window (set 07-30)
  has now elapsed at 3 weeks.
- Q3 `psychiatrist near me bangalore` → **Mindtalk CITED**, described as offering psychiatrist
  consultations at five Bengaluru centres with same-week availability.

---

### B. AUTO-FIXED — 4

| # | Item | Before → After |
|---|---|---|
| B1 | Brief-queue refill (standing job) | 8 raw / **5 effective** `/blogs/` briefs → **11 raw / 8 effective**. 3 new blog briefs written and Verifier-passed. |
| B2 | Tier A `/doctors/` gap on the account's best-CVR cluster | No couples/marriage listing page existed (only `relationship-issues-*`). Wrote `briefs/NEW-couples-therapists-in-bangalore-brief.md`. |
| B3 | Paid-conversion mining | `scripts/google-ads-search-terms.py` ran clean (account 2992649306, 30d). Surfaced the couples cluster: ~34 conversions on ₹4,910, incl. `couple therapy bangalore` **31% CVR** and `couple therapy near me` **38% CVR**. Both new cost briefs are grounded on it. |
| B4 | BACKLOG hygiene | 3 stale `draft_sprint_prompt` rows resolved without escalation — T17-22 re-scoped, T17-23 and T17-25 rejected with evidence. |

**Briefs written (all Verifier-passed):**

| Brief | Tier | Grounding |
|---|---|---|
| `NEW-couple-therapy-cost-in-bangalore` | A | Paid ~34 conv/30d @ up to 38% CVR; GSC `coupl*` family 5,257 impr / 32 clicks / 0.61% CTR / pos ~10. `/treatments/couples-therapy` mentions cost 3× with no fee section. |
| `NEW-rtms-treatment-cost-in-india` | A | GSC 122 impr/28d across 4 procedure-cost queries, pos 2.3–29.5; head term at 29.5. Neither live rTMS page contains a price. |
| `NEW-acrophobia-treatment-fear-of-heights` | B | 14,800/mo, Amaha pos=10, Mindtalk has zero acrophobia content. Scoped to treatment intent. |
| `NEW-couples-therapists-in-bangalore` | A | doctors-listing, not `/blogs/` — handed to T9/T11, not shipped by T20. |

Run composition: **3 `/blogs/` briefs = 2 Tier A + 1 Tier B (67% Tier A)**, satisfying INTENT-PRIORITY §3
(≥60% Tier A, ≤30% Tier B, 0 Tier C). No pages shipped; weekly cap untouched (T9 at 7/20).

---

### C. ESCALATED — 3

#### C1. `T17-7-AEO-DOCTORS-SPRINT-01` — **stays open. My closure was wrong; the Verifier reversed it.**
I closed this as a false positive on the evidence that `/doctors/<slug>` renders MDX bodies and emits
FAQPage schema. **That evidence is real but it is about a different page class.** There are three:

| Page class | Source | MDX body? | FAQPage live | Status |
|---|---|---|---|---|
| `/doctors` (index) | `src/app/doctors/page.tsx` — hardcoded JSX | **NO** | **0** | **T17-7 target — genuinely dev-blocked** |
| `/doctors/<listing-slug>` | `doctors-listings/*.mdx` | YES | 5 | unblocked |
| `/doctors/<doctor-slug>` | `doctors/*.mdx` | frontmatter only | 0 | partially blocked |

All three claims in the original 08-05 flag check out against the live tree: `page.tsx` calls
`getFile("pages/doctors")` once, inside `generateMetadata` only; `content/pages/doctors.mdx` has
`seo.structuredData: null` and no `faqs:`; live `/doctors` emits FAQPage count 0. My own task spec also
names *"programmatic doctor-page executor"* in its escalate table — closing it contradicted the registry.

**Ask unchanged: Option A, dev adds a `faqs:` reader to `src/app/doctors/page.tsx` (~2h).**

#### C2. `CWV-REGRESSION-05` — **downgraded P0 → P2, not closed.** Homepage only.
Homepage lab LCP **reproduces** (11.04s today vs 11.65s on 08-19) — so "oscillation artifact" was the wrong
framing and I have dropped it. But it is **unattributable**: `largest-contentful-paint-element` returns zero
items, the last network request completes at **5.79s**, FCP is 0.96s and CLS is 0. Nothing is loading at 11s.

Decisive evidence: **page-level** CrUX (`loadingExperience.id = https://www.mindtalk.in/`, no origin
fallback) gives **LCP p75 = 1,437ms, FAST**. Google's CWV ranking input is field p75, so the "must fix
before the 08-26 core update" framing is unsupported.

Caveats stated rather than buried: CrUX is a 28-day rolling window and would dilute a recent regression —
rebutted by field LCP never crossing 2.5s across five flagged regressions since June. And the homepage
CrUX `overall_category` is **AVERAGE**, not FAST, dragged by **INP 232ms**. The page is not green; it is
not an LCP emergency. Dev spec stands; the weekly P0 re-escalation should stop.

#### C3. Brief-queue shortfall — **declared, not hidden.**
Spec target is ≥12 shippable. Post-run: 11 raw / **8 effective**. **Shortfall 4.**

*Verifier VETO 6 (honoured):* I triggered the refill on the **effective** count (5 < 6) and then reported
completion against the **raw** count. Triggering on effective is defensible and the spec supports it
("real shippable queue, not raw file count"), but measuring completion on raw is metric-switching. Held to
one metric throughout, the refill is **+3 `/blogs/`** (the couples-therapists brief is `/doctors/` and does
not count) against a target of 12 effective. Root cause of the residual gap is unchanged: the genuinely
un-served, non-cannibalizing `/blogs/` territory is close to exhausted, which is itself the argument for
consuming the 42 Tier A `/doctors/` briefs.

---

### D. ROUTED TO LEARNER / META-LEARNER — not Kushal's

| # | Item |
|---|---|
| D1 | **T17 render-wait fix** — add a hydration wait + retry before `get_page_text` on AI answer pages. Closes 4 weeks of phantom Chrome stalls. |
| D2 | **`BRAIN-ACROPHOBIA-CLAIM-01`** — the 08-13 Strategist stamp claims "acrophobia, claustrophobia already covered". Neither page exists. |
| D3 | **`YMYL-PATH-GATE-DRIFT-01`** — proposed PRINCIPLE: a medical-procedure page placed under `/blogs/` still requires a named clinical reviewer, regardless of path. The AP3-B gate is path-triggered, so commercial scoping can route around it; that is drift even when the resulting page is compliant. |
| D4 | **Reviewer-load state is stale/transposed.** T9 logs carry tirzah-johnson=9 and tejal-jaiswal=7; actual counts from `src/content/blogs/*.mdx` are **tirzah-johnson 6, tejal-jaiswal 9**. Load-based reviewer assignment is running on wrong numbers. |
| D5 | **`new-content-discovery.py` still cannot complete.** `--all` times out (D2 of the 08-17 run); `--gsc` exits 0 without rewriting `new-content-opportunities.json` (mtime still 08-17 10:26). Needs a chunked/resumable mode — `scripts/*.py` belongs to the Strategist Verifier, not T20. |
| D6 | **Stray build artifacts in the repo:** `src/content/blogs/what-is-biofeedback-therapy.mdx.tmp_merge` and `what-is-rtms-treatment.mdx.tmp_merge`. `src/**`, so not T20's to remove. Low priority. |
| D7 | **`filterCondition` values are hyphenated** (`Relationship-Issues`), matched against `d.illnesses` in `src/lib/doctors.ts`. A space-separated value silently renders an empty specialist list. Worth a lint at brief-generation time — it would have shipped a blank Tier A page today. |

---

### E. TODAY'S SENSOR FLAGS — verified, no action needed

- **T1 rank sweep:** 289 keywords, **0 new flags**, 0 CRITICAL.
- **AP8 quarantine (9 URLs → position 100 in one sweep):** correctly auto-quarantined as API noise. I
  confirmed all 9 return **HTTP 200** live, so no real deindexation sits underneath the sentinel. No escalation.
- **T2 GSC validation:** 3 carry-over MODERATE flags → 2 closed as NOISE/IMPROVING, 1 CONFIRMED
  (`/blogs/psychology-of-love`, CTR_DROP, rank 2→9, impressions +353% while clicks halved). T3 has already
  written `briefs/psychology-of-love-brief.md`. Working as designed; not a T20 item.
- **T9 auto-ship:** SKIPPED on the `/blogs/` cluster cap (7/6, next slot 08-25). Correct behaviour, not a flag.
- **Stub-pilot:** 2nd consecutive workless run. The 08-14 Slack escalation is the standing flag; the task
  correctly declined to re-ping. **Not re-escalated today** — Kushal's (a)/(b)/(c) decision is 7 days old
  and weekly re-pings are noise.

---

### RUN SUMMARY

| | |
|---|---|
| Flags collected | 14 (BACKLOG open items + today's sensor logs) |
| **False positives closed with evidence** | **2** (CWV-ASSESSMENTS-CRITICAL-01 · T17-24 Chrome stall, 4 weeks running) |
| **Auto-fixed** | **4** (queue refill +3 blog briefs · Tier A couples listing brief · paid mining · 3 BACKLOG rows resolved) |
| **Escalated** | **3** (T17-7 `/doctors` index — *reinstated after my wrong closure* · CWV-REGRESSION-05 downgraded P0→P2 · queue shortfall 4) |
| Routed to Learner / Meta-Learner | 7 |
| Brief queue | 11 raw / **8 effective** `/blogs/` (was 8 / 5) · target 12 · **shortfall 4** |
| Pages shipped | 0 |
| Verifier sub-agent | **6 VETOs + 11 corrections — all honoured.** 2 conclusions reversed, 2 briefs structurally fixed. |

**Net:** the highest-value output is **not** a fix — it is `DOCTORS-LISTINGS-UNBLOCKED-01`: **42 Tier A
`/doctors/` briefs are shippable today** and have been sitting idle behind a blocker that applies to a
different page class. Tier A is the 70–95%-intent class and the most reliable attribution signal in the
system. Two multi-week escalations (Chrome ×4, assessments CWV) stopped reaching Kushal.

**And the run's own discipline note:** I got two things materially wrong — closing T17-7 by conflating
page classes, and rejecting acrophobia by inverting the zero-click-trap test. Both were caught in-run and
corrected before delivery. That is the mechanism working, and it is why this digest reports 3 escalations
rather than 1.

---

## 2026-08-22 (Saturday) — RUN 3

**Inputs read:** `brain/BACKLOG.md` (T10 stamp 08-22), `brain/WATCH.md`, `brain/INTENT-PRIORITY.md`,
`brain/VERIFIER.md`, `logs/{observation-2026-08-22, ops-health-2026-08-21, stub-pilot-2026-08-21,
gsc-validation-2026-08-21, rank-summary-2026-08-21, data-quality-suspect-2026-08-*, auto-ship-2026-08-21,
conversion-intelligence-2026-08-19}`, `flagged-drops.json`, `confirmed-drops.json`, `config.json`,
`briefs/*.md` (57), the live site (58 curl checks), Mixpanel 4011856, and GSC.

**Verifier sub-agent:** spawned adversarially against this run's own claims. Returned **2 VETOs, 3
CORRECTIONS, 1 UPHELD — approval rate 1 of 5. All honoured.** Two of my conclusions were withdrawn
outright and the brief I amended had to be substantially reverted. The corrections are the most
important output of this run and are recorded as first-class content below, not as footnotes.

---

### A. FALSE POSITIVES CLOSED — **0**

I intended to close two. Neither survived the Verifier. Both became downgrades instead. Recording zero
closures rather than inflating the number is the point of the mechanism.

---

### B. DOWNGRADED — verified-real, but materially mis-stated — 2

#### B1. `DEAD-CLICKS-W34-CRITICAL-01` — **CRITICAL → P2 chronic. Ad-spend block WITHDRAWN.**

Flag (2026-08-20, T19 W34): *"Dead clicks 4,441 (+111% WoW). Paid traffic amplifying broken UX…
revenue leak… escalate immediately; block further BOF ad spend increase until UX fixed."*

Ground truth, Mixpanel project 4011856 — **the same project T19 queried** (confirmed in
`logs/conversion-intelligence-2026-08-19.md`: *"Mixpanel project: 4011856 (unified)"* and
`brain/UX-FRICTION-PAGES.md`: *"project 4011856, trailing 7d"*). Project 3986277 does not exist in this
account, so the "T20 measured a different source" objection fails and verification was legitimate.

| Window | Dead clicks |
|---|---:|
| Aug 5–11 | 3,856 |
| **Aug 12–18 (W34)** | **4,304** |
| **WoW** | **+11.6%** |

**The "+111%" is a scope artifact, not a decimal slip** *(Verifier CORRECTION — my first framing was
wrong)*. `UX-FRICTION-PAGES.md` line 17 shows the comparison: site-wide W34 `4,441` against a W33 column
of `~2,100` explicitly marked **"(est)"**. That W33 estimate came from `conversion-intelligence-2026-08-12.md`
Q10–Q12, which measured only three URL clusters (`/appointments` 535 + `/assessments` 750 +
`/find-therapist` 615 = 1,900). A site-wide total was divided by a three-cluster subtotal.

**My "trend is DOWN 4 consecutive weeks" claim was FALSE and is withdrawn** *(Verifier CORRECTION — the
most important catch of the run)*. I read the `2026-08-17` weekly bucket (3,657) as a completed week. It
is a **partial week** — 08-17 is a Monday and today is Saturday. Daily run-rates tell the opposite story:

| Window | Dead clicks/day |
|---|---:|
| Aug 5–11 | 551 |
| Aug 12–18 | 615 |
| **Aug 17–21 (current)** | **660 — highest in the 9-week series** |

Projecting ~4,620/wk, **above** the 07-20 peak of 4,393. Volume is rising.

**What does survive:** the dead-click-per-pageview *rate* has oscillated 7.8–10.9% for nine straight
weeks with no trend (latest 9.37%). Dead clicks scale with traffic; bug density is unchanged.

**Verdict:** real problem, wrong number, wrong urgency. The "+111% doubling" that justified blocking ad
spend is not real, so **that recommendation is withdrawn**. But this is a chronic UX defect at an
all-time-high absolute volume on the highest-intent traffic — it stays open at P2. Two further notes:
I verified one sub-claim and would have closed the whole row, which would have silently deleted the
**`doctor_card` attribution-bleed (3rd recurrence)** item — that remains **unverified and open**. And I
never reconciled my 4,304 against T19's 4,441 (3.2% gap, same project, same window, same event).

#### B2. `T5-REFILL-CRITICAL-16` — **CRITICAL → P3. 16 consecutive days of a false premise.**

Flag: *"16th consecutive carry. **0 shippable NEW blog briefs in queue.** T9 cannot ship new blogs
without fresh briefs. Mac Mini must run T5 NOW."*

I parsed all 57 `briefs/*.md`, extracted `**intent_tier:**` and `**Suggested URL:**`, and curl-verified
every slug against the live site:

| Class | Briefs | Live check | Shippable |
|---|---:|---|---:|
| `/blogs/` with `intent_tier` | 11 | **11/11 → HTTP 404** | 11 raw / **8 effective** |
| `/doctors/` Tier A | 43 | **43/43 → HTTP 404** | 43 |
| `/treatments/` | 0 | — | **0** |

(3 `/blogs/` are NEEDS_HUMAN per `auto-ship-2026-08-04.txt`: conduct-disorder-in-children,
relationship-problems-and-solutions, gender-identity-disorder → effective 8.)

**"0 shippable" has been false for 16 consecutive days.** But *(Verifier CORRECTION)* I over-reached by
citing 54: the flag's own body says *"Doctor listings briefs stuck separately — T5 needs `/blogs/` and
`/treatments/` new briefs"*, so it had already excluded the 43. On its own scope the honest number is
**8 `/blogs/` + 0 `/treatments/`**.

**And it is not wholly false** — 2 of its 3 named Tier A priorities are genuinely unwritten:
`psychologists-in-kochi` (absent) and a Kerala/Kochi `malayalam-speaking-doctors` variant (only
`-in-delhi` / `-in-mumbai` exist), with P8 Kerala confirmed 4 weeks. So: **downgrade and re-scope to
those specific gaps, do not close.**

**The finding underneath the finding — the bottleneck is consumption, not generation.**
`logs/auto-ship-2026-08-21.txt`: `Status: SKIPPED — cluster cap exceeded · /blogs/ cluster: 7/6 (next
slot 2026-08-25) · **Candidates in queue: 49**`. T9 is sitting on 49 candidates and shipping zero
because of the VERIFIER §9 cluster cap. Generating briefs today could not have produced one page.

*(Verifier CORRECTION, accepted:* the 08-21 run reported the identical queue — 11 raw / 8 effective —
and **escalated** it as a shortfall. Same numbers, opposite verdict 24 hours later. The reconciliation
is that yesterday's run had *triggered* the refill at 5 < 6 and was then obliged to reach 12; today the
trigger never fires. Stated plainly rather than left as a silent inconsistency.*)

---

### C. MY OWN CLAIMS VETOED AND WITHDRAWN — 2

#### C1. `ASSESSMENT-AIO-SCHEMA-AUDIT-01` — **my closure WITHDRAWN. Flag stays OPEN, re-scoped.**

I claimed all three proposed fixes were disposed of. **VETOED on the evidence.**

- My "interpretation section is already present" finding used the regex
  `interpret(ing|ation)? your (score|results)|what your score means|how to interpret`. The Verifier
  re-ran it: it returns **exactly 2 hits on every page, both the same string in the same template
  block** — the sitewide CTA *"Mindtalk's psychiatrists and clinical psychologists **can interpret your
  results**"*. That is a booking CTA saying a *clinician* will interpret — the opposite of on-page
  interpretation. **My evidence was boilerplate.**
- The conclusion nonetheless survives on evidence I failed to gather. The Verifier extracted the H2/H3
  trees: `ace-test` → *"What ACE scores predict"*, *"What to do with a high ACE"*; `dass-21` →
  *"DASS-21 severity band table"*; `obq-44` → *"OBQ-44 profile interpretation"*; `c-ssrs` →
  *"Safety planning after C-SSRS"*. Fixes (2) and (3) **are** substantively live (FAQPage ×1 with 7
  Question entities, MedicalWebPage ×2, speakable = 0 on all four).
- **Speakable: overstated.** Google's Speakable feature is limited to English-language news publishers,
  so it will not yield a Google rich result here. But the flag's stated purpose was *"so AI engines
  attribute the answer to Mindtalk"* — ChatGPT/Perplexity crawlers, not Google News eligibility. Correct
  wording: **ineligible for Google's feature; unknown for LLM citation; low-value, deprioritise** — not
  "not viable."
- **The core error:** I disposed of the *remedies* and declared the *problem* gone. The flag's actual
  subject is **16 pages at pos 7–19 losing 20–85% of Day-21 impressions** (c-ssrs 1,802→244, obq-44
  1,154→292, ace-test 1,773→103). I verified **none** of it. RULE 1 says an impressions claim verifies
  in GSC; I ran no GSC pull. I also applied the wrong registry row — *"Schema missing → curl → present =
  FALSE POSITIVE"* does not govern an AIO-displacement flag that merely *proposes* schema as one remedy.
- Sample not census: 4 of 16 pages. And `c-ssrs` is a **suicide-risk instrument** — reducing Kushal's
  visibility into it must never happen silently.

**Re-scoped ask:** stop asking Kushal to approve work that is already done; **run a GSC pull across the
16 pages to confirm the impression loss is real before proposing any remedy.**

#### C2. `psychology-of-love-brief.md` re-diagnosis — **WITHDRAWN. Strategist's diagnosis reinstated.**

I tiered the brief `C` and rewrote its root cause, claiming the exact `psychology of love` family had
**0 queries / 0 impressions / 0 clicks** and that the Strategist's remedy therefore chased a keyword
with zero demand. **VETOED — and the file says the opposite.**

`scripts/gsc-pull.py` line 96 sets `"rowLimit": 50` and lines 103–104 compute window totals as **sums
over the returned rows only**. Both windows sit at exactly 50 rows, ordered clicks-desc then
alphabetical. The current window's alphabetical tail terminates at **`love and bonding`** — so
`psychology of love`, sorting at "p", **could not appear regardless of its true volume.** My flagship
finding was a row-cap artifact, not a measurement.

Worse, the counter-evidence was in the same file. `previous_window` (which did reach "p"):

> `psychology of love` — **40 impressions · 2 clicks · position 29.6 · CTR 5.0%**

That was **100% of the page's clicks that week**, at a healthy 5% CTR from page 3. The primary keyword
is the page's only proven click source. It dropped out of a 50-row report that `love` flooded — which is
closer to *supporting* the Strategist than refuting them.

**Also out of scope** *(Verifier CORRECTION, accepted)*: the registry authorises exactly two moves on a
brief — classify it, or archive it — plus the `Broken link / 404` class. Re-diagnosing root cause and
superseding remedies is **judgement**, which RULE 2 assigns to escalation. I overstepped.

**What survives and stands:**

| Item | Status |
|---|---|
| `intent_tier: C` set (was the queue's only untiered brief) | ✅ registry-authorised auto-fix |
| Brief's CTA target `/treatments/relationship-counselling` **404s** → retargeted `/illnesses/relationship-issues` (200) | ✅ registry `Broken link / 404` |
| Mandatory Tier A link `/doctors/psychologists-in-bangalore` (200) — page's only booking path | ✅ retained |
| `love` = 303 impr at pos **1.4**, 0.33% CTR + entity junk (Jamie Ford novel, *Love Story 2050*, `=love`, `l.o.v.e.`) | ✅ real rows, real dilution |
| Clicks 2 → 1 = noise-level, not a 50% collapse worth a sprint | ✅ clicks are cap-immune |
| Success metric replaced: **clicks on primary KW + onward Tier A clicks**, NOT impressions/CTR/position | ✅ impression base is unmeasurable |
| Keyword-density 8–12× and H2 renames | ⤴️ **restored** — my "do not do this" was withdrawn |

**§1 stated honestly, not dressed up** *(Verifier CORRECTION)*: I made the ship conditional on *adding*
a Tier A link and called that §1 compliance. §1 requires a **measured** click path; adding a link
creates an unmeasured one, so limb (b) still fails the day after ship. Read literally, §1 says
*"Otherwise: reject and log"* → archive. **Shipping is a recorded deviation from §1 and is Kushal's
call.** The brief is **ON HOLD**.

---

### D. AUTO-FIXED — 4

| # | Item | Before → After |
|---|---|---|
| D1 | Untiered brief in queue (registry auto-fix) | `psychology-of-love-brief.md` had no `intent_tier` → classified **C**. Queue now 57/57 tiered. |
| D2 | Broken link target in a brief | `/treatments/relationship-counselling` **404** → `/illnesses/relationship-issues` **200**. All 5 link targets in the brief re-verified live. |
| D3 | **WATCH ID collision** | **W40 was assigned twice** — `/blogs/psychology-of-love` (opened 08-21, Day-21 09-11) *and* the 5-blog T9 cohort (opened 08-11, Day-21 09-01 / Day-42 09-22). Two cohorts, one ID, different eval dates would have corrupted both verdicts. Renumbered psychology-of-love → **W42** (W41 already taken by the 08-18 cohort). |
| D4 | Stale success metric on that watch | W42's row still targeted *"pos 9 → pos≤5, +30 clicks/wk"* and a CTA to the 404 URL. Replaced with the clicks-based metric and corrected target. |

**Brief-queue standing job:** **11 raw / 8 effective `/blogs/` shippable.** Floor is 6. **Trigger did not
fire; no refill run — deliberately.** Spec Step 4: *"count shippable `/blogs/` briefs. **If < 6**, run
the brief-starvation auto-fix"*; the registry's *"Refill to ≥12"* is the target *inside* that auto-fix,
not a standing floor. At 8 ≥ 6 it never activates. Verifier **UPHELD** this, and independently confirmed
the substantive argument: T9 is cap-blocked with 49 candidates until 08-25, so briefs written today
could not ship a page. Adding inventory to a consumption-blocked pipeline would have been motion, not
progress. **Weekly cap untouched. 0 pages shipped. `src/**` untouched. Nothing deleted.**

---

### E. ROUTED TO META-LEARNER / STRATEGIST-VERIFIER — not Kushal's — 5

| # | Item |
|---|---|
| E1 | **`gsc-pull.py` `rowLimit: 50` is a systemic measurement defect.** Window totals are sums over returned rows only. **252 of 746 window objects (33.8%) across `gsc-data/` are at the cap** — so `impressions`, `avg_position` and every derived CTR/impressions-delta signal are truncated samples of variable size. This is what produced both the withdrawn "0 impressions" finding *and* the original `PSYCHOLOGY-OF-LOVE-CTR-DROP-01` signal. `scripts/*.py` is outside T20's write scope. **Highest-value item in this run.** |
| E2 | **`new-content-discovery.py --all` times out** — 3rd confirmed recurrence (D5 of the 08-21 run). Ran to a 300s timeout today without completing; `new-content-opportunities.json` mtime still 2026-08-17 (5 days stale). Needs a chunked/resumable mode. Low urgency while the queue is consumption-blocked. |
| E3 | **The `+353%` impressions figure** in `WATCH.md` / `BACKLOG.md` / the 08-21 log traces to the 08-21 GSC pull (94→426); today's pull gives 96→371 = +286%. Both are 50-row-capped sums, so **neither is a real impressions delta.** Not an arithmetic error — a provenance/reliability one. |
| E4 | **`brain/.git` lock files cannot be cleared from the sandbox.** 9 `.lock` files (incl. accumulated `*.gone.2.lock` cruft from prior failed clearing attempts); both `os.rename()` and `os.unlink()` return EPERM on the FUSE mount. Note the previously-recorded `os.rename()` workaround **no longer works**. `git status` still functions, so impact is limited. Already in `pending-human-actions`; **not re-escalated** — Kushal has it. |
| E5 | **AP8 verified working, no action.** I checked whether the 9 daily quarantines are the *same* URLs recurring (which would mean AP8 is masking a real problem). Across 8 days of `data-quality-suspect-*` logs the sets are near-disjoint and rotate randomly. Genuine API noise. AP8 is correctly designed. |

---

### F. TODAY'S SENSOR FLAGS — verified, no action

- **T1 rank sweep (08-21):** 289 keywords, **0 new flags**, 0 CRITICAL, 0 MAJOR. 9 AP8 quarantines (see E5).
- **T2 GSC validation:** 3 flags → 2 removed as NOISE/IMPROVING, 1 CONFIRMED (`psychology-of-love`). `confirmed-drops.json` is `{}`. Working as designed.
- **T4 observation monitor:** 13 URLs in pipeline, 0 checks due today, 0 alerts. Next: 4 Day-21 midpoints on 08-25.
- **T9 auto-ship:** correctly SKIPPED on the `/blogs/` cluster cap (7/6). Not a flag.
- **Stub-pilot:** 3rd consecutive workless run. The 08-14 verdict is the standing flag; **not re-pinged** — weekly re-pings on an 8-day-old decision are noise.
- **Schema (`SCHEMA-MEDICAL-TYPES-01`, PR #23):** independently re-confirmed live. `/illnesses/depression` and `/illnesses/anxiety` both emit `FAQPage` + `MedicalCondition` + `Article`; `/treatments/narrative-therapy` emits `FAQPage` + `MedicalTherapy`. The W36/W37 root-cause hypothesis is genuinely addressed ahead of the 09-11 finals.
- **`T17-7-AEO-DOCTORS-SPRINT-01`:** re-confirmed real — live `/doctors` emits only `Organization`, `SearchAction`, `WebSite`; **FAQPage count 0**. Escalated 4× already; **not re-pinged today.**

---

### RUN SUMMARY

| | |
|---|---|
| Flags collected | 18 (BACKLOG open rows + today's sensor logs + ops-health carry-overs) |
| **False positives closed** | **0** — both intended closures were downgraded instead after Verifier review |
| **Downgraded (real, but mis-stated)** | **2** — `DEAD-CLICKS-W34` CRITICAL→P2 (ad-spend block withdrawn) · `T5-REFILL-16` CRITICAL→P3 (16-day false premise) |
| **My own claims vetoed and withdrawn** | **2** — `ASSESSMENT-AIO` closure · `psychology-of-love` re-diagnosis |
| **Auto-fixed** | **4** — brief tiered · 404 link target · W40→W42 ID collision · stale watch metric |
| Routed to Meta-Learner | 5 (incl. the `gsc-pull.py` 50-row cap — the run's most valuable finding) |
| Escalated to Kushal | **3** — §1 Tier C deviation call · `ASSESSMENT-AIO` re-scoped (needs GSC pull) · `DEAD-CLICKS` P2 with ad-spend block withdrawn |
| Brief queue | 11 raw / **8 effective** `/blogs/` + **43 Tier A `/doctors/`**, all 404-verified · floor 6 · **refill trigger did not fire** |
| Pages shipped | 0 · `src/**` untouched · nothing deleted |
| Verifier sub-agent | **2 VETOs + 3 CORRECTIONS + 1 UPHELD — approval rate 1/5. All honoured.** |

**Net.** Two multi-week escalations were defused rather than deleted: a CRITICAL that would have blocked
ad spend on a scope artifact, and a 16-day-old "the queue is empty" that was wrong every single day.
Both were downgraded, not closed, because parts of each are genuinely real — and saying so is the
difference between filtering noise and manufacturing it.

**The structural finding is that the engine is not brief-starved, it is brief-constipated:** 54
verified-shippable briefs, 43 of them Tier A, against a T9 run that skipped with 49 candidates queued
behind a cluster cap. Sixteen days of "run T5 NOW" escalations pointed at the wrong end of the pipe.

**And the discipline note.** I got two things materially wrong — closing the AIO flag on evidence that
turned out to be a boilerplate CTA, and declaring a keyword dead when it was merely past a row cap that
I had not noticed. Both were caught in-run and reversed before delivery. The row cap is the more serious
of the two: it means a third of this system's GSC-derived signals, including the very flag I was
investigating, are computed on truncated samples. I would not have found it without being forced to
defend a wrong claim.

---

## 2026-08-23 (Sunday) — RUN 4

**Inputs read:** `brain/BACKLOG.md` (T10 stamp 08-23 20:17), `brain/BRAIN.md` (T12 stamp 08-23 18:00),
`brain/WATCH.md`, `brain/INTENT-PRIORITY.md`, `brain/VERIFIER.md`, `config.json`, `tracking-db.json`,
`logs/{observation-2026-08-23, ops-health-2026-08-22, auto-ship-2026-08-21, rank-summary-2026-08-21,
gsc-validation-2026-08-21}`, `brain/memory/decisions/2026-08-23.md`, all 57 `briefs/*.md`,
`gsc-data/` (179 files), the live site (16 curl checks), **GSC (63 page-filtered queries)**,
**PageSpeed Insights (9 runs)**, and the `mindtalk` product repo (read-only).

**Verifier sub-agent:** spawned adversarially against this run's own claims. Returned
**3 UPHELD / 5 CORRECTION / 2 VETO — approval rate 3 of 10. All honoured.**
**Both VETOs were mine and both conclusions are withdrawn below.** The corrections are recorded as
first-class content, not footnotes.

---

### A. THE RUN'S PRINCIPAL FINDING — a false zero that produced five failing verdicts

T12 ran at 6 PM today and wrote into BRAIN.md: *"5 watches evaluated … **All 5 verdict 🔴 STALLED** …
GSC Aug 13-20 window: **all 5 show 0 impressions** … PRIMARY CONFOUND: August Core Update causing
documented broad SERP volatility."*

**The zeros are an input-format artifact.** `scripts/gsc-pull.py:80` builds the page filter as
`full_url = f"{PAGE_URL_BASE}{url_path}"` with `PAGE_URL_BASE = "https://www.mindtalk.in"`. T12 passed
a **full URL** on `--url` instead of a path, so the filter became
`https://www.mindtalk.inhttps://mindtalk.in/blogs/...` and matched **zero rows**. Three independent
confirmations: (1) the five output files are named `gsc-data/https:__mindtalk.in_blogs_*.json` — the
`url_path.replace("/","_")` fingerprint of a full URL; (2) they are ~550 bytes with `keywords: []`
while normal pulls are 13–18 KB; (3) **40 other pages pulled path-form in the same session at 18:10
returned normal data**, which isolates the cause to the input, not to GSC or to the pages.

**Ground truth — page-dimension, filter `https://www.mindtalk.in` + path, window 2026-08-13→08-20:**

| Watch | Page | T12 read | Truth (impr / clicks / pos) | Primary query |
|---|---|---:|---|---|
| W30 | `/blogs/how-to-deal-with-relationship-stress` | 0 | **78 / 0 / 8.6** | `relationship stress` pos 7.2 |
| W31 | `/blogs/how-to-fix-your-sleep-schedule-quickly` | 0 | **1,608 / 2 / 9.6** | primary KW **pos 1.8** (183 impr) |
| W32 | `/blogs/mental-exhaustion-symptoms-causes` | 0 | **376 / 0 / 17.3** | `mental exhaustion` pos 6.3 |
| W33 | `/blogs/what-is-eft-tapping-guide` | 0 | **467 / 2 / 8.1** | `eft tapping` pos 5.4 |
| W39 | `/blogs/yoga-for-anxiety` | 0 | **2,055 / 16 / 8.8** | `yoga for anxiety` |
| | **TOTAL** | **0** | **4,584 impressions / 20 clicks** | **4 of 5 on page 1** |

*(Verifier CORRECTION ×3, all accepted:* my first ground-truth figures were **1,836 impr / 5 clicks** —
2.5× low, because I summed `dimensions:["query"]` rows, which GSC privacy-filters. **That is the same
error family I was indicting.** All figures above are now page-dimension. My "3 of 5 on page 1" was
also understated — it is 4 of 5. And T12 issued **Day-21/Day-14 INTERIM** verdicts with the watch left
OPEN, not closures; my proposed remedy of "close and hand back" was backwards — the correct action is
to **correct them in place**, which is what was done.*)

**Action:** the 5 interim verdicts are marked measurement-invalid in `WATCH.md` (a correction block at
the head of the file plus an annotation appended to each of the 5 rows) and in `BRAIN.md`. **No watch
was closed and no replacement 🟢/🟡 verdict was issued — that is T12's rubric, not mine.** T12 must
re-issue on corrected data. The 5 corrupt data files are annotated in place with
`_AUTHORITATIVE_page_dimension_2026_08_23` (page-dim) and `_query_dim_floor_2026_08_23`.

---

### B. THE SAME DEFECT CLASS, ONE ORDER OF MAGNITUDE WIDER

Chasing the mechanism turned up its larger sibling. `scripts/day42-batch-gsc.py:59` sets
**`rowLimit: 25`**, and window totals are sums over the returned rows only.

**Reproduced end-to-end, not inferred** *(Verifier CORRECTION — upgraded my "plausibly manufactured" to
demonstrated):*

| Page | Window | At `rowLimit: 25` | Uncapped | Recorded in BACKLOG |
|---|---|---:|---:|---:|
| `/assessments/ace-test` | Aug 11–18 | **101 impr / pos 20.2** | 1,260 / pos 16.1 | **103 / pos 20.3** |
| `/assessments/c-ssrs` | Aug 11–18 | **244 impr** | 530 | **244** |

The mechanism *(Verifier addition):* **GSC returns rows sorted by clicks descending, ties broken
alphabetically** — not by impressions. On a 1-click page the cap returns that one row plus 24
alphabetically-first zero-click rows (`6 ace score`, `a c e test`, …). Truncation is therefore a
**near-random sample, not a top-N sample**, and severity scales with (rows − limit) — which is why a
152-row page collapses ~12×.

**Consequence:** the entire **2026-08-21 assessment Day-42 batch (77 pages: 45 RESOLVED / 16
SCHEMA_OPTIMIZATION_NEEDED / 16 NEEDS_REFRESH)** ran on this script. All 77 verdicts are suspect, and
the derived **"58.4% assessment establishment rate vs 80% for blogs"** in BRAIN.md is computed on
truncated data. Both are now **quarantined pending an uncapped re-pull**, not deleted.

---

### C. FALSE POSITIVES CLOSED (Rule 1) — 3

| # | Flag | Evidence |
|---|---|---|
| C1 | **`ACES-TEST-INVESTIGATE-01`** | Claimed "D21 1,773 impr/wk → D42 103 = −94.2%". Truth: D21 window **393 / 1 click**, current **1,740 / 10 clicks** = **+343%**. Invalid for two independent reasons: the D42 figure is the `rowLimit:25` artifact above, **and** *(Verifier addition)* the "1,773 impr/**wk**" baseline is a **19-day cumulative** — `tracking-db.json` `week_3_check_notes`: *"GSC 07-10->07-28: impr=1773"* ≈ 653/wk. No window yields −94%. |
| C2 | **`ASSESSMENT-AIO-SCHEMA-AUDIT-01`** | The 08-22 run withdrew its own closure and re-scoped the ask to *"run a GSC pull across the 16 pages before proposing any remedy."* **Done — and the premise fails.** Cohort **1,367 → 1,835 vs the Day-21 window (+34%)** and **1,819 → 1,835 week-over-week (+0.9%)**; the claimed "20–85% loss" appears under neither. `c-ssrs` **+82% / +0.6%**, pos **14.7 → 9.3**, **11 clicks**; `obq-44` **+32–51%**, **13 clicks**. Position improved **11/16**; **13/16** flat-or-up. |
| C3 | **`T9-SLEEP-STAGES-AP9`** | `briefs/archive/NEW-the-4-stages-of-sleep-explained-brief.md`, mtime **2026-07-24 17:11** — 30 days. Still listed "STILL OPEN" in `ops-health-2026-08-22.log` Part A.5. |

*(Verifier CORRECTIONS on C2/C3, accepted:* my C2 "+34%" compared against the **Day-21** window while
the like-for-like prior week gives **+0.9%** — both are stated above rather than picking the flattering
one. The cohort has **17** members; I silently dropped `/treatments/play-therapy`. And "the 5 decliners
are all tiny volumes" was **wrong**: `/assessments/epds` fell **687→413 = −274 impressions**, the
cohort's largest absolute mover — I cited 8→6 and 27→20. Its series (282→330→687→413) reads as a spike
normalising, but I had not checked. On C3, "FALSE POSITIVE" overstates: T9 archived the file **in the
same minute it rejected it** — housekeeping, not Kushal choosing Option A. Correct framing: close as
**Option A executed by default**, strike the row's false *"consuming a brief-runway slot"* rationale
(it is not among the 57 active briefs), and re-file the Option-B reframe as an ordinary T5 idea rather
than a human gate.*)

**Safety note on C2:** `c-ssrs` is a suicide-risk instrument. Closing is the conservative direction —
*executing* the flag would have meant AIO/schema-optimising that page while it ranks pos 9.3 with 11
clicks and improving. Reducing Kushal's visibility into it was checked for explicitly and does not occur.

---

### D. MY OWN CLAIMS VETOED AND WITHDRAWN — 2 (both CWV)

#### D1. `CWV-ASSESSMENTS-CRITICAL-01` — **my proposed reopen is WITHDRAWN. The 08-21 closure stands.**

I measured `/assessments` at perf 66 / LCP 10.6s and moved to reopen the 08-21 false-positive closure
(which had rested on a single reading of perf 89 / LCP 2,401ms). **VETOED.** Five further PSI runs
today returned **perf 81–98, LCP 2.18–2.33s**. My reading was the outlier.

**My own evidence refuted me and I did not notice:** an LCP of 10.6s with **all network activity
complete at 3.1s** is not a slow page, it is an **invalid measurement**. The correct inference is
*discard the reading* — not *reopen a flag in order to explain it*. That is precisely the error I spent
this run indicting T12 for, committed in the same run.

Also **dropping the `largest-contentful-paint-element = 0 items` fingerprint entirely**: it returns 0
items on the homepage at LCP 2.78s as well, so it carries no diagnostic signal and should never have
been cited as one — including in the 08-21 entry above.

#### D2. `CWV-DOCTORS-PAGE-01` — **escalation WITHDRAWN. Probable-FIXED.**

I was about to escalate *"verified NOT fixed, LCP 10.7s, dev deadline 08-25"* to the dev team **three
days before the August Core Update**. Five PSI runs today: **LCP 2.40s, perf 81–92**, against the
2026-08-12 flag state of **8.95s / perf 56**. The evidence points to the dev fix having **landed**.

Correct action: report **probable-fixed**, ask dev to confirm what shipped and when, keep **08-25 as a
confirmation checkpoint rather than an escalation**. A false CWV alarm three days before a core update
spends credibility the genuinely open items need.

**What survives from D1/D2 as new items:** `T14-PSI-SINGLE-SAMPLE-01` (every CWV CRITICAL in this
system is raised from one lab sample; one URL read 10.6s and 2.3s ten minutes apart today;
`reports/technical-health-2026-07-15.md` shows 7 of 8 pages simultaneously at 9–11s and all
simultaneously "recovered" by 07-29 — seven regressions and seven fixes in a fortnight is not a
physical story) and `CRUX-PAGE-FIELD-DATA-GAP-01` (P3 — `/assessments` and
`/doctors/psychiatrists-in-bangalore` both return `origin_fallback: True`, so the "field data is FAST"
argument used on 08-21 is valid for the homepage only).

---

### E. AUTO-FIXED — 5

| # | Item | Before → After |
|---|---|---|
| E1 | **20-run MISMATCH-SKIP churn** — T10 has asked Kushal to delete 2 proposal files on **20 consecutive runs** | Verified genuinely superseded: `t16-read-pending-human-actions` asks for `### Part A.5`, already live at `task16…md:90`; `t5-floor-miss-brain-flag` asks for the BRAIN.md floor-miss write, already live at `task5…md:141`. Both applied 2026-08-10 via the anchor-fix versions. **FUSE denies `unlink()` on this mount**, so both are **tombstoned in place** with a `⛔ SUPERSEDED — SKIP ON SIGHT` header + `**Status:** superseded`, and copied to `brain/applied-changes/superseded/`. **Nothing deleted; the churn ends.** |
| E2 | 5 corrupt GSC data files carrying false zeros | Annotated in place with `_INVALID`, the exact mechanism, `_AUTHORITATIVE_page_dimension_2026_08_23` and `_query_dim_floor_2026_08_23`. Copies in `gsc-data/archive-invalid-2026-08-23/`. |
| E3 | **W39 Day-42 date contradiction** *(Verifier finding — I had missed it)* | `WATCH.md` says **2026-09-16**; the 08-20 / 08-22 / 08-23 Strategist stamps call **2026-08-26** the "Day-42 final". Arithmetic: ship 2026-08-05 + 42d = **2026-09-16**; 08-26 is the **Day-21 midpoint**. WATCH.md is correct; noted in WATCH.md and BRAIN.md. |
| E4 | Stale interim verdicts in `WATCH.md` | Correction block at head of file + per-row annotation on all 5 rows, with page-dim ground truth. |
| E5 | `BRAIN.md` carrying an unsupported "concerning pattern" | Corrected; 58.4% establishment rate quarantined inline. |

**Brief-queue standing job:** 57 briefs, **0 untiered**. **11 `/blogs/` briefs with an `intent_tier`,
all 11 curl-verified HTTP 404**; 3 are NEEDS_HUMAN → **8 effective**. Floor is 6 → **8 ≥ 6, the refill
trigger did not fire.** Plus **43 Tier A `/doctors/` briefs**, all 404. Weekly cap 7/20 untouched.
**0 pages shipped. `src/**` untouched. `scripts/*.py` untouched. Nothing deleted.**

---

### F. ESCALATED TO KUSHAL — 3 (each with the fix pre-written)

| # | Item | The ask |
|---|---|---|
| F1 | **`GSC-MEASUREMENT-INTEGRITY-01`** | Three defects, one class, all in `scripts/*.py` which T20 may not edit: (1) `gsc-pull.py` accepts a full URL on `--url` and silently emits a garbage filter — **no guard**; (2) `gsc-pull.py:96` `rowLimit: 50`; (3) `day42-batch-gsc.py:59` `rowLimit: 25`. Plus: window totals sum **query-dimension** rows, which GSC privacy-filters (1,836 vs a page-dim truth of 4,584 on the same 5 pages). **Fix ≈3 lines + pagination:** `if url_path.startswith("http"): raise ValueError(...)`; `rowLimit: 1000` with `startRow` pagination; use `dimensions:["page"]` for page totals. This one change prevents today's five false verdicts, the fake ace-test −94%, the fake c-ssrs collapse, and the suspect 77-page batch. |
| F2 | **`T9-DOCTORS-QUEUE-MISLABEL-01`** | `auto-ship-2026-08-21.txt` says *"Candidates in queue: 49 /blogs/ pages … All candidates: /blogs/ → blocked by cluster cap"* and lists `/blogs/online-psychiatry` at #2. That brief reads `Suggested URL: /doctors/online-psychiatry`, `Content Type: DOCTOR_LISTING`, `Suggested File: src/content/doctors-listings/online-psychiatry.mdx`. **Only 11 of 49 are `/blogs/`; 43 are `/doctors/` Tier A and are not subject to the `/blogs/` cap.** T9 cap-blocked pages it was free to ship. Concrete root cause of `DOCTOR-EXECUTOR-VELOCITY-01`. *(Verifier addendum — this also falsifies my own closing line yesterday and today that "briefs written now could not ship a page": true for `/blogs/`, false for `/doctors/`.)* |
| F3 | **`MINDTALK-REPO-RESET-CMD-01`** | `ops-health-2026-08-22.log` instructs `git reset --hard origin/main`. Real state: HEAD on `feat/exec-refresh-doctors-bangalore-20260821`, **134 behind / 1 ahead**, **10 modified tracked files**, **80 untracked entries (128 files) colliding with origin/main**. That command *on the feature branch* does not fix an orphaned commit — it **creates** one; and `git checkout main` would abort on the collisions. *(Verifier CORRECTION: I checked 3 of the 10 files and generalised. All 10 checked: 8 are byte-identical to origin/main, but `what-is-rtms-treatment.mdx` differs by 13 lines and `life-coach-therapy.mdx` **deletes a 5-Q&A `faqs:` block** origin/main has — both local versions are older/worse, so nothing of value is lost, **but by luck, not by the check I ran**.)* Safe sequence supplied in the digest. T20 did not touch the repo. |

**Not re-escalated (verified real, already with Kushal, no new information):** `T17-7-AEO-DOCTORS-SPRINT-01`
(4×), `psychology-of-love` §1 Tier C call, `DEAD-CLICKS-W34` (P2), `PERSONALITY-DISORDER-YMYL-SIGNOFF-01`,
`STUB-PILOT-CONVERSION-VERDICT-01`, `W28-alzheimers` option A/B, and `brain/.git` lock files
(**re-tested today: 10 `.lock` files, all `unlink()` → EPERM** — genuinely blocked, 3rd day, brain
backups still not committing).

---

### G. TODAY'S SENSOR FLAGS — verified, no action

- **T4 observation monitor (08-23):** 13 URLs, 0 checks due, **0 alerts**. Next: 4 Day-21 midpoints 08-25.
- **T1 rank (08-21 carry):** 0 CRITICAL, 0 MAJOR, 9 AP8 quarantines. ALGO_WATCH inactive.
- **T2 GSC:** 1 confirmed drop (`psychology-of-love`), already ON HOLD pending Kushal's §1 call.
- **T9 auto-ship:** SKIPPED on the `/blogs/` cluster cap (7/6) — correct for `/blogs/`, **wrong for the 43 `/doctors/` briefs** (F2).
- **T10 (8 PM):** 3 Meta-Learner proposals applied and Verifier-approved; 3 future proposals correctly deferred to 08-30.
- **August Core Update 2026-08-26 (3 days):** conservative posture respected — 0 content shipped, 0 briefs written, 0 sprints created.

---

### RUN SUMMARY

| | |
|---|---|
| Flags collected | 21 (BACKLOG open rows + today's T10/T12 output + ops-health carry-overs) |
| **False positives closed** | **3** — `ACES-TEST-INVESTIGATE-01` · `ASSESSMENT-AIO-SCHEMA-AUDIT-01` · `T9-SLEEP-STAGES-AP9` |
| **Verdicts invalidated** | **5** — today's T12 interim 🔴s (W30/W31/W32/W33/W39); **4,584 impressions / 20 clicks recorded as zero** |
| **Quarantined** | **77** — the whole 08-21 assessment Day-42 batch + the derived 58.4% establishment rate |
| **Re-scoped** | **1** — `ASSESSMENT-NEEDS-REFRESH-BATCH-01`: 2 of its top-3 targets are growing; 6/16 have 0 impressions and 15/16 have 0 clicks → reconstitute, don't re-rank |
| **My own claims vetoed and withdrawn** | **2** — the `CWV-ASSESSMENTS` reopen and the `CWV-DOCTORS` dev escalation. Both CWV items resolve in the *good* direction. |
| **Auto-fixed** | **5** — 20-run proposal churn ended (tombstoned, not deleted) · 5 corrupt GSC files annotated · W39 date · WATCH.md corrections · BRAIN.md quarantine |
| **Escalated to Kushal** | **3** — `GSC-MEASUREMENT-INTEGRITY-01` · `T9-DOCTORS-QUEUE-MISLABEL-01` · `MINDTALK-REPO-RESET-CMD-01` |
| **New items filed (not Kushal's)** | **2** — `T14-PSI-SINGLE-SAMPLE-01` · `CRUX-PAGE-FIELD-DATA-GAP-01` |
| Brief queue | 11 raw / **8 effective** `/blogs/` (floor 6, **no refill**) + 43 Tier A `/doctors/` · all 404-verified |
| Pages shipped | **0** · `src/**` untouched · `scripts/*.py` untouched · nothing deleted |
| Verifier sub-agent | **3 UPHELD / 5 CORRECTION / 2 VETO — approval rate 3/10. All honoured.** |

**Net.** The engine spent today recording a broad pre-Core-Update stall that did not happen. Five pages
carrying **4,584 impressions and 20 clicks** — one of them ranking at **position 1.8** on its primary
keyword — were written down as zero and failed, and a Core Update was named as the cause. The same
defect class, at `rowLimit: 25`, had already manufactured a −94% "collapse" on a page that has since
grown **+343%**, and it underwrites all 77 verdicts in the 08-21 assessment batch. Three flags closed,
five verdicts invalidated, seventy-seven quarantined — from one three-line guard that nobody has written.

**And the discipline note.** I got the two CWV items wrong in the same run in which I made measurement
integrity the headline: I read a single outlier PSI sample and moved to reopen one flag and escalate
another to dev, three days before a core update. My own evidence — all network complete at 3.1s under a
claimed 10.6s LCP — said the reading was invalid, and I used it to argue the page needed explaining
instead of the measurement needing discarding. The Verifier caught both. I also computed my headline
ground truth by summing query-dimension rows, understating it 2.5× by exactly the privacy-filter
mechanism I was writing up. Getting the diagnosis right and the method wrong in the same document is
the failure mode worth naming, and it is why the adversarial pass is not optional.

---
---

# 🔧 T20 AUTO-REMEDIATION — 2026-08-24 (Monday, 8:45 PM IST)

**Run type:** scheduled · **Verifier sub-agent:** run, adversarial, 1 VETO + 3 CORRECTION + 2 UPHELD — all honoured
**Shipped:** 0 pages · `src/**` untouched · `scripts/*.py` untouched · nothing deleted (archive-only)

---

## A. FALSE POSITIVE CLOSED — 1 (today's #1 Strategist action)

### A1. `PTSD-TREATMENT-INVESTIGATE-01` — **CLOSED, NO ACTION**

T10 accepted this today as the week's top action, sourced from `reports/weekly-summary-2026-08-24.txt`:
*"PTSD Treatment −61.3% impressions WoW (307 vs 793), avg position worsening by +53 positions …
the most urgent drop this week … Audit and refresh the PTSD Treatment page immediately."*

**Ground truth (GSC, page dimension, rowLimit 1000 paginated):**

| Page | Aug 08–14 | Aug 15–21 | Position |
|---|---|---|---|
| `/illnesses/posttraumatic-stress-disorder-ptsd` | 179 impr | 137 impr | 13.2 → **11.0 improved** |
| `/blogs/ptsd-treatment-and-recovery` | 266 impr | 165 impr | 14.8 → **8.9 improved** |
| `/blogs/understanding-complex-ptsd` | 230 impr | 139 impr | 9.9 → **7.3 improved** |

**The baseline is one anomalous day.** Query `complex ptsd` carried 443 of the cluster's 794 baseline
impressions. Daily trace: **442 of those 443 landed on 2026-08-08 alone, at position 1.0**; the other
17 are spread across Aug 1–17 (max 9 on any other day). The spike lands on `/assessments/trauma-ptsd`
(483 that day against a ~55/day baseline).

**Clean-baseline test (Aug 01–07 vs Aug 15–21, excluding the anomaly day) — the cluster is UP:**
trauma-ptsd **+61.3%**, illnesses/ptsd **+93.0%**, ptsd-treatment-and-recovery **+16.2%**,
itq **+47.6%**, doctors/ptsd-specialists **+59.3%**, understanding-complex-ptsd −4.8%,
pcl-5 −12.5% (position improved 23.2 → 14.7). **No PTSD page lost position on any baseline.**

Refreshing these three pages — during a Spam Update rollout — would have spent a refresh slot on
pages that are all rising, to chase a single day's spike.

> **Verifier CORRECTION honoured (method).** My first pass hand-picked four PTSD URLs. Two of them
> (`/blogs/how-to-fix-ptsd-recovery-steps`, `/treatments/emdr-for-ptsd`) carry ~0 impressions and are
> not cluster constituents at all; the volume actually sits on `/assessments/trauma-ptsd` and
> `/assessments/itq`, **neither of which I checked**. The Verifier enumerated all 60 pages by
> query-filter and *did* find a materially-losing page I missed (trauma-ptsd, −28.5%, pos 5.1 → 9.0)
> — which then dissolved on the clean baseline, because the Aug-08 spike is on that same page.
> **The conclusion survived; my method did not. Enumerate cluster constituents by query-filter,
> never hand-pick URLs and generalise.** Same error class as 2026-08-23 D1/D2.

---

## B. VERIFIED REAL → DOWNGRADED, NOT ESCALATED — 1

### B1. `BANGALORE-COMMERCIAL-INVESTIGATE-01` — **watch, not `flag_for_human`**

Query drops verified exactly: `best psychiatrist in bangalore` 10.2 → 21.9; `psychologist in bangalore`
9.6 → 18.4; and the family is wider than T10 reported (`best psychologist in bangalore` 17.5 → 24.8,
`psychiatrists in bangalore` 7.0 → 54.6, `top psychiatrist in bangalore` 8.4 → 13.9).

**Not escalation-grade:** these are 5–36 impr/day tail queries whose weekly average is set by 2–3
outlier days (Aug 17–19) and which have **already recovered post-window** — `top psychiatrist in
bangalore` Aug 20/21/22 = 6.2 / 6.2 / 9.0; `best psychiatrist in bangalore` peaked at 50.6 on Aug 17,
*before* the update window, then 10.8 / 11.9 on Aug 20 / 22. Confound is the **August 2026 Spam
Update** (rolling from 08-18), **not** a Core Update — `logs/gsc-validation-2026-08-24.txt` records it
as not targeting health content, ALGO_WATCH not set.

> **Verifier CORRECTION honoured — two of my three evidentiary legs were falsified.**
> ⚠ **Do not cite page-level average position as evidence here.** I wrote that
> `/doctors/psychologists-in-bangalore` "improved 36.7 → 31.6". That improvement is entirely
> `therapist near me` (293 impr @ **pos 155.9** → 61 impr) leaving the weighted mean. Ex-that-query
> the page went **26.0 → 27.8, i.e. worsened**. This is a fresh instance of the exact defect
> `GSC-MEASUREMENT-INTEGRITY-01` was escalated for yesterday — committed by me, one day later.
> I also called 27 → 20 clicks "stable"; that is **−26%** on a Tier A booking page and is the one
> genuinely open signal. And the 08-21 refresh (`7163c679`) covers 1 of the 7 measured days, so it
> cannot explain the week and is not yet evidence of a fix.

**Watch recheck 2026-08-31, post-Spam-Update, on clicks + like-for-like query positions only.**

---

## C. AUTO-FIXED — 4

### C1. Brain backup — **4-night stall ended, and the standing escalation was wrong all along**

`brain/.git` had 15 lock files; `unlink()` → **EPERM on all 15**. T16 has been asking Kushal to
`rm -f` four of them since 2026-08-22, and `backup-history.md` shows the same failure recurring since
**2026-08-07** with four different one-off bypasses invented and then lost (Python rename, GitHub Data
API, /tmp clone, force-push).

**Root cause (observed, not assumed):** on this FUSE mount **git's own `unlink()` returns EPERM**, so
every git command that touches the index leaves its lock behind and breaks the *next* command.
`rm -f` therefore fixes exactly one operation before it re-breaks — **the escalation Kushal has been
receiving could never have worked.** The Verifier reproduced it independently: a read-only
`git status` emitted `unable to unlink '.git/index.lock': Operation not permitted`, created a fresh
lock, and `rm -f` on that new lock returned `Operation not permitted`.

`os.rename()` **is** permitted. Archiving each lock immediately before and after every git invocation
is durable. Result: **commit `8b3f5aa`, 33 files, pushed `da4099d..8b3f5aa`, tree clean, 0 unpushed.**
15 locks archived (not deleted) to `logs/brain-git-stale-locks-archive-2026-08-24/`.
Reference implementation: `outputs/t20_brain_backup.py`. Row appended to `backup-history.md`.

> **Verifier security scan of the full 2,981-line commit diff: CLEAN** — 0 hits for PATs, `ghp_`,
> `AIza`, `sk-`, `AKIA`, private keys, `client_secret`, `.pickle`. The three `x-access-token` hits are
> placeholder shell syntax in runbook prose. No credential was committed or pushed.
> **Verifier CORRECTION honoured:** 15 locks, not the 10 I first counted (5 more were generated by my
> own git invocations mid-run — which is itself the mechanism).

### C2. 14 Tier A doctor briefs had a wrong URL prefix

T5 wrote today's 14 doctor-listing briefs with `**Suggested URL:** /doctors-listings/<slug>`.
**`/doctors-listings/` is not a URL prefix on this site.** Verified: `/doctors/<slug>` → **200** on 4/4
live listing pages, `/doctors-listings/<slug>` → **404** on 2/2; `sitemap.xml` has **836 URLs, 0**
containing `doctors-listings` and **287** under `/doctors/` (168 of them `<specialty>-in-<city>`);
`config.json → tracked_specialty_listings` uses `doctors/<slug>` exclusively. `doctors-listings` is the
**content directory** (`src/content/doctors-listings/`), which is why the briefs' own `Suggested File`
was already correct — T5 conflated directory with route.

All 14 corrected (URL line only; `Suggested File` untouched and byte-identical, Verifier-diffed).
Originals archived to `briefs/archive/pre-t20-url-fix-2026-08-24/`. All 14 slugs also 404 at the
correct `/doctors/` path → genuinely new, no redundancy. Queue now: 0 malformed prefixes.
*(Verifier minor correction honoured: audit comment said `tracked_urls`; real key is
`tracked_specialty_listings` — corrected in all 14.)*

### C3. Two held briefs had no in-file hold — T9 would have shipped them

`conduct-disorder-in-children` and `gender-identity-disorder` have been carried as NEEDS_HUMAN since
the 2026-08-04 auto-ship run, **but neither brief file contained any marker** — the hold lived only in
session notes, so every T9 run since has been free to pick them up. Conflicts re-verified live today
(`/illnesses/conduct-disorder` 200, `/blogs/conduct-disorder-signs-causes-and-treatment` in sitemap,
`/illnesses/gender-identity-disorder` 200). Durable `⛔ NEEDS_HUMAN — DO NOT SHIP` blocks written into
both, each with Kushal's three options. *Found by the Verifier, not by me — I was carrying the count
of 3 from session notes without reading the files.*

### C4. `is-online-therapy-confidential` — prior Verifier VETO surfaced

Sat unflagged inside the shippable pool while carrying a 2026-08-18 VETO (FAQ schema duplication with
`/treatments/online-therapy`, plus a suicide-safety confidentiality-limits boundary). Named gate
written into the brief — not a blanket hold, but T9 must honour both constraints at ship time.

---

## D. CLAIM VETOED — 1 (mine)

### D1. `T5-REFILL-CRITICAL-17` — **my FALSE-POSITIVE closure is WITHDRAWN. The flag stays open.**

I moved to close this as false because T5 ran today and produced 20 real briefs (797–897 words each)
against a floor of 12. All of that is true. **But I tested a premise that I myself replaced two days
ago.** `BACKLOG.md` line 44 records my own 2026-08-22 re-scoping: the flag was downgraded but
explicitly **NOT closed**, because three named gaps were unwritten. Today's run closed **zero** of them:

- **Kochi briefs: 0** (`ls briefs/ | grep -i kochi` → empty)
- **Malayalam-Kerala variant: still absent** (only `-in-delhi`, `-in-mumbai`)
- **`/treatments/` briefs: 0**

Today's 14 Tier A picks came from `[STANDING_TIER_A_BACKLOG]`, a **static list that cannot surface
Kerala**, and discovery ran in **CACHED MODE** (live script timed out, cache 14 days old) — a caveat I
omitted. **P8 Kerala is a confirmed 4-week conversion signal**; closing this would have dropped it.

**Action for Strategist (not Kushal):** stop re-emitting the generic "pipeline starvation" headline —
it has now been false three times. Rename the row to **`T5-KERALA-TREATMENTS-GAP-01` (P3)** with those
three items as its literal acceptance criteria, and add Kochi + Malayalam-Kerala to the standing Tier A
backlog so the next T5 run can reach them.

---

## E. VERIFIED, NO ACTION

- **AP8 pos-100 quarantine (15 pages) — correct, no deindexation.** Spot-checked 4 on the page
  dimension: `/treatments/life-coach-therapy` 3,169 impr @ pos 12.0, `/blogs/alexithymia` 543 @ 11.8,
  `/blogs/managing-teen-depression` 48 @ 5.9, `/blogs/how-to-manage-bipolar-disorder-daily` 18 @ 21.8.
  DataForSEO said 100. AP8 is doing its job.
- **T2 GSC validation (08-24):** 0 confirmed drops, both MODERATEs correctly cleared.
- **T4 observation:** 0 alerts; 4 Day-21 midpoints fire tomorrow (08-25).
- **Weekly cap:** `max_new_content_per_week = 20`, T5 used 20/20. Respected. 0 shipped by T20.

---

## F. BRIEF-QUEUE STANDING JOB

**77 briefs, 0 untiered. 17 `/blogs/` briefs, all 17 curl-verified 404**; 3 blocked
(relationship-problems-and-solutions, conduct-disorder-in-children, gender-identity-disorder) →
**14 effective shippable vs a floor of 6 → refill did NOT fire.** Plus **57** Tier A `/doctors/` briefs.

The three files without a `Suggested URL:` field (`guide-to-reset-your-sleep-cycle`,
`psychologists-in-bangalore`, `psychology-of-love`) are older-format **REFRESH** briefs targeting live
pages — the "200 = shipped, archive it" rule correctly did **not** fire on them. A naive reading of that
registry row would have archived three valid refresh briefs.

> **Verifier CORRECTION honoured:** 17 `/blogs/` and 57 `/doctors/`, not the 19/58 I first reported —
> I had folded 2 of the 3 no-URL refresh briefs into the `/blogs/` denominator. `14 effective` was
> right by coincidence, not by arithmetic.

---

## G. ESCALATED TO KUSHAL — 3 (each with the fix pre-written)

| # | Item | The ask |
|---|---|---|
| G1 | **`T6-POSITION-UNITS-BUG-01`** | `reports/clusters-2026-08-24.csv` column `Position WoW` is a **percentage** — the PTSD row reads `9.8, 6.4, +53.1%`. The T6 narrative step renders it as *"avg position worsening by **+53 positions**"*. The real move is 6.4 → 9.8 = **3.4 positions**. This single mis-rendering is what turned a one-day artifact into "the most urgent drop this week / highest-priority content action". It will misfire on **every** future run. Fix: in the T6 narrative generator, format `Position WoW` as `Δ{prev:.1f}→{curr:.1f} ({pct:+.1f}%)`, never as a bare position count. Lives in `scripts/` — **T20 may not edit it.** |
| G2 | **`MINDTALK-REPO-STALE-CHECKOUT-02`** | `~/Documents/GitHub/mindtalk` local HEAD `7097922`; `git merge-base --is-ancestor 7163c67 HEAD` → **NO**. Flagged by T16 on 08-23, still open. Worse, the tree is dirty with **staged *and* unstaged** edits to the two files `7163c67` already shipped (`psychologists-in-bangalore.mdx`, `counsellors-in-bangalore.mdx`) plus `page.tsx`, `what-is-rtms-treatment.mdx`, `yoga-for-anxiety.mdx`. **This is the exact divergence that silently dropped commit `675dc26` on 2026-07-23.** T20 did not touch the repo. Safe sequence: stash the 5 modified files → `git fetch origin && git checkout main && git pull` → diff the stash against origin/main before restoring anything. |
| G3 | **`PENDING-HUMAN-ACTIONS-9-DAYS-STALE-01`** | `logs/pending-human-actions-2026-08-15.txt` — T16's Slack delivery **failed on 08-15** and was never retried. Five items have been invisible for **9 days**: `PERSONALITY-DISORDER-YMYL-SIGNOFF-01`, `STUB-PILOT-CONVERSION-VERDICT-01`, `T9-SLEEP-STAGES-AP9`, `W28-alzheimers` (A/B), `TRUST-ISSUES-HUMAN-01` (a/b/c). Re-delivered in today's digest. |

**Not re-escalated** (verified real, already with Kushal, no new information): `GSC-MEASUREMENT-INTEGRITY-01`,
`T9-DOCTORS-QUEUE-MISLABEL-01`, `T17-7-AEO-DOCTORS-SPRINT-01`, `psychology-of-love` §1 Tier C call,
`DEAD-CLICKS-W34` (P2), `ASSESSMENT-AIO-SCHEMA-AUDIT-01`.

---

## H. FILED, NOT KUSHAL'S — 3

- **`T6-CLUSTER-RANKING-BY-PERCENT-01`** — clusters are ranked by % change, which buried the week's
  actual largest loss: `what is a life coach` fell **10,183 → 1,866 impressions (−8,317)** at 0 clicks
  both windows. Site-wide impressions fell 35,734, so **this one zero-click Tier C query is 23% of the
  entire WoW decline**, against the PTSD cluster's −487. Disposition stays no-action (AP11 Tier C), but
  the "−8.9% impressions" headline should read as *one Tier C query normalising*, not a broad decline.
- **`T6-DAILY-OUTLIER-GUARD-01`** — `/assessments/trauma-ptsd` spiked **again** inside the current
  window (252 impr on 2026-08-21 vs ~55/day). Next week's PRE window contains it, so **the identical
  false drop will be manufactured on 2026-08-31**. Guard: drop any day >3× the trailing median before
  computing WoW.
- **`T16-FUSE-GIT-PATTERN-01`** — T16 should adopt the `clear_locks()`-around-every-git-call pattern
  (`outputs/t20_brain_backup.py`) instead of re-deriving a bypass each week. Task specs are the
  Meta-Learner's to edit, not T20's.

---

## I. OPEN, TRACKED, NOT ESCALATED

- `/blogs/psychology-of-love` fell **rank 2 → 9 (Δ+7, CTR_DROP)** and was removed from flagged-drops by
  T2's AP7 `BRIEF_CREATED` hygiene rule — on the strength of a brief written 08-21 that nothing
  confirms is queued to ship. **A page-1 → page-2 fall on a live page is now tracked only by the
  existence of a file.** Already ON HOLD pending Kushal's §1 Tier C call; noted so the hygiene rule
  is not mistaken for a resolution.

---

## RUN SUMMARY — 2026-08-24

| | |
|---|---|
| Flags collected | 14 (T10 top-5 + today's sensor logs + ops-health carry-overs) |
| **False positives closed** | **1** — `PTSD-TREATMENT-INVESTIGATE-01` (today's #1 action) |
| **Downgraded, not escalated** | **1** — `BANGALORE-COMMERCIAL-INVESTIGATE-01` → watch 08-31 |
| **Auto-fixed** | **4** — brain backup unblocked + pushed · 14 doctor-brief URLs · 2 missing NEEDS_HUMAN holds · 1 latent VETO surfaced |
| **My own claim vetoed** | **1** — the `T5-REFILL-CRITICAL-17` closure. Flag stays open, re-scoped. |
| **Escalated to Kushal** | **3** — `T6-POSITION-UNITS-BUG-01` · `MINDTALK-REPO-STALE-CHECKOUT-02` · `PENDING-HUMAN-ACTIONS-9-DAYS-STALE-01` |
| **Filed, not Kushal's** | **3** — cluster-ranking-by-percent · daily-outlier guard · T16 FUSE git pattern |
| Brief queue | **17 `/blogs/` (14 effective, floor 6 — no refill)** + 57 Tier A `/doctors/` · all 404-verified |
| Pages shipped | **0** · `src/**` untouched · `scripts/*.py` untouched · nothing deleted |
| Verifier sub-agent | **2 UPHELD / 3 CORRECTION / 1 VETO — all honoured** |

**Net.** The engine's #1 action for the week was a single day's impression spike read backwards. A
442-impression Monday on `/assessments/trauma-ptsd` inflated the PTSD baseline by 56%; when it fell out
of the comparison window the cluster showed −61%, and a **percentage** in the `Position WoW` column was
rendered as **positions**, turning a 3.4-position move into "+53 positions". Two artifacts stacked into
"the most urgent drop this week — refresh immediately", on three pages that are all *rising*. The units
bug (G1) will do this again next Monday, and the same page has already spiked again (H).

Separately, a four-day backup escalation resolved to an instruction that could not have worked: `rm -f`
on a mount where git's own `unlink()` is EPERM fixes exactly one git command. That flag had been going
to Kushal since 2026-08-07 in four different forms.

**And the discipline note, second day running.** I argued yesterday's measurement-integrity case and
then, one day later, cited a page-level average position that moved only because a position-156 query
left the weighted mean — the same defect, in the same direction, in my own evidence. I also hand-picked
four PTSD URLs and generalised from them without enumerating the cluster, carried a NEEDS_HUMAN count
of 3 from session notes without opening the files, and moved to close a flag against a premise I had
myself replaced two days earlier. The Verifier caught all four. Right conclusion, wrong method, three
runs in a row — the adversarial pass is not optional, and the recurring failure is **reasoning from
notes and samples instead of from the artefact**.

---

# 🔧 T20 AUTO-REMEDIATION — 2026-08-26 (Wednesday)

**Flags collected:** 9 (08-25 sensor logs + T16 ops-health carry-overs + standing job)
**Verifier sub-agent:** 1 UPHELD · 3 CORRECTION · 3 VETO · 5 unprompted findings — **all honoured**
**Net:** the engine's two loudest alarms today were both unreal, the queue that looked full was
structurally unshippable, and the six pages that went live yesterday carry ten dead booking links
that my own fix produced.

---

## A. THE HEADLINE — I broke six live pages two days ago and nobody caught it until now

**`DOCTORS-LISTINGS-DEAD-LINKS-01` — 10 dead Tier A booking CTAs in production.**

Every one of the 6 pages T9 shipped on 2026-08-25 carries `/doctors-listings/*` anchors.
**`/doctors-listings/` is not a URL prefix on this site.** All 10 return 404, live, right now
(re-verified by curl 2026-08-26). These are the booking CTAs — the conversion path
INTENT-PRIORITY.md exists to protect.

| Live page | dead anchors |
|---|---:|
| `/blogs/affordable-therapy-bangalore` | **4** — *all four body links* |
| `/blogs/family-counselling-bangalore` | 2 |
| `/blogs/best-psychiatrist-for-depression-bangalore` | 1 |
| `/blogs/cbt-therapy-online-india` | 1 |
| `/blogs/online-couples-therapy-india` | 1 — *the only body link* |
| `/blogs/online-marriage-counselling-india` | 1 |

**Scope is contained and measured:** I fetched all **297 live `/blogs/` pages**. Exactly these 6
are affected. No other live page carries the bad prefix.

**Root cause is mine.** The 2026-08-24 T20 run (§C2) found the same `/doctors-listings/` → `/doctors/`
confusion and fixed it — but only in the `**Suggested URL:**` field of 14 *doctor* briefs. It never
touched the **internal-link anchor lists inside the `/blogs/` briefs**, and T9 authored those anchors
verbatim into MDX one day later. I fixed the symptom I was looking at and left the one I wasn't.

**T20 cannot fix this** — it lives in `src/content/blogs/*.mdx` in the website repo. Escalated as E1
with the mapping pre-resolved (below). Three of the ten need a *different* target, not a prefix
rewrite, because no `/doctors/` equivalent exists at all — I checked each.

**Also still queued with the bad prefix:** `conduct-disorder-in-adults` (9 anchors),
`conduct-disorder-in-children` (10). Both are now held for other reasons, so nothing ships from them,
but they must be corrected before release.

---

## B. VERIFICATION — 2 of my 3 false-positive closures were WITHDRAWN

### B1. `/doctors/psychologists-in-bangalore` CRITICAL 13→100 — **my closure WITHDRAWN. Stays open.**

I moved to close this as a DataForSEO pos-100 artifact on the strength of the page improving:
impressions 721→776 (+7.6%), avg position 18.3→**16.9**.

**The Verifier reproduced the window and I was wrong — for the third consecutive run, by the same mechanism.**
On the **23 queries present in both windows**, the page went **14.59 → 16.26, i.e. worsened by 1.67**.
The apparent improvement is pure composition: 27 queries averaging position 36.4 and carrying 121
impressions simply **left** the window. Both windows are complete (listed impressions sum exactly to
the window totals — 721/721 and 776/776), so this is not a row-limit artifact.

Worse:
- The tracked keyword is **absent from both windows' full 50-query lists** in all three spellings.
  Absence is what a rank collapse looks like — it is not evidence against one.
- The GSC file's own `"signal"` field reads **`CTR_DROP`**, `clicks_delta_pct: -17.6`. I quoted the
  impressions and position out of that file and omitted its verdict.
- `flagged-drops.json` independently records `psychologists in bangalore` **17.7 → 25.3** and
  `psychologist in bangalore` **9.6 → 18.4** (flagged 08-24, source: weekly-report).
- T2 on 08-25 did **not** clear this as noise. It removed it under **AP7 hygiene** ("brief already
  exists"). On the same run T2 *did* close the separation-anxiety flag as `NOISE — GSC shows recovery`.
  It deliberately did not do that here.
- `BANGALORE-COMMERCIAL-INVESTIGATE-01` is an **open watch with recheck 2026-08-31 — which I opened
  myself two days ago.**

> `BACKLOG.md` line 484, written by me on 08-24: *"⚠ Do NOT cite page-level avg position here."*
> I then cited page-level average position here.

**Disposition: UNCONFIRMED — held on the existing 2026-08-31 watch.** Not escalated (already tracked),
not closed. The page is technically healthy (200, FAQPage + 10 Physician nodes, no noindex) — that was
true and is irrelevant.

### B2. `/treatments/narrative-therapy` URGENT midpoint +13.4 — **DOWNGRADED, not closed**

T4 raised `URGENT 🚨 … manual review required immediately` on a page with **6 impressions in the
window**. Four queries total. The +13.4 average is driven by one 2-impression query
(`narrative therapy india`, 7→59.5); excluding it the page **improved 9.43 → 4.25**.
GSC's own `signal` field says `NOISE`.

**Verifier correction honoured — twice:**
1. I cited the head query improving 4.4→**1.5** as affirmative evidence. That datapoint has
   **2 impressions**. Using a 2-impression reading as proof while dismissing a 2-impression reading as
   noise is the same error in both directions. The defensible statement is that **the entire page is
   below measurement threshold**, not that the head query improved.
2. "Closed as noise" is the wrong disposition. This is a T4 Day-21 midpoint (day 22 of 42) on the
   08-04 refresh; the Day-42 final is due **2026-09-15** and BACKLOG already schedules a
   post-Core-Update investigate on 09-05.

**Disposition: INSUFFICIENT DATA — defer to the Day-42 final (2026-09-15).** De-escalated from URGENT.
Not sent to Kushal.

### B3. T9's own note "`online-couples-therapy-india` has 2 internal links (min 3)" — **my rebuttal WITHDRAWN**

I claimed 24 internal links "inside `<main>`". **There is no `<main>` element on that page** — it uses
`<article>` + `div.prose`. Of the 24 T9-eligible hrefs in the document, **21 are footer chrome**,
byte-identical across five pages including two unrelated controls; the other 3 are auto-generated
"Related Insights" cards. **Inside the article prose: 0 T9-eligible internal links.** The single body
link is `/doctors-listings/couple-therapists-in-bangalore` → **404**.

T9 was not wrong. T9 was generous. And this is the same defect as §A.

---

## C. AUTO-FIXED — 9

### C1. The brief queue looked full and could ship nothing — `intent_tier` was in the wrong place

T9's ship gate is explicit: *"Every brief must carry `intent_tier: A|B|C` in **frontmatter**."*
**54 of 74 `NEW-*` briefs carried it only as a bold markdown header line** (`**intent_tier:** A`),
outside the YAML block. T9 therefore reported them as `INTENT_TIER MISSING` and skipped them — 52 on
the 08-25 run alone.

The partition is exact and proves the mechanism without reading a line of T9's code:

| `intent_tier` location | count | what T9 did |
|---|---:|---|
| inside the ```yaml block | **20** | = exactly {6 shipped} ∪ {14 skipped as DOCTOR_LISTING} |
| bold header line only | **54** | **all skipped** |
| absent | 0 | — |

**Fixed:** `intent_tier: X` inserted into the first YAML block of all 54, value unchanged (each was
already classified and justified in its own Intent Gate Record — this moved the value to where the gate
looks, it did not reclassify anything). 3 older-format REFRESH briefs have no YAML block and were
correctly skipped; T9 never opens them anyway (its Step 1 globs `NEW-*-brief.md`).
Originals archived to `briefs/archive/pre-t20-intent-tier-frontmatter-2026-08-26/`.
**All 54 diff-verified byte-identical apart from the 4-line insertion. 0 YAML parse failures across all 76 briefs.**

> **Verifier CORRECTIONS honoured — three of them.**
> **(i) The count is 54, not the 57 I first reported.** 57 only reaches that number by including three
> non-`NEW-` REFRESH briefs that T9 never globs.
> **(ii) T9's own run log is wrong, not mine.** `logs/auto-ship-2026-08-25.txt` reports 6 + 15 + 52 = **73**;
> ground truth is 6 + 14 + 54 = **74**. Both skip buckets are off and one candidate is unaccounted for.
> I spent effort reconciling against 52. Reconcile against the files, not that log. → filed as F1.
> **(iii) "The real count was 0, not 14" is overstated.** Of the 14 the 08-24 run claimed, **6 were
> genuinely shippable and T9 shipped all 6 the next day.** The true count on 08-24 was **6 — exactly at
> the floor**, not 14 and not 0. The 0 describes only today's post-ship residue.

### C2. Two prose-only holds that T9 cannot read — made literal

Promoting the tier made every held brief *visible* to T9 for the first time. Two carried holds written
only in prose:
- `relationship-problems-and-solutions` — NEEDS_HUMAN since 08-18 (AP9 overlap), recorded in a "T9 Skip
  Log" section at the foot of the file
- `is-online-therapy-confidential` — a binding 08-18 Verifier VETO in a blockquote

T9's Step-2 filter matches **five literal phrases** and neither file contained one. Without this fix my
own tier promotion would have caused T9 to ship two pages Kushal has explicitly not approved.
Machine-readable `⛔ DO NOT SHIP` blocks written into both, each carrying its release condition.
*(This is the second run in a row that the prose-only-hold class has bitten — see 08-24 §C3.)*

### C3. `conduct-disorder-in-adults` — held, not fixed

Looked like a mechanical near-miss (0 FAQs). It is not. Two blockers:
- **Path contradiction:** `Suggested URL`, `Suggested File` and `Content Type` all say `/blogs/`, while a
  pasted `SHIP PATTERN` block says ship to `/doctors-listings/`. T9 skipped it on 08-18 for exactly this.
- **Four unanswered `## Clinical Input Requested` questions**, on an outline that is DSM-5 diagnostic
  material (adult-onset specifier, CD-vs-ASPD differential, remission rates, treatment options).

**T20 does not clear clinical gates.** Held with the three options pre-written → E2.

### C4. `online-therapy-for-indians-in-usa` — repaired, and it was never shippable

Same `/doctors-listings/` SHIP PATTERN paste error — on a page about the **US diaspora**, where the
pasted text talks about `filterCity:"Mumbai"` and "never imply an in-person centre". Self-evidently a
template paste, contradicting three fields in the same file. Block marked **SUPERSEDED** (retained for
audit, not deleted). Also fixed: metaTitle **68→56 chars** (over T9's 65 limit — would have failed
forever), `reviewer: "Mindtalk Clinical Team"` → `sufia-nusrat` (T9 requires a pool slug),
placeholder FAQs/takeaways → real content, and a **dead anchor** `/treatments/online-counselling`
(**404**, curl-verified) → `/treatments/online-therapy` (200). T9-eligible links 2 → 4.

### C5. Dead-anchor sweep across the whole `/blogs/` brief queue

30 distinct internal-link anchors referenced by `/blogs/` briefs, all curl-checked. **5 dead.**
One was genuinely broken (C4). Four were forward references to briefs still queued — a real hazard,
because T9 would author a link to a 404. Fixed by giving 6 briefs an explicit **link-order note** with a
named, live fallback anchor rather than a fragile ship-ordering dependency.

> **Verifier CORRECTION honoured:** my first fallback for the Tamil and Telugu briefs was
> `/treatments/online-therapy` — **already in both link lists**. Executing the fallback would have left
> 2 unique live links, below T9's floor of 3. Changed to `/treatments/psychotherapy` (200) and a 4th
> link added to each.

### C6. `couple-therapy-cost-in-bangalore` — reviewer did not exist

`reviewer: ayushi-jain` is **not in `logs/reviewer-load-state.json`**. T9's Step-2 reviewer check would
have rejected this brief on every run, silently, forever. Reassigned to `vijayalaxmi-umate` (load 2).
*Found by my own T9 gate simulation, not by reading the brief.*

### C7. 7 stale briefs archived
6 blog briefs whose slugs now return 200 after T9 shipped them 08-25, plus
`psychologists-in-bangalore-brief.md`.

> **Verifier CORRECTION honoured.** The action is right but I justified it partly on "the page returns
> 200" — which is exactly the reasoning the 08-24 run warned against, because a REFRESH brief's target
> *always* returns 200. **The only valid ground is the `[COMPLETE 2026-08-21 commit:7163c6793b3c]`
> marker in BACKLOG.md.** "200" is struck from the rationale.
> AP7 does not break: T2 keys it off `tracking-db.json` status, not off the file existing.

### C8. `tracking-db.json` brief_path repointed
`/doctors/psychologists-in-bangalore` still pointed at the brief I archived this morning.
`task3-serp-analysis-briefs.md` branches on that string and `sheets_logger.py` logs it.
Repointed to the archive path; `tracking-db.backup-2026-08-26-pre-t20-briefpath.json` written first.
*(Verifier unprompted finding — I broke this myself an hour earlier and did not notice.)*

### C9. Discovery + paid mining
`scripts/new-content-discovery.py --all` **timed out** (same as T5's 08-24 run) → fell back to
`new-content-opportunities.json`, **2 days old** (vs the 14-day cache T5 used on 08-24). Per the T5
fallback ladder — not escalated. `scripts/google-ads-search-terms.py` ran clean (exit 0, 198 qualified
terms, 193 converting). Per the registry, a paid-mining result is never escalated.

---

## D. BRIEF-QUEUE STANDING JOB — refill fired

**Trigger:** effective T9-shippable `/blogs/` briefs = **5**, against a floor of 6.
(Not the 14 the queue appeared to hold — see C1.)

**Written: 6 briefs. Retired by the Verifier: 1. Net +5.**

| Brief | Tier | Evidence (all re-verified against source files) |
|---|---|---|
| `psychiatrist-online-consultation-india` | A | 690 impr/90d @ pos 9.0–9.1, 14 clicks — hub, no page exists |
| `online-psychiatrist-consultation-in-tamil` | A | 544 impr, **40 clicks, 7.4% CTR**, pos 5.1 |
| `online-counselling-in-malayalam` | A | 240 impr @ 6.4 + **1.0 measured paid conv** + Kerala P8 4-week signal |
| `online-therapy-in-telugu` | A | **1.0 measured paid conv** @ ₹30.16 |
| `online-counselling-in-hindi` | A | Delhi NCT **177 book-clicks W34, +86.3% record** — serves open `DELHI-NCT-T5-BRIEF-URGENT-01` |
| ~~`what-happens-in-a-counselling-session`~~ | ~~B~~ | **RETIRED — Verifier VETO** |

Composition: **5 Tier A / 0 Tier B / 0 Tier C** — satisfies INTENT-PRIORITY §3 (≥60% Tier A).

### D1. VETO — `what-happens-in-a-counselling-session` re-created a decision taken 8 days earlier

My brief asserted *"Nothing live covers it."* **False.** `/blogs/what-is-talk-therapy` is live (200) with
the H2 **"What to Expect in Your First Talk Therapy Session"** — whose body already covers
confidentiality, what the therapist asks, and how later sessions build. And a near-identical brief was
already vetoed and retargeted on 2026-08-18; the archived filename says so verbatim:
`NEW-what-to-expect-in-first-therapy-session-brief-vetoed-AP9-retarget-to-refresh-what-is-talk-therapy-2026-08-18.md`.
Its H2s were *"The First 10 Minutes"* / *"What Your Therapist Will Ask You"* / *"How the Session Ends"*.
Mine were *"The first ten minutes"* / *"What you will be asked"* / *"How a session ends"*.

**Root cause, and it applies to all 6 briefs I wrote today:** my AP9 test was *"sitemap token overlap
< 0.60"* — a **filename-similarity test, not a content-redundancy test**.
`what-happens-in-a-counselling-session` vs `what-is-talk-therapy` scores low on shared tokens and high
on shared intent, so the check waved through a page it should have blocked. **Replace token overlap with
a live-content check before the next refill run.** → filed as F3.

Retired to archive with the rationale. The demand (647 impr @ pos 5.7, 0 clicks) is real and routed to
T3 as a **refresh of `/blogs/what-is-talk-therapy`**, per the 08-18 decision.

### D2. VETO — the Telugu brief rested on a false premise and produced a wrong CTA

I wrote: *"there is no Telugu-language page anywhere on the site… the sitemap shows no
`/doctors/telugu-speaking-*` page."* **Six are live**, all 200, and all were in the very
`live_paths.txt` the brief cites. The consequence was not cosmetic: the brief routed a Telugu-language
query to **`/doctors/english-speaking-doctors-in-hyderabad`**. Corrected to
`/doctors/telugu-speaking-doctors-in-hyderabad` + `/doctors/telugu-speaking-doctors`.
Also corrected: ₹30.16 is the **8th cheapest of 193** converting terms, not "the cheapest".

### D3. CORRECTION — cannibalisation warning added to the Tamil brief
`psychiatrist online consultation free tamil`'s `triggering_page` is **`/doctors/tamil`**, which is
**live and already ranking pos 5.1 at 10.83% CTR**. That page is working. A hard warning is now in the
brief: target the *how-it-works/what-it-costs* intent, keep `/doctors/tamil-speaking-*` as the CTA, and
escalate rather than outrank a converting page. Also noted: **no Tamil or Hindi paid term exists** in the
converting set — those two briefs rest on GSC alone, unlike Malayalam and Telugu.

### D4. CORRECTION — ship-order note was in the wrong file
*"At most one language spoke per T9 run"* existed **only in the Hindi brief**. T9 opens briefs
independently and would never have seen it — the identical failure mode as C2. Replicated into the hub,
Tamil, Malayalam and Telugu briefs.

### Queue state at end of run

| | |
|---|---:|
| **T9 gate-passing `/blogs/` briefs** | **11** (floor 6) |
| of which authoring-complete | **6** |
| of which still carrying placeholder FAQ/takeaway fields | 5 |
| held (correctly, with machine-readable holds) | 5 |
| Tier mix of gate-passing | **9 A / 2 B / 0 C** |
| Tier A `/doctors/` briefs (out of T9 scope) | 57 |

> **Verifier CORRECTION honoured:** "12 shippable" would have been a misleading headline. 5 of the
> gate-passing briefs still contain literal `[PAA question 1]` placeholders, and **every** brief in the
> queue — including all 5 I wrote today — has a bracketed writer-instruction `quickAnswer`.
> Reported as **11 gate-passing / 6 authoring-complete**.

---

## E. ESCALATED TO KUSHAL — 3 (+ 4 re-delivered)

| # | Item | The ask |
|---|---|---|
| **E1** | 🚨 **`DOCTORS-LISTINGS-DEAD-LINKS-01`** | 10 dead Tier A booking CTAs live on the 6 pages shipped 08-25. Dev spec below — 7 are a prefix rewrite, 3 need a new target. Caused by T20's own incomplete 08-24 fix. |
| **E2** | **`CONDUCT-DISORDER-ADULTS-DECISION-01`** | Brief has a path contradiction **and** 4 unanswered clinical questions on DSM-5 diagnostic content. **(a)** route to `/doctors/conduct-disorder-in-adults` — but `/doctors/conduct-disorder-specialists` + `-in-bangalore` are already live, check redundancy; **(b)** keep as `/blogs/`, clinician answers the 4 questions and signs off; **(c)** retire — `/illnesses/conduct-disorder` and `/blogs/conduct-disorder-signs-causes-and-treatment` are both live. |
| **E3** | **`MINDTALK-REPO-STALE-CHECKOUT-03`** | Escalated 08-23 (T16) and 08-24 (T20). **My 08-24 recovery instruction was unsafe — corrected sequence below.** |

**E1 — dev spec, paste-ready.** In `~/Documents/GitHub/mindtalk/src/content/blogs/`:

```
# 7 links — pure prefix rewrite, all targets verified 200:
affordable-therapy-bangalore.mdx                 /doctors-listings/{counsellors,psychiatrists,psychologists,therapists}-in-bangalore  ->  /doctors/…
best-psychiatrist-for-depression-bangalore.mdx   /doctors-listings/depression-specialists-in-bangalore  ->  /doctors/depression-specialists-in-bangalore
family-counselling-bangalore.mdx                 /doctors-listings/{family-therapists,therapists}-in-bangalore  ->  /doctors/…

# 3 links — NO /doctors/ equivalent exists; needs a substitute (all verified 200):
cbt-therapy-online-india.mdx          /doctors-listings/online-therapists-india          ->  /treatments/online-therapy
online-couples-therapy-india.mdx      /doctors-listings/couple-therapists-in-bangalore   ->  /doctors/relationship-issues-psychologists-in-bangalore
online-marriage-counselling-india.mdx /doctors-listings/marriage-counsellors-in-bangalore ->  /doctors/relationship-issues-specialists
```
A blanket `s#/doctors-listings/#/doctors/#g` fixes 7 of 10 and leaves the other 3 still 404 — do the
three substitutions explicitly.

**E3 — corrected recovery sequence. Do NOT re-clone.**

Facts (all independently verified twice): local `main` = **`feb506b`, 2026-07-21 — 36 days stale**;
local `origin/main` ref = **`7163c67`, Aug 21 — 5 days stale**; HEAD sits on branch
`feat/exec-refresh-doctors-bangalore-20260821`; `feat/auto-ship-blogs-2026-08-25` exists but points at
`7097922` — an **empty shell** (and so do the `-08-05` and `-08-18` branches, so the pattern predates
this week); **none of the 6 MDX files T9 shipped on 08-25 exist locally** though all 6 URLs are 200;
commits `5a413a57`/`b52b6fc8` are not valid local objects; `.git/shallow` absent, so this is not a
shallow clone. **Conclusion: T9 ships via the GitHub Git Data API and bypasses the local checkout
entirely. The local tree is a write-only graveyard.**

> **Verifier VETO on my 08-24 recommendation — honoured.** I proposed stash-and-pull, then today
> proposed re-cloning. **Re-cloning would destroy 80 untracked paths** — `git stash` does not touch
> untracked files by default. Those include whole untracked directories under `src/`
> (`src/app/find-your-match/`, `src/components/analytics/`, `src/lib/seo/`, `src/hooks/`, `src/types/`)
> plus 16 `src/content/mindful-minutes/*.mdx` and 6 `src/content/doctors*/*.mdx`. Every untracked route
> sampled is live in production, and all 10 modified tracked files were confirmed already-live
> (e.g. `discover-schema.ts`'s `audioObjectNode` — prod `/mindful-minutes/4-7-8-breathing` emits
> AudioObject JSON-LD). But that was inferred **from production, not confirmed against origin**
> (`git ls-remote` has no credentials here), and it says nothing about the non-content artifacts
> (`.agents/`, `.claude/skills/`, `docs/ads/`, `docs/changelogs/`, `scripts/audit-content.mjs`).

```bash
cd ~/Documents/GitHub/mindtalk
git fetch origin
git branch backup-local-$(date +%F)                                  # preserve committed work
tar czf ~/mindtalk-untracked-$(date +%F).tgz $(git ls-files --others --exclude-standard)
git checkout main && git reset --hard origin/main                    # only after the tarball exists
```
Re-clone only once that tarball exists **and** `git ls-remote origin main` runs with working credentials.

**Re-delivered — 4 pending human actions, now 11 days stale.** T16's Slack delivery failed on 08-15 and
was never retried; re-delivered 08-24, still open today: `PERSONALITY-DISORDER-YMYL-SIGNOFF-01`,
`STUB-PILOT-CONVERSION-VERDICT-01`, `T9-SLEEP-STAGES-AP9`, `W28-alzheimers` (A/B).
*(`TRUST-ISSUES-HUMAN-01` is now struck through in BACKLOG — closed. Corrected from the 08-24 count of 5.)*

**Not re-escalated** (verified real, already with Kushal, no new information):
`BANGALORE-COMMERCIAL-INVESTIGATE-01` (watch 08-31), `GSC-MEASUREMENT-INTEGRITY-01`,
`T6-POSITION-UNITS-BUG-01`, `T17-7-AEO-DOCTORS-SPRINT-01`, `DEAD-CLICKS-W34` (P2),
`ASSESSMENT-AIO-SCHEMA-AUDIT-01`, `psychology-of-love` §1 Tier C call.

---

## F. FILED — not Kushal's

- **F1 `T9-RUN-LOG-ARITHMETIC-01`** — `logs/auto-ship-2026-08-25.txt` reports 6 + 15 + 52 = **73**
  candidates; ground truth is 6 + 14 + 54 = **74**. Both skip buckets are wrong and one candidate
  vanishes (probably `gender-identity-disorder`, excluded at Step 1). Any downstream reasoning from that
  log is unsound. → Meta-Learner (T13).
- **F2 `GSC-PULL-WINDOW-OVERLAP-01`** — in every file `scripts/gsc-pull.py` writes,
  `previous_window` = 08-08→08-15 and `current_window` = 08-15→08-22. **2026-08-15 is in both.** The
  windows are not disjoint; a day is double-counted depending on endpoint inclusivity. This sits
  underneath *every* drop and midpoint verdict the engine produces. One-line fix, but it lives in
  `scripts/` — **T20 may not edit it.** → Strategist Verifier.
- **F3 `AP9-TOKEN-OVERLAP-IS-NOT-A-REDUNDANCY-TEST-01`** — the AP9 check used by T20's refill (and
  copied into 6 briefs today) compares slug tokens against sitemap paths. That is a filename-similarity
  test. It passed a page that duplicates a live page and re-created an 8-day-old veto (D1). Any brief
  generator must fetch and read the candidate's nearest live page, not diff its filename. → T5 + T20 spec.
- **F4 `T4-MIDPOINT-NEEDS-IMPRESSION-FLOOR-01`** — T4 raised `URGENT 🚨 manual review required
  immediately` on a page with **6 impressions**. Position deltas need a minimum-impressions floor before
  they can fire an alert. → Meta-Learner (T13).
- **F5 `GSC-INFRA-01` recurrence #5** — the host disk is at **227G/229G, 100% full, 1.7G free**. It
  blocked T20's own scratch writes this run. Already open with Kushal; noted, not re-escalated.

---

## G. VERIFIED, NO ACTION

- **Weekly cap respected.** `max_new_content_per_week = 20`; T9 used 6/20 this week. **T20 shipped 0
  pages.** `src/**` untouched, `scripts/*.py` untouched, nothing deleted — everything archived.
- **Schema fix confirmed still live.** `/treatments/narrative-therapy` emits `FAQPage` + `MedicalTherapy`;
  `/doctors/psychologists-in-bangalore` emits `FAQPage` + `MedicalOrganization` + 10 `Physician` nodes.
  `SCHEMA-MEDICAL-TYPES-01` (PR #23) is holding.
- **Google Core Update began rolling today (2026-08-26)**, on top of the Spam Update running since 08-18.
  Both false-positive candidates today were single-page position artifacts. **Do not queue refreshes off
  this week's position data** — wait for the update to settle.

---

## RUN SUMMARY — 2026-08-26

| | |
|---|---|
| Flags collected | 9 |
| **False positives closed** | **0** — 2 of my 3 closures were vetoed and withdrawn |
| **De-escalated** | **1** — narrative-therapy URGENT → insufficient data, defer to Day-42 (09-15) |
| **Re-opened by the Verifier** | **1** — psychologists-in-bangalore stays on its 08-31 watch |
| **Auto-fixed** | **9** — 54 briefs unblocked · 2 prose-only holds made literal · 7 archived · 1 brief repaired · 1 held · 6 link-order guards · 1 phantom reviewer · 1 tracking-db path · discovery fallback |
| **Briefs written / retired** | **6 written, 1 retired by Verifier → net +5** |
| **Escalated to Kushal** | **3** + 4 re-delivered |
| **Filed, not Kushal's** | **5** |
| Brief queue | **11 T9 gate-passing (6 authoring-complete), 5 held** · 9A/2B/0C · floor 6 ✅ |
| Pages shipped by T20 | **0** |
| Verifier sub-agent | **1 UPHELD / 3 CORRECTION / 3 VETO / 5 unprompted — all honoured** |

**Net.** The queue was never starved of briefs — it was starved of briefs T9 could *read*. 54 files
carried their intent tier three lines above the place the gate looks, and the engine reported a full
pipeline while shipping from a pool of six. That is now fixed and the queue stands at 11 gate-passing.

But the run's real finding is the one nobody asked for: **the six pages that went live yesterday carry
ten dead booking links, and I put them there.** The 08-24 fix corrected `/doctors-listings/` → `/doctors/`
in the field I happened to be looking at and left the same string in the anchor lists one section below.
T9 authored them into MDX the next day. On `/blogs/affordable-therapy-bangalore`, all four body links are
dead; on `/blogs/online-couples-therapy-india`, the only one is. Those are the booking CTAs.

**And the discipline note, third run running.** I argued the measurement-integrity case on 08-23,
committed the same error on 08-24, was corrected, and then did it again today — closing a CRITICAL on a
page-level average that moved only because 27 low-position queries left the window, against an open watch
**I opened myself two days ago**, in a file whose own `signal` field said `CTR_DROP`. I also claimed 24
internal links inside an element that does not exist on the page, asserted that no Telugu page existed
while six were live in the file I was citing, and re-wrote a brief that was vetoed eight days ago. The
Verifier caught all four. The pattern is unchanged and now unmistakable: **I reason from the artefact I
am holding instead of the artefact I am claiming about.** Every wrong claim today would have been
falsified by opening one more file.

---

# 🔧 T20 AUTO-REMEDIATION — 2026-08-26 (Wednesday, 8:45 PM IST — scheduled run)

> Second T20 run today. The 12:52 IST run was a catch-up after Mac Mini downtime; this is the regular
> 8:45 PM slot, reading T10's 8:09 PM Strategist output. Scope tonight = flags raised **since** that
> run: T10's 20:18 BACKLOG/WATCH stamp, T14 technical-health (09:55), T16 ops-health (09:46),
> T19 conversion-intelligence (11:16).

**Flags collected: 12 · False positives closed: 9 · Downgraded: 1 · Auto-fixed: 5 · Escalated: 4 ·
Filed to T13: 5 · Pages shipped by T20: 0**

---

## A. FALSE POSITIVES CLOSED (Rule 1) — 9

### A1–A6. `logs/ops-health-2026-08-26.log` — all 6 "❌ MISSED" verdicts are false

Ground truth = `list_scheduled_tasks`, pulled 20:58 IST and independently re-pulled by the Verifier
(all `lastRunAt` matched to the second):

| task | claimed | actual `lastRunAt` | IST | verdict |
|---|---|---|---|---|
| T15 mixpanel-conversion-monitor | MISSED / "chronic" | `2026-08-26T04:35:37Z` | 10:05 | ✅ RAN |
| T19 conversion-intelligence | MISSED / "chronic" | `2026-08-26T05:36:47Z` | 11:06 | ✅ RAN |
| T9 auto-ship-new-blogs | MISSED | `2026-08-26T09:37:11Z` | 15:07 | ✅ FIRED (see E2) |
| T11 executor | MISSED | `2026-08-26T11:06:09Z` | 16:36 | ✅ RAN |
| T10 strategist | MISSED | `2026-08-26T14:39:59Z` | 20:09 | ✅ RAN |
| T20 auto-remediation | MISSED | `2026-08-26T15:25:06Z` | 20:55 | ✅ RAN (this run) |

Corroborated by artifacts independent of the scheduler: `logs/conversion-intelligence-2026-08-26.md`
(T19, 14 Mixpanel queries), `brain/memory/experiments/2026-08-26-flag_for_human-*.md` ×2 (T11), and a
`2026-08-26 T10` stamp in BACKLOG.md + WATCH.md + BRAIN.md (T10).

**Root cause D1 — future runs mislabelled as missed.** The log was written at **09:46 IST** as a
catch-up for T16's 08-25 23:08 slot, but evaluated **2026-08-26's** schedule. Every task whose
`nextRunAt` fell later that same day was still in the future at check time and was marked MISSED. Its
conclusion — *"Likely cause: Mac Mini sleep/offline from ~10 AM to ~11 PM IST"* — is unsupported. The
Mac Mini was up; the tasks ran.

### A7. "T15+T19 chronic: 7-day consecutive miss" — category error

Both are **Wednesday-only** tasks (`0 10 * * 3`, `0 11 * * 3`). A 7-day gap is not a miss, it is the
cadence; their prior run 2026-08-19 was the previous Wednesday. **Root cause D2 — weekly-cadence tasks
judged against a flat 24h staleness test.**

### A8. `GSC OAuth EXPIRED — 9 consecutive weeks` (T14 recommended action **#1**, "URGENT")

Closed. T20 ran a live pull tonight:
`PYTHONPATH=.pip-packages python3 scripts/gsc-pull.py --url /illnesses/anxiety`
→ **exit 0**, real data (`impressions +16%`, 50 keywords), `gsc-data/illnesses_anxiety.json` written
15,736 B. Independently re-run and confirmed by the Verifier. Corroborated: T2's 08-25 validator wrote
two 17 KB `gsc-data/*.json` payloads with live rows. **GSC is authenticating and returning data.**
Whatever narrower API surface T14 probes (indexation / URL-Inspection scope) is not "OAuth expired" —
and that framing has put a false credential request in front of Kushal for **nine weeks**.
*(Verifier correction honoured: T20's supporting detail "token refreshed today 09:52" was wrong — the
`gsc-token.pickle` mtime is 21:00:43, i.e. rewritten by T20's own test pull. Immaterial to the verdict,
but it was an unchecked claim and is withdrawn.)*

### A9. `/blogs/understanding-dominant-personality-and-dominating-nature` "missing FAQPage **despite
having `faqs:` frontmatter** — possible MDX-level regression"

Closed. The page has **no `faqs:` key** — the string `faqs` appears nowhere in the file. Its 3
`blocks.faq-list` components are empty placeholders (`id:` + `title: null`, nothing else).

T20 parsed all 283 blog MDX; the Verifier re-parsed indentation-aware and matched exactly:

- **71** carry top-level `faqs:` → these emit FAQPage correctly ✅
- **185** carry legacy `blocks.faq-list` without `faqs:`
- **0 of those 185** contain any question/answer data. Across all 283 files, **698/698** faq-list blocks
  are `title: null`; the key histogram over all 662 blocks in the 185 files is `{id: 662, title: 662}`.

Verifier went further and read the emitter: `src/app/blogs/[slug]/page.tsx:224` reads `data.faqs` and
gates on `validFaqs.length > 0`; nothing in the blog route reads `faq-list` (only
`src/app/[slug]/page.tsx:189`, the CMS-pages route). **The live output is exactly what the code
predicts. No regression, no lost FAQ content, no emitter bug.**

> Note on provenance: T14 phrased this correctly as an *investigation* ("investigate if `faqs:`
> frontmatter is missing from that specific MDX file"). The false assertion — "**despite having** faqs:
> frontmatter" — was introduced when T10 hardened it into the BACKLOG row. The failure is in the
> hand-off, not in T14.

*(Non-bug observation for T3/T5: 212 of 283 blog pages have no FAQ content at all. That is a content
opportunity, relevant to P5 AI-citation — not a defect, and not escalated.)*

---

## B. DOWNGRADED — 1

**`SCHEMA-MEDICALWEBPAGE-RESIDUAL-01` — H → P2.** Verified via `curl -L` + `@type` extraction on four
pages (bodies 132–224 KB; the Verifier flagged that a truncated `curl` exit-23 body would fake an
"absent schema" result, so body size was asserted, not just exit code):

| page | emits |
|---|---|
| `/illnesses/anxiety`, `/illnesses/depression` | `MedicalCondition` ✅ `FAQPage` ✅ (10 Q/A) `BreadcrumbList` ✅ `WebPage` `Article` |
| `/treatments/counselling-therapy`, `/treatments/narrative-therapy` | `MedicalTherapy` ✅ `FAQPage` ✅ (4 Q/A) `BreadcrumbList` ✅ |

`MedicalWebPage` is genuinely absent on all four — **the flag is real.** But the severity is not:
neither `MedicalWebPage` nor the types already present produce a Google rich result, so adding it
changes no SERP eligibility. Calling it "the most relevant open schema gap" during the Core Update
overstates it.

> **Verifier CORRECTION honoured.** T20 justified the downgrade by calling `MedicalCondition` /
> `MedicalTherapy` "the *more specific* types". That is a category error — `MedicalWebPage` subclasses
> `WebPage` (page container), `MedicalCondition` subclasses `MedicalEntity`. Orthogonal branches, not
> substitutes. The phrasing is withdrawn; the conclusion stands on the rich-result argument alone.

> **Verifier unprompted finding, carried into the dev spec:** `/treatments/*` emit **no page-level
> container at all** — no `WebPage`, no `Article`. That is a larger gap than the flagged one and was
> sitting in a parenthetical.

---

## C. AUTO-FIXED (Rule 2) — 5

**C1. Archived 3 superseded Meta-Learner proposals.** `t16-read-pending-human-actions-2026-07-26-2030.md`,
`t5-floor-miss-brain-flag-2026-07-26-2030.md`, `t5-floor-12-output-enforcement-2026-07-19-2030.md` →
`brain/applied-changes/superseded/*.archived-2026-08-26-T20` (moved via `os.rename()`, **nothing
deleted**; FUSE `unlink()` EPERM still active, re-confirmed).

All three were verified dead before moving: the first two carry `⛔ SUPERSEDED — DO NOT APPLY`
tombstones naming their live replacements, and the Verifier confirmed the superseding changes are
actually in place — `### Part A.5 — Pending human-action escalations` at
`cowork-tasks/task16-operational-health-backup.md:90`, and `**BRAIN.md floor-miss flag
(Slack-independent):**` at `cowork-tasks/task5-new-content-discovery.md:141`. The third has a
byte-identical `.applied` twin.

**This ends the churn that fired today's `🚨 STALE ALERT` and 20+ consecutive MISMATCH-SKIPs** (39
mismatch entries in `applied-history.md`). `brain/proposed-changes/` now holds only the 3 genuinely
active previews, all Apply-on **2026-08-30** (future) — confirmed by the Verifier.

**C2. Wrote the dev handoff that BACKLOG cited but which did not exist.** T10's 20:18 stamp pointed dev
at `reports/dev-handoff-2026-08-26-dead-links.md`; the file was never created — the spec lived only
inside this log. Now written, covering all four dev items with tonight's re-verified status codes.

**C3. Corrected the false claim in `SCHEMA-MEDICAL-TYPES-01`.** The line "FAQPage **+ MedicalWebPage**
JSON-LD now emit from illness/treatment templates" is false — PR #23 shipped FAQPage only. **That single
wrong line is what generated T14's alarm tonight.** Corrected in place with the live evidence.

**C4. Annotated `SCHEMA-MEDICALWEBPAGE-RESIDUAL-01`** with the verification result, the downgrade, and
the closure of the `faqs:` sub-claim, so the next reader does not re-litigate it.

**C5. Appended a correction block + addendum to `logs/ops-health-2026-08-26.log`** so the 6 false MISSED
verdicts cannot be re-read as truth by tomorrow's T10.

---

## D. ESCALATED TO KUSHAL / DEV — 4

**E1 🚨 `DOCTORS-LISTINGS-DEAD-LINKS-01` — day 2, still broken, re-escalated.**
Re-verified 21:00 IST: all 9 `/doctors-listings/*` targets 404; exactly 10 dead anchors across exactly
6 live pages (4 / 2 / 1 / 1 / 1 / 1 — Verifier confirmed each count from live HTML). On
`/blogs/affordable-therapy-bangalore` **every** body booking link is dead; on
`/blogs/online-couples-therapy-india` the only one is. All 6 prefix-rewrite targets and all 3
substitute targets verified 200 with real content.

> **Verifier VETO honoured — the spec's fix location was wrong.** It said "in
> `~/Documents/GitHub/mindtalk/src/content/blogs/`". Local `HEAD` = `feb506b`, **2026-07-21, five weeks
> stale**; **none of the 6 `.mdx` files exist locally**, and a repo-wide grep for `doctors-listings`
> across all `.mdx` returns **zero**. A dev following the original spec would have found nothing and
> closed the ticket as already-fixed. The handoff now leads with this and directs the fix to the remote
> tree via the GitHub Data API (T9's actual ship path), or a `fetch`/`reset` **after** the
> untracked-file tarball from `MINDTALK-REPO-STALE-CHECKOUT-03` exists.

**E2 🚨 `T9-SILENT-DEATH-01` — NEW tonight.**
T9 fired on schedule at 15:07 IST and **produced nothing**: no `logs/auto-ship-2026-08-26.txt` (every
prior run wrote one), no tracking-db write, no Slack archive, and **0 pages live** — the Verifier curled
all 16 `/blogs/` brief slugs, every one 404. Session transcript
`local_3d91a081-244e-43af-8721-e63e76a1a7ea` shows **4 tool calls — bash, ToolSearch ×2, Vercel
`list_teams` — then termination with no result line.** Silent early death at startup, not a
"0 candidates" skip and not a cap block (11 shippable briefs, weekly cap 6/20, cluster slot open).

**This was the first T9 run after the brief queue was unblocked this morning.** The pipeline was finally
loaded and the ship step did nothing. Last call before death was a Vercel MCP call → suspect tool/MCP
init, not content logic. **T20 deliberately did not ship in T9's place:** Core Update Day 1 is live and
T9 runs again Friday 08-28, so duplicating it buys nothing and risks unattributable movement. T20 will
re-verify on 08-28 and escalate as systemic if the artifact is missing again.

**E3 `GSC-MEASUREMENT-INTEGRITY-01` — re-escalated with new information (reproduced on demand).**
Previously "reported"; now deterministic. Same page, seconds apart:

```
gsc-pull.py --url /illnesses/anxiety                      -> 100 impr / 50 keywords / +16%
gsc-pull.py --url https://www.mindtalk.in/illnesses/...   ->   0 impr /  0 keywords /  +0%  exit 0
```

The failure is **silent** — `+0%/+0%` reads exactly like a legitimate "no change" verdict.

> **Verifier finding — the blast radius is worse than reported.** A full-URL call still **writes a
> junk-keyed zero-row `gsc-data/*.json`** that later reads as legitimate history. **5 such records exist
> from 2026-08-23**, and for **4** (`relationship-stress`, `sleep-schedule`, `mental-exhaustion`,
> `eft-tapping`) **no valid path-form record exists at all** — the only GSC data on disk for those pages
> is a false zero. Those 4 are the W30-W33 cohort already flagged `MEASUREMENT-INVALID`. **This is the
> root cause of that flag.** Spec now asks for three things: path normalisation, raise-on-zero-rows, and
> purge + re-pull of the 5 junk records before T12 re-issues the W30-W33 Day-42 finals (due 09-08).

**E4 `SCHEMA-MEDICALWEBPAGE-RESIDUAL-01` (P2) + non-www `307` → `301` (P3).** Both in the handoff,
both batched — explicitly *not* Core-Update urgent. The 307 is now in its 10th consecutive week.

**Not re-escalated** (verified real, already with Kushal, no new information): `CORE-UPDATE-YMYL-HOLD-01`,
`W38-NARRATIVE-THERAPY-URGENT-01` (a/b/c pending), `CHATGPT-AEO-SPRINT-REVIEW-01` (hold to 09-05),
`DELHI-NCT-T5-BRIEF-URGENT-01` (P15 demoted to one-week anomaly by T19 W35 today: 97 clicks, −45.2%),
`THERAPIST-NEAR-ME-SERP-CHECK-01`, `MINDTALK-REPO-STALE-CHECKOUT-02/03`, `GSC-INFRA-01` (disk 226G/229G,
**2.7G free** — recurrence #6, worked around via `HOME`/`XDG_CACHE_HOME` redirect), and the 4 pending
human actions now **12 days** stale.

---

## E. FILED — not Kushal's — 5

- **F1 `T16-FUTURE-RUN-MISLABELLED-AS-MISSED-01`** — a catch-up run must evaluate the schedule for the
  day it is catching up on, and must never mark a task missed when `nextRunAt > now`. → T13.
- **F2 `T16-WEEKLY-CADENCE-DAILY-STALENESS-TEST-01`** — staleness must be measured against each task's
  own cron interval, not a flat 24h. → T13.
- **F3 `T16-LOG-MISSTATES-OWN-RUN-TIME-01`** *(Verifier, unprompted)* — the log header claims "Run time:
  2026-08-26 ~23:00 IST" when T16 had not run that day at all. A log that misstates its own run time
  makes every staleness inference in it unauditable. → T13.
- **F4 `T14-GSC-PROBE-OVERCLAIMS-AUTH-FAILURE-01`** — T14 must name the exact API call that fails rather
  than inferring a blanket "OAuth expired"; 9 weeks of false credential escalation. → T13.
- **F5 `T9-SHIP-GATE-IGNORES-DO-NOT-SHIP-MARKER-01`** *(Verifier, unprompted)* — T20 writes
  machine-readable `⛔ DO NOT SHIP` / NEEDS_HUMAN holds into briefs, and **no downstream gate consumes
  them**. 5 briefs would otherwise be eligible. → T13.

---

## F. VERIFIED, NO ACTION

- **Brief queue HEALTHY — no refill fired.** 16 `/blogs/` briefs pass the raw gate (`intent_tier` in the
  proposed-frontmatter yaml fence **and** slug returns 404); **5 carry an explicit `⛔ DO NOT SHIP` /
  NEEDS_HUMAN hold**, so **true shippable = 11 (9 Tier A / 2 Tier B)** against a floor of 6.
- **Discovery FRESH** — `new-content-opportunities.json` written 2026-08-24 (Monday, its cadence). No
  `DISCOVERY STALE` in today's logs. No re-run needed.
- **Weekly cap respected** — `max_new_content_per_week = 20`; 6/20 used. **T20 shipped 0 pages.**
  `src/**` untouched, `scripts/*.py` untouched, **nothing deleted** — everything archived.
- **Core Update Day 1 (2026-08-26).** No refreshes queued off today's position data.

---

## RUN SUMMARY — 2026-08-26 (evening)

| | |
|---|---|
| Flags collected | 12 |
| **False positives closed** | **9** — 6 ops-health MISSED (one root cause) · weekly-cadence mislabel · GSC OAuth (9 wks) · FAQPage sub-claim |
| **Downgraded** | **1** — SCHEMA-MEDICALWEBPAGE-RESIDUAL-01 H→P2 |
| **Auto-fixed** | **5** — 3 proposals archived (ends 20+ day churn) · dev handoff written · 2 false BACKLOG claims corrected · ops-health log corrected |
| **Escalated** | **4** — dead links (day 2, spec re-pointed) · T9 silent death (NEW) · gsc-pull (reproduced + junk records) · schema/307 (batched) |
| **Filed to T13** | **5** |
| Brief queue | **11 shippable (9A/2B)** · 16 raw-gate, 5 held · floor 6 ✅ · no refill needed |
| Pages shipped by T20 | **0** |
| Verifier sub-agent | **9 claims audited — 5 UPHELD · 3 CORRECTION · 1 VETO · 7 unprompted findings — all honoured** |

**Net.** Nine of twelve flags were not real. The six "missed task" alarms came from a catch-up monitor
reading the wrong day's schedule; the nine-week GSC credential request dissolved on one live API call;
the FAQPage "regression" was a page that simply has no FAQs. What survived is worth more than what did
not: **T9 fired this afternoon and silently died after four tool calls**, on the first run after the
brief queue was finally unblocked — the ship pipeline is down and nothing else noticed, because
ops-health tests `lastRunAt` rather than "did the task write its artifact".

**And the discipline note.** The Verifier caught three errors of mine tonight. Two were the same failure
the last four runs recorded: I counted 16 shippable briefs while **5 of them carry DO-NOT-SHIP holds I
wrote myself — two of them this morning** — and I reported "7 of 7" false MISSED verdicts because I
grepped the marker count *after* appending my own correction and counted myself. The third, the dead-link
spec pointing at a local checkout where the files do not exist, would have wasted a dev's evening and
likely closed a P0 as already-fixed. Same root cause each time: **I measured the artefact in my hand
instead of the artefact I was making a claim about.** The counter-move is not more care, it is
structural — every count I publish needs a second, independently-derived count before it leaves the run.

---

# 🔧 T20 AUTO-REMEDIATION — 2026-08-28 (Friday)

Run start 16:01 IST. Catch-up burst: the whole scheduler replayed today between 15:08 and 16:01 IST
(every task's `lastRunAt` falls in that window), so "today's logs" are a compressed day, not a normal one.

## A. THE HEADLINE — `T9-SILENT-DEATH-01` root cause found. It is not a silent death.

T9 fired Wed 08-26 and Fri 08-28 (scheduler `lastRunAt` confirms both) and wrote no artifact either
time. Ops-health called it a silent death and stopped there. It is worse and more fixable than that:

**The 08-26 run authored SEVEN complete blog pages and died between authoring and `git commit`.**

All 7 are untracked files in the local checkout; all 7 are **404 in production**. Two days of
finished content never shipped. Separation from the 14 already-live MDX files sharing the same
`2026-08-28 15:36:29` mtime (a bulk working-tree restore, not authoring) is exact and unambiguous:

| | the 7 undeployed | the 14 already-live |
|---|---|---|
| `publishedOn` | `2026-08-26` | `08-04` / `08-11` / `08-25` |
| `intent_tier` in frontmatter | present (5×A, 2×B) | absent |
| production HTTP | **404** | **200** |

All 7 pass the full Verifier gate with **zero vetoes** — body 1,085–1,455 words, 4–8 unique internal
links, 5 FAQs each, titles ≤64, descriptions ≤159. No broken-JSX risk.

`therapy-cost-in-india` · `psychiatrist-online-consultation-india` ·
`online-psychiatrist-consultation-in-tamil` · `online-therapy-for-indians-in-usa` ·
`couple-therapy-cost-in-bangalore` · `therapy-after-a-breakup` · `acrophobia-treatment-fear-of-heights`

**T20 cannot ship them** — hard constraint, never push to the website repo. Escalated with a
paste-ready spec: `reports/dev-handoff-2026-08-28-t9-undeployed-batch.md`. ~15 min of work; no
authoring, no review. Two blockers named in the spec: ship all 7 **atomically** (3 intra-batch
forward links), and swap one non-resolving reviewer.

**The systemic point:** the brief queue is healthy at 11 against a floor of 6. Content velocity is
not supply-constrained. The ship stage is dropping its own output on the floor, and ops-health
cannot see it because T16 tests `lastRunAt` instead of "did the artifact appear".

## B. FALSE POSITIVES CLOSED — 5

- **`form_submitted −52% CRITICAL crash` — CLOSED, recovered and then some.** T15's 08-26 reading was
  55 unique submitters/7d. Re-measured on the same metric and window today (Mixpanel 4011856,
  unique users, last 7d): **156** — +184% vs the "crash" figure and +36% above the 115 baseline it
  was compared against. Highest reading in the series.
- **`BACKEND-FAIL-ENGINEERING-01` (13.7%, "4th consecutive rise, engineering escalation required
  before ads restart") — CLOSED.** Recomputed on T15's own formula, last 7d:
  `lead_create_failed 16 / (form_submitted 156 + lp_form_submitted 92 + 16)` = **6.06%**. Halved from
  13.7%, below the prior 7.5% reading. Net leads 113 → **248 (+119%)**.
- **Why both fired:** T15 ran 07-29, 08-05, then **08-26** — it skipped 08-12 and 08-19, then labelled
  a **21-day** change "WoW". Its 7-day window (Aug 20–26) also landed on a trough. Nothing re-read the
  metric before T10 escalated it today. → filed to T13.
- **`PTSD-CLUSTER-DROP-01` ("PTSD Treatment −61.3% impr / −53 positions, SEVERE") — CLOSED, direction
  is inverted.** GSC live (`sc-domain:mindtalk.in`), Aug 1–7 vs Aug 15–21: PTSD cluster **229 → 550
  impressions (+140.2%)**, clicks 12 → 18; head term `cptsd test` 145 → 344 impr, position **10.3 →
  8.7 (improved)**. The exact `"ptsd treatment"` family: 12 → 18 impr (+50%), and the exact query's
  own absolute base is **2–6 impressions** at position **2.2 → 2.5**. A "−61.3%" on a 6-impression
  base is four impressions of noise, and "−53 positions" cannot be reconciled with pos 2.2 → 2.5.
  **The 09-05 `investigate_regression` should be cancelled.** Root cause: the weekly report computes
  percentage deltas with no minimum-impression floor. → filed to T13.
- **`misses: executor(Fri)` — CLOSED, third recurrence of a known T16 bug.** `mindtalk-executor`
  `nextRunAt = 2026-08-28T11:05:25Z` (16:35 IST) — **in the future**. T16 marked it missed at 15:55 IST.
  This is exactly `F1 T16-FUTURE-RUN-MISLABELLED-AS-MISSED-01`, filed to T13 on 08-26, still unfixed.
- **`misses: auto-remediation(Fri)` — CLOSED, same class.** T16 evaluated at 15:55 IST; T20 started
  16:01 IST. (`auto-remediation(Thu)` is real — no `logs/remediation-2026-08-27.txt` — but it is the
  same Mac Mini downtime as the whole catch-up burst, not a separate actionable failure.)
- **9 AP8 pos-100 quarantines — correctly quarantined, no action.** Spot-checked 4 of the 9 live:
  `/illnesses/sleep-disorder`, `/treatments/cognitive-behavioural-therapy-cbt`,
  `/blogs/understanding-technology-addiction-and-mobile-addiction`,
  `/doctors/psychologists-in-bangalore` — all **200**. Pipeline handled it; nothing to escalate.

## C. AUTO-FIXED — 4

1. **Brain backup stall CLEARED — and the durable pattern found.** `brain/.git/index.lock` was a
   stale 0-byte lock from 08-26 21:10 (42h). `rm` fails EPERM on the FUSE mount. Renaming it works —
   but the **Verifier caught that renaming alone does not hold**: git recreates the lock on the very
   next *read* and cannot unlink it, so every `git status` re-poisons the repo for writes. The
   working fix is to **clear the lock in the same invocation as the git write**. Applied:
   `git add -A` → 36 files staged → commit **`6a746b4`** (5,506 insertions) → **pushed**, remote
   `mindtalk-brain-backup` now at `6a746b4` (confirmed via `git ls-remote`). Two days of brain state
   — BACKLOG, BRAIN, TRAJECTORY, WATCH, 8 `memory/*` files — was uncommitted and unbackupable. It is
   now safe. Nothing deleted; the lock was archived, not removed.
2. **Broken reviewer reference corrected in a brief.** `NEW-psychiatrist-online-consultation-india-brief.md`
   specified `reviewer: "santanu-tripathy"`. Verified non-resolving: no
   `src/content/doctors/santanu-tripathy.mdx`; `/doctors/santanu-tripathy` 301s to the generic
   `/doctors` index; and the already-live page using it (`/blogs/drug-addiction-symptoms`, 08-04)
   emits **no `reviewedBy` Person node at all**, while the control `/blogs/signs-of-adhd` emits a full
   Person node. Corrected to `dr-sneha` (MD Psychiatry, page 200, load 3). Same mechanical class as
   the 08-22 `psychology-of-love` broken-link fix.
3. **7 briefs annotated `📦 MDX ALREADY AUTHORED — AWAITING COMMIT/PUSH`** so the next T9 run does
   not re-author work that already exists, and so the state is legible to a human. Deliberately
   phrased to avoid T9's five hold-filter phrases — these pages *should* ship.
4. **Stale remote-tracking ref lock cleared** (`refs/remotes/origin/main.lock`) so brain
   `git status` stops reporting a false "ahead 1".

## D. ESCALATED — 2 (both with the fix pre-written)

- **P0 `T9-SILENT-DEATH-01` → 7 undeployed pages.** Spec:
  `reports/dev-handoff-2026-08-28-t9-undeployed-batch.md`. Includes the exact `git add` path list
  (NOT `git add -A` — the checkout has ~13,000 untracked files), the reviewer diff, the atomic-ship
  warning, the post-deploy curl verification, and the two engineering fixes that stop the recurrence
  (T9 must write its log on the failure path; T16 must test for the artifact, not `lastRunAt`).
- **P1 `DOCTORS-LISTINGS-DEAD-LINKS-01` — day 3, re-verified real, unchanged.** All 9
  `/doctors-listings/*` anchors still **404** today. Verifier independently re-derived the census by
  curling all 23 candidate live pages: **exactly 10 dead anchors on exactly 6 pages**, matching the
  08-26 handoff line-for-line. A blanket `/doctors-listings/` → `/doctors/` rewrite fixes 7 of 10;
  `/doctors/couple-therapists-in-bangalore`, `/doctors/marriage-counsellors-in-bangalore` and
  `/doctors/online-therapists-india` are themselves 404, so the handoff's three named substitutions
  are required. Spec unchanged: `reports/dev-handoff-2026-08-26-dead-links.md`.

**Not re-escalated** (verified real, already with Kushal, no new information): `CORE-UPDATE-YMYL-HOLD-01`,
`W38-NARRATIVE-THERAPY-URGENT-01`, `T9-DOCTORS-QUEUE-MISLABEL-01`, `STUB-PILOT-CONVERSION-VERDICT-01`
(a/b/c, 14 days old), `MINDTALK-REPO-STALE-CHECKOUT-02/03`, `GSC-INFRA-01`, `THERAPIST-NEAR-ME-SERP-CHECK-01`.

## E. FILED — not Kushal's — 4

- **F6 `T15-MULTI-WEEK-GAP-LABELLED-WOW-01`** — T15 must compare against its own *previous run*, and
  label the interval it actually measured. An 08-26-vs-08-05 delta reported as "WoW" produced two
  P0-shaped escalations from a metric that had already recovered. → T13.
- **F7 `WEEKLY-REPORT-NO-IMPRESSION-FLOOR-01`** — percentage deltas must be suppressed below a minimum
  impression base (suggest 50/wk). "−61.3%" on a 6-impression query nearly bought a wasted 09-05
  investigation. → T13.
- **F8 `VERIFIER-BYTE-VS-CHAR-AND-FRONTMATTER-WORDCOUNT-01`** *(Verifier, unprompted — and it caught
  me making both errors in this run)* — `wc -c` counts **bytes**, so any `metaDescription` containing
  `—`, `–` or `₹` reads 1–3 chars over and manufactures false VETOs (I raised a false VETO on
  `online-therapy-for-indians-in-usa` this way: 159 chars, 161 bytes). And `wc -w` on a whole MDX file
  counts the frontmatter — `quickAnswer`, `keyTakeaways` and all 5 FAQ answers — inflating body word
  counts by 370–560 and producing false PASSes on genuinely thin pages. Use `len()`/`wc -m` for
  chars and strip frontmatter before counting words. → T13.
- **F9 `REVIEWER-ASSIGNER-ACCEPTS-NONEXISTENT-SLUG-01`** — `logs/reviewer-load-state.json` carries
  `santanu-tripathy` (`assigned_count: 2`) while `brain/memory/reviewer-mapping.md` has zero
  references to it. A reviewer slug must only be assignable if `src/content/doctors/<slug>.mdx`
  exists. One live page already ships with no author schema because of this. → T13.

## F. VERIFIED, NO ACTION

- **Brief queue HEALTHY — no refill fired.** Two independently-derived counts agreed exactly:
  **11 shippable `/blogs/` briefs (9 Tier A / 2 Tier B)** against a floor of 6. 18 briefs target
  `/blogs/`; 16 have 404 slugs; 6 carry active DO-NOT-SHIP/NEEDS_HUMAN holds (**corrected from my
  first count of 5 — the Verifier caught that `psychology-of-love-brief.md` carries an active hold I
  had filed only under "already-live"**); 2 target live pages and are refresh briefs. Two briefs
  containing `⛔` were correctly judged NOT held — in both the marker heads a *superseded* /
  *corrected* audit block, not a live hold.
- **7 of those 11 already have authored MDX on disk** (§A). The remaining 4 unauthored:
  `online-counselling-in-hindi`, `online-counselling-in-malayalam`, `online-therapy-in-telugu`,
  `rtms-treatment-cost-in-india`.
- **Discovery FRESH** — `new-content-opportunities.json` written 2026-08-24 (Monday, its cadence).
  No `DISCOVERY STALE` in today's logs. No re-run needed. No paid-mining skip.
- **Weekly cap respected** — `max_new_content_per_week = 20`; 6/20 used. **T20 shipped 0 pages.**
  `src/**` untouched, `scripts/*.py` untouched, **nothing deleted** — everything archived.
- **Core Update status is internally contradictory and worth a correction, not an escalation.**
  Today's `gsc-validation-2026-08-28` searched and concluded the "August 2026 Core Update" is
  **NOT officially confirmed by Google** and explicitly says the 08-27 log's "confirmed" claim is
  incorrect; T10's BACKLOG header asserts "Core Update STILL LIVE (Day 3)". The disagreement drives a
  *conservative* YMYL hold, so the risk of leaving it is low — but the brain currently holds both
  claims as true. Noted for T10/T12; not escalated.

---

## RUN SUMMARY — 2026-08-28

| | |
|---|---|
| Flags collected | 11 |
| **False positives closed** | **5** — form_submitted crash · backend fail rate · PTSD cluster · executor "missed" · auto-remediation(Fri) "missed" |
| **Auto-fixed** | **4** — brain backup stall cleared + pushed (`6a746b4`) · broken reviewer reference · 7 briefs annotated · stale ref lock |
| **Escalated** | **2** — 7 undeployed pages (P0, new spec) · dead links (P1, day 3, unchanged) |
| **Filed to T13** | **4** |
| Brief queue | **11 shippable (9A/2B)** · floor 6 ✅ · no refill needed · 7 already authored |
| Pages shipped by T20 | **0** (hard constraint) |
| Verifier sub-agent | **8 claims audited — 5 UPHELD · 3 CORRECTION · 0 VETO · 6 unprompted findings — all honoured** |

**Net.** Five of eleven flags were not real, and the two loudest — a "CRITICAL on-site booking form
crash" and a backend failure rate said to block the ads restart — had both already reversed before
they were escalated. Form submissions are at 156/7d, the highest in the series; the fail rate is
6.1%, less than half the number in the alert. A third, the "SEVERE" PTSD collapse, moved in the
opposite direction: that cluster grew 140%, and the specific query behind the alarm has a six-
impression base and never left position 2.

What survived is worth the run. **T9 has not been failing to produce — it has been producing and
losing it.** Seven finished, gate-passing pages have been sitting in an uncommitted working tree
since Wednesday while ops-health reported the task as having run. The brief queue was never the
constraint; the last fifteen minutes of the pipeline is.

**Discipline note.** The Verifier corrected three of my own claims: my word counts included YAML
frontmatter (inflating by ~400 words/page), my metaDescription VETO was a byte count masquerading as
a character count, and my hold tally was 5 when it was 6. All three are the same failure as the last
four runs — *measuring something adjacent to the thing I was making a claim about*. The counter-move
held this time only because the second count was derived by a different process, not by me being
more careful. Two independent counts before any number leaves the run: keep it.


---

# 🔧 T20 AUTO-REMEDIATION — 2026-08-28 (EVENING, 20:45 IST — scheduled run)

**Context.** A T20 run already fired at 16:01 IST today. This run did **not** carry its conclusions
forward: it re-verified both open escalations against live production and audited the morning run's
own auto-fixes. That audit is where most of tonight's value came from.

Verifier sub-agent: **5 UPHELD · 3 CORRECTION · 1 VETO · 5 unprompted findings — all honoured.**
Two of my own conclusions were overturned and are recorded as such below.

## A. FALSE POSITIVES CLOSED (Rule 1) — 3

**A1. `T17-CHROME-STALL-08-28`** (logged 🔴 CRITICAL / `flag_for_human`) — **CLOSED, 2nd time.**
Two independent grounds:
- **Registry.** `cowork-tasks/task20-auto-remediation.md:51` puts "Chrome stall on Mac Mini" in the
  🟢 **AUTO-FIX** table — *"attempt Chrome restart… only escalate if restart fails twice"* — and hard
  constraint line 108 forbids escalating anything the registry can auto-fix. Filing it as
  `flag_for_human` is a registry violation independent of Chrome's actual state, and the prescribed
  restart-twice was never attempted before either escalation.
- **Live.** Browser connected (`list_connected_browsers` → 1 local macOS instance), `tabs_context_mcp`
  created a tab, two Perplexity queries ran end-to-end. The real defect reproduced directly: first
  `get_page_text` at ~30s returned only *"Searching the web · 1 completed"*; a second read at ~65s
  returned the complete answer. This is exactly the render-wait bug closed on 2026-08-21 as `T17-24`,
  which the 08-28 entry re-raises without referencing.
- **Stated limit (Verifier caveat, honoured):** T17 runs Thursday evening; this ran Friday evening. A
  successful Friday `tab_create` does not disprove a Thursday-specific disconnect, and the recorded
  symptom differs ("No text content found" on 08-21 vs "Searching the web" tonight). The defensible
  claim is *the escalation is unjustified and the render-wait bug is real and reproducible* — **not**
  that Thursday's stall was that bug.

**A2. `Best Psychologists in Bangalore` pos 13→100** — DataForSEO noise, AP8 correctly applied.
All 10 pages in today's rank-100 cohort curled: **every one returns 200**, 0.28–0.66s — nothing is
gone. GSC `doctors_psychologists-in-bangalore.json` (pulled 08-27): `signal=NOISE`, clicks
**13→15 (+15.4%)**, impressions 795→769 (−3.3%), **page avg position improved 19.3→15.3**, head query
`psychologist near me` **pos 7.4** on 531 impressions.
⚠️ **Correction to my derivation (Verifier).** I quoted a "10.6–12.5 head-query band"; that was not the
head query and understated the case. More seriously, the file's `keywords` array is **capped at 50 rows**
(clicks-desc then alphabetical, terminating at `"avinash ubaradka"`) and **the tracked query `best
psychologists in bangalore` is not in it at all.** I cited a file as ground truth for a query the file
does not contain. The conclusion holds on page-level evidence; the derivation did not. Same `rowLimit`
class as `GSC-MEASUREMENT-INTEGRITY-01`.

**A3. MODERATE `/doctors/psychologists-in-mysore` 7→11** — not escalated. Page 200, fast. **No GSC
file exists** for it under the `/doctors/` path (only stale `doctors-listings_*` pulls from June), so
per AP5/AP8 there is no cross-reference and no action is permitted. Queued for T2, not treated as real.

## B. VETOED — my own conclusion, withdrawn — 1

**"The 08-21 `/doctors/psychologists-in-bangalore` refresh has NOT failed."** Withdrawn. The GSC
windows are `08-10→08-17` (entirely pre-ship) vs `08-17→08-24`; the refresh shipped **08-21**, so the
"post" window holds **3 days** — this is not a pre/post test. Two of the three watch queries named in
`WATCH.md:1148` are truncated out of the file; the one present, `adhd therapist near me`, **moved the
wrong way (71.9→76.6)** and appears in the file's own `dropping_keywords`. And `WATCH.md:1157` says not
to close watches on drops observed in this window — which cuts both ways.
**Correct wording: no evidence of failure. W-PSYCH-BLR-20260821 stays open; verdict at 09-04.**
This is the same error class I indicted the morning run for: pre-empting an open watch's check date.

## C. AUTO-FIXED (Rule 2) — 4

**C1. 🔴 `briefs/archive/t9-shipped-2026-08-28/` renamed** →
`MISLABELLED-DO-NOT-TREAT-AS-SHIPPED-2026-08-28/`, plus a `READ-ME-FIRST.md` inside.
Created 16:25 today; the name asserts 7 briefs shipped. **None are — all 7 curl 404.** Membership is
also wrong: includes `rtms-treatment-cost-in-india` (no authored MDX), omits
`online-psychiatrist-consultation-in-tamil` (has one). Under the registry's *"200 = shipped → archive"*
rule a future run trusting the folder **name** would have dropped 7 of the 11 shippable briefs and
silently buried the current P0. Renamed via `os.rename()` (unlink is EPERM on this FUSE mount).
**Nothing deleted; top-level originals remain authoritative.**

**C2. Second brief with the non-resolving reviewer fixed.** The morning run corrected one brief and did
not sweep the queue. **`NEW-online-counselling-in-hindi-brief.md` still carried ACTIVE
`reviewer: "santanu-tripathy"`** — Tier A, unauthored, T9-shippable, i.e. live to replicate the defect
on another commercial page. Changed to `krishna-k-r` (record present; `/doctors/krishna-k-r` 200 real
profile, no redirect; cluster fit Anxiety/OCD/CBT/Psychotherapy; active-brief load 0). All **12** active
reviewer slugs in the queue were then checked against both the 59 doctor records and live HTTP —
**zero non-resolving slugs remain.**

**C3. `lastReviewed` bump REVERTED** (Verifier hard-flag, honoured). My slug swap had also set
`lastReviewed: 2026-08-28`. That field is not inert: `src/app/blogs/[slug]/page.tsx` feeds it to
`dateModified`, and `src/components/medical/ReviewerByline.tsx` renders it as the visible
*"Last reviewed {date}"*. On ship it would have published a claim that a named psychiatrist clinically
reviewed a mental-health page on 2026-08-28 — in UI **and** structured data — on a page whose body is
still an unwritten placeholder. Reverted to 2026-08-26 and filed as F11 (systemic: all 72 NEW briefs).

**C4. Dev handoff corrected.** `reports/dev-handoff-2026-08-26-dead-links.md` asserted *"None of the 6
`.mdx` files exist locally"* and that a repo-wide grep *"returns zero files."* **Both false**, re-tested
tonight: all 6 exist as untracked paths and the grep returns **6 files / 10 anchors**. The instruction
(work the remote tree) was right; the stated reason was not, and a dev who verified it would have had
grounds to discount the whole ticket. Corrected in place with the real reason (5-week-stale HEAD +
~80 untracked paths at risk).

## D. ESCALATED — 2 re-verified + 2 new — 4

**D1. 🔴 P0 `T9-UNDEPLOYED-BATCH-2026-08-26` — day 3, unchanged.** All 7 re-curled **with and without
`-L`: 404 on both**. All 7 still untracked; HEAD `feb506b`. Body words (frontmatter stripped)
**1,124–1,454**. Nothing moved in the ~5h since the morning escalation.
⚠️ Added tonight per Verifier U3: **`src/content/blogs/psychiatrist-online-consultation-india.mdx` — the
file that will actually ship — still carries `reviewer: "santanu-tripathy"`.** Only the *brief* was
corrected. BACKLOG previously read "Brief already corrected by T20", which reads as *handled*; combined
with "ship all 7 ATOMICALLY" a dev could commit the batch and reproduce the defect. BACKLOG line fixed.

**D2. 🔴 P1 `DOCTORS-LISTINGS-DEAD-LINKS-01` — day 3, unchanged.** Verifier did a full census, not a
sample: sitemap 842 URLs, **297 under `/blogs/`**, every one curled. **6 pages / 10 anchors / 9 unique
targets** — per-page counts identical to the 08-26 spec. All 9 targets 404. **6 of 9 have a `/doctors/`
200 equivalent** → blanket rewrite fixes 7 of 10; 3 need named substitutes.

**D3. 🆕 P1 `REVIEWER-NEVER-ASSIGNED-01` — 52 live blog pages carry no reviewer at all.** Full corpus,
all 297 live `/blogs/` pages: **57 emit zero `reviewedBy`**, **12 emit zero `reviewedBy` AND zero
`Person`**. Of the 57, five are the broken-slug case; the other **52 have no `reviewer:` field at all**.
An E-E-A-T authorship gap across ~18% of the blog corpus, during documented vertical volatility.
Needs a content/dev decision + a template guard. T20 cannot fix (`src/**`).

**D4. 🆕 P2 `REVIEWER-SLUG-UNRESOLVED-01` — 5 live pages; mechanism fully established.**
`santanu-tripathy` resolves to nothing: no `src/content/doctors/santanu-tripathy.mdx` among 59 records;
`https://www.mindtalk.in/doctors/santanu-tripathy` **301 → `/doctors`** (generic index). Exactly 6 local
MDX use it; **5 are live and all 5 emit `reviewedBy` = 0 — 100% correlation, no counterexample.**
Upstream cause: `logs/reviewer-load-state.json` lists `santanu-tripathy` with `assigned_count: 2` while
`reviewer-mapping.md` has no such reviewer — **the auto-assigner draws from a registry containing a
reviewer with no doctor page.**

⚠️ **CORRECTION — my original framing of D3/D4 was wrong and the Verifier caught it.** I reported
"5 of 16 sampled pages emit no reviewer" and named `relationship-stress`, `eft-tapping`,
`mental-exhaustion`, `sleep-schedule` alongside `drug-addiction-symptoms`. **Four of those five slugs do
not exist as live URLs** (the real pages are `how-to-deal-with-relationship-stress`,
`what-is-eft-tapping-guide`, `mental-exhaustion-symptoms-causes`,
`how-to-fix-your-sleep-schedule-quickly`) — I curled 404s and read the resulting zeros as evidence.
Only `drug-addiction-symptoms` was real. I also asserted one mechanism for all five when there are two,
and the larger one (52 pages, never assigned) I had not found at all. **Root error: I did not check
status codes in the sweep** — the identical mistake as the `-L` trap below, one hour apart.

## E. FILED — not Kushal's — 4

- **`F10 REGISTRY-200-EQUALS-SHIPPED-UNSAFE-FOR-REFRESH-BRIEFS-01`** — the stale-brief rule
  ("200 = shipped → archive") is unsafe for REFRESH briefs, which legitimately target live pages. Two
  in the queue (`guide-to-reset-your-sleep-cycle`, `psychology-of-love`) return 200 and are valid; the
  literal rule would have destroyed them. Amend to **"200 = shipped, for NEW briefs only."** My
  deviation was correct on the merits but is a deviation from the registry text, so it is documented
  rather than left as an undocumented judgement call.
- **`F11 BRIEF-LASTREVIEWED-FABRICATES-CLINICAL-DATE-01`** — all 72 NEW briefs carry `lastReviewed` =
  their generation date, which ships as a visible + schema clinical-review claim. See C3.
- **`F12 T20-DAY-COUNT-EPOCH-01`** — the dead-links flag was "day 3" this morning and "day 4" from me
  tonight, same calendar day. It is an age counter on a live escalation. Fix the epoch. (Standardised
  to **day 3** tonight.)
- **`F13 VERIFIER-WORDCOUNT-STILL-UNRESOLVED-01`** — **three incompatible ranges now exist for the same
  7 files**: BACKLOG 1,085–1,455; me 1,123–1,453; Verifier 1,124–1,454. `F8` is filed but unfixed;
  until one method lands in `VERIFIER.md` §5 the word-count gate is not reproducible.

## F. VERIFIED, NO ACTION

- **Core Update label** — corrected in BACKLOG with the **hold deliberately left on**. Verified two
  ways (today's own `gsc-validation-2026-08-28` Step 7 + independent web search): no confirmed August
  2026 update; last confirmed ranking change is the **June 2026 spam update, ended 26 June**. Per the
  Verifier's two conditions, the correction (a) restates the hold's *real* basis — third-party
  healthcare-vertical volatility + 5 `algo_watch=True` confirmed drops — so no future run reads "the
  reason was false" and lifts it, and (b) surfaces that **~09-05 now has no anchor** and T10 must
  re-set the settle date. Lifting the hold would unpark the YMYL queue, W38, CHATGPT-AEO and
  PTSD-CLUSTER in one move — **T10's/Kushal's call, not T20's.**
- **Brief queue** — 75 briefs, 0 untiered, 18 `/blogs/` tiered, 16×404 + 2×200 (both REFRESH, correctly
  live), 5 durable `⛔ DO NOT SHIP` blocks → **11 shippable (9A/2B) vs floor 6 → no refill fired.**
  Counted twice by different methods; Verifier re-derived all of it independently and confirmed every
  figure. **Leading indicator noted:** only **4** are actually authorable next run — but with 57 Tier A
  `/doctors/` briefs also queued (~68 total), the system is **not supply-constrained; the ship stage is.**
- **AI citation data** — 2 of 40 cells recovered while proving Chrome works. Q1 `best mental health
  platform india` ❌ **absent, 4th consecutive week**, with **Amaha now cited with its Bengaluru centres
  enumerated** — direct encroachment on Mindtalk's home city. Q3 `psychiatrist near me bangalore` ✅
  **cited, retained.** Logged to `ai-citation-history.md`, superseding the "all engines SKIPPED" line.

## HARD CONSTRAINTS — ALL CLEAN (Verifier-audited)

| Constraint | Verdict | Evidence |
|---|---|---|
| No edits to `src/**` | ✅ | Zero src files modified after 16:00. The 30 files at mtime 15:36:29 are a sub-second `checkout: moving from main to main` artifact in the reflog. |
| No edits to `scripts/*.py` | ✅ | `find scripts -name '*.py' -newermt 2026-08-28` → 0. |
| No push to website repo | ✅ | HEAD `feb506b`, unchanged; no commits or pushes in reflog today. |
| Nothing deleted | ✅ | Archive dir **renamed**, not removed; 293 archived briefs intact; today's copies coexist with their originals. |
| No page shipped | ✅ | All 7 batch URLs 404; no new commits. |
| Weekly cap (`max_new_content_per_week: 20`) | ✅ | 0 pages shipped this week. |

## RUN SUMMARY — 2026-08-28 (evening)

| | |
|---|---|
| Flags collected | 9 |
| **False positives closed** | **3** — Chrome stall CRITICAL (2nd closure) · psychologists-in-bangalore rank-100 · mysore MODERATE (no GSC ref) |
| **Auto-fixed** | **4** — mislabelled archive dir renamed · 2nd bad reviewer slug swept · fabricated `lastReviewed` reverted · dev handoff false statement corrected |
| **Escalated** | **4** — P0 undeployed batch (day 3, re-verified) · P1 dead links (day 3, re-verified) · 🆕 52 pages with no reviewer · 🆕 5 pages with unresolved reviewer slug |
| **Filed to T13** | **4** (F10–F13) |
| Brief queue | **11 shippable (9A/2B)** · floor 6 ✅ · no refill · 4 authorable next run |
| Pages shipped by T20 | **0** (hard constraint) |
| AI citation cells recovered | **2 of 40** (Q1 ❌ absent 4th wk · Q3 ✅ retained) |
| Verifier sub-agent | **5 UPHELD · 3 CORRECTION · 1 VETO · 5 unprompted findings — all honoured** |

**Net.** The morning run's two escalations are both real and both unmoved, so the day's headline
stands: seven finished pages have been sitting uncommitted since Wednesday and the bottleneck is the
last fifteen minutes of the pipeline, not supply. What this run added came from auditing that run
rather than trusting it — a mislabelled archive directory that would have silently deleted 7 of the 11
shippable briefs and buried the P0; a second brief still carrying the reviewer slug the morning fixed
in only one place; and a false statement in the dev handoff that would have let a dev close the
dead-links ticket as already-fixed. None of those were on any flag list.

The reviewer thread turned out to be the largest finding and the one I got most wrong. Chasing one bad
slug surfaced that **52 live blog pages carry no reviewer at all** — an E-E-A-T gap an order of
magnitude bigger than the defect that led me to it — but my own census was wrong on 4 of the 5 pages I
named, because I curled slugs that do not exist and read the resulting zeros as findings.

**Discipline note.** Twice tonight I measured the wrong thing and reached a confident wrong conclusion:
`curl -L` followed a 301 to the generic `/doctors` index and I read the resulting 200 as "the page
exists", nearly filing a correction against a morning finding that was right; and I counted
`reviewedBy` on four URLs that were 404s. Both are the same failure the last five runs recorded —
*measuring something adjacent to the thing I was claiming.* The first was caught by re-reading the
primary source before writing, the second only by the Verifier. **Concrete rule for next run: any curl
used as evidence must record its status code without `-L`, and any page-level census must assert 200
before it counts anything on the page.** Two independent counts is necessary and was not sufficient —
both of my counts were downstream of the same bad URL list.
