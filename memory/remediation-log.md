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
