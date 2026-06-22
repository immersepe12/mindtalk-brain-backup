# WATCH — Active Observations

**Owner:** Strategist adds; Learner closes.
**Format:** One row per page/query under observation. Stale entries (>60 days) auto-pruned.

| Watch ID | URL | Query | Type | Opened | Action that triggered watch | Expected outcome | Check on | Status |
|---|---|---|---|---|---|---|---|---|
| W1 | /illnesses/dementia | dementia treatment | YMYL_recovery | 2026-06-09 | Sprint A (commit `270cf0c`) | impressions +15-25% | 2026-06-23 | open |
| W2 | /illnesses/alzheimers | alzheimers treatment | YMYL_recovery | 2026-06-09 | Sprint A | +15-25% | 2026-06-23 | open |
| W3 | /illnesses/posttraumatic-stress-disorder-ptsd | ptsd | YMYL_recovery | 2026-06-09 | Sprint A | +15-25% | 2026-06-23 | open |
| W4 | /illnesses/drug-addiction | drug addiction | YMYL_recovery | 2026-06-09 | Sprint A | +15-25% | 2026-06-23 | open |
| W5 | /treatments/eclectic-therapy | eclectic therapy | YMYL_recovery | 2026-06-09 | Sprint A | +15-25% | 2026-06-23 | open |
| W6 | /treatments/biofeedback-therapy | biofeedback therapy | YMYL_recovery | 2026-06-09 | Sprint A | +15-25% | 2026-06-23 | open |
| W7 | /blogs/understanding-dominant-personality-and-dominating-nature | dominant personality | AI_overview_defense | 2026-06-09 | Sprint B/1 (commit `aa5e3b9`) | impressions 1.3k → 3.5k | 2026-06-23 | open |
| W8 | /blogs/20-quotes-to-inspire-healthy-relationships | relationship quotes | AI_overview_defense | 2026-06-09 | Sprint B/2 (`5dfe080`) | 1.7k → 4k | 2026-06-23 | open |
| W9 | /blogs/emotional-distress-all-you-need-to-know | emotional distress | AI_overview_defense | 2026-06-09 | Sprint B/3 (`c1e0d67`) | 2.2k → 5k | 2026-06-23 | open |
| W10 | top 20 pages from W12 analyst | (multiple) | CTR_metarewrite | 2026-06-09 | Sprint C (`7c3c2c4`) | +2,180 clicks/wk total | 2026-06-23 | open |
| W11 | / (homepage) | mindtalk | conversion_redesign | 2026-06-12 | Homepage app-first (merge `c35193f`) | "Get the App" becomes #1 hero CTA | 2026-06-19 | open — ⏸ **DEFERRED by Learner 06-21** (Mixpanel access blocked; no rank/impr harm; verdict unmeasurable, not failed — `memory/experiments/deferred-W11-2026-06-21.md`) |
| W15 | /blogs/understanding-anxiety-neurosis | anxiety neurosis | CTR_metarewrite | 2026-06-16 | Sprint C-2 clean-target round (`579bb7c`) | CTR ≥ 3% (from 0.9% at pos 4.6) | 2026-06-30 | open |
| W12 | /blogs/couple-therapy-techniques | couple therapy techniques | NEW_indexation | 2026-06-17 | Auto-ship NEW blog (`549dac3`) | indexed + impressing within 4-6wk | 2026-07-01 | scheduled (check task created 06-19, Executor T11) |
| W13 | /blogs/how-to-find-a-therapist-for-ocd | how to find a therapist for ocd | NEW_indexation | 2026-06-17 | Auto-ship NEW blog (`549dac3`) | indexed + impressing within 4-6wk | 2026-07-01 | scheduled (check task created 06-19, Executor T11) |
| W14 | /blogs/how-to-find-a-therapist-in-india | how to find a therapist in india | NEW_indexation | 2026-06-17 | Auto-ship NEW blog (`549dac3`) | indexed + impressing within 4-6wk | 2026-07-01 | scheduled (check task created 06-19, Executor T11) |
| W16 | (10 URLs at exactly pos 100) | data-quality | indexation_reconcile | 2026-06-17 | DataForSEO 06-16 quarantine (data-quality gate) | recover to prior pos on 06-18 pull (= confirmed noise) | 2026-06-18 | ✅ **CLOSED 2026-06-18 — confirmed DataForSEO noise.** The 06-16 ten recovered (none in today's pos-100 set); today's 15 pos-100 URLs are a *different* set → exact-100 rotates run-to-run = API noise, not deindex. "≥4 still at 100" NOT met. No action (AP5). |

## Pending observations (activate as watches when condition met) — added 2026-06-15

| Item | Condition to activate | Then |
|---|---|---|
| ~~3 NEW blogs (couple-therapy-techniques, how-to-find-a-therapist-for-ocd, how-to-find-a-therapist-in-india)~~ ✅ **ACTIVATED 2026-06-17** | Shipped live via `549dac3` (Task 9 manual completion). Vercel block resolved. | **W12-W14 opened** (above), indexation watch, +14d check 2026-07-01. |
| ~~10 quarantined pos-100 URLs (W16)~~ ✅ **CLOSED 2026-06-18** | Thu 2026-06-18 daily rank pull re-checked them | **Confirmed DataForSEO noise.** 06-16 ten recovered (none in 06-18 pos-100 set); 06-18 produced a *different* 15-URL pos-100 set → pattern rotates = API noise. W16 closed, no action (AP5/P5). |
| ~~15 quarantined pos-100 URLs (06-18 set)~~ ✅ **CLOSED 2026-06-19 — confirmed DataForSEO noise** | Fri 2026-06-19 daily rank pull re-checked them | **Zero overlap** between the 06-18 set (mood-disorder, narrative-therapy, anxiety-symptoms-in-men …) and the 06-19 set (art-therapy, abandonment-issues, cbt-for-insomnia …) — `comm -12` empty. "Same ≥4 still at 100" escalation NOT met → exact-100 set rotates run-to-run = API/parsing artefact, not deindex. No action (AP5/P5, **4th** confirmation). |
| ~~15 quarantined pos-100 URLs (06-19 set: art-therapy, abandonment-issues, cbt-for-insomnia, eustress-distress, anxiety-coping-kids, anxious-attachment, hsdd, mindfulness-stress, ptsd-treatment-and-recovery, teen-depression, fear-ending-relationship, double-empathy-autism, panic-attack-calming, psychologists-in-bangalore, therapists-in-hyderabad)~~ ✅ **CLOSED 2026-06-22 — confirmed DataForSEO noise (5th confirmation)** | Mon 2026-06-22 daily rank pull re-checked them | **Zero overlap** between the 06-19 set and the 06-22 pos-100 set (13 URLs) — `comm -12` empty. "Same ≥4 still at 100" escalation NOT met → exact-100 rotates run-to-run = API/parsing artefact, not deindex. Independent corroboration: sleep-disorder-tests reports "pos 100" today yet GSC shows it +32% impr (228→301). No action (AP8/P5, **5th** confirmation). |
| 13 NEW quarantined pos-100 URLs (06-22 set: emotionally-focused-therapy-eft, music-therapy, positive-psychology, how-to-control-anger-in-relationship, how-to-manage-bipolar-disorder-daily, how-to-manage-stress-for-mental-health, male-vs-female-depression, managing-teen-depression, sleep-disorder-tests, stress-management-everything, stress-management-mastering, new-years-resolutions, tips-to-overcome-mental-exhaustion) | **Re-check next pull Tue 2026-06-23** (rank-pull cron Mon/Tue/Thu/Fri). Strategist 06-22: assume rotating noise per AP8 (5 consecutive confirmations now). | If the *same* ≥4 URLs report exactly 100 AGAIN on 06-23 → escalate to genuine deindex investigation. If recovered (expected, per AP8) → confirmed noise, no watch needed. Assume noise until the 06-23 pull confirms. |
| **Sleep-disorder + stress cluster GSC slide (06-22 weekly report)** — 12 cluster avg-position drops, 5 sleep-related: /illnesses/sleep-disorder (474 impr), circadian-rhythm, delayed-sleep-phase, sleep-talking, ocd-thoughts, top-10-stressors (263), migraine-stress (304), positive-psychology, anger-in-relationship, save-marriage, conduct-disorder, drug-addiction (450). All `gsc_validation: PENDING`. | **Task 2 GSC-validates the 12 flags Tue 06-23**; then read-only cluster diagnostic (BACKLOG #14) audits cannibalization + internal-link overlap across the sleep blogs. | If GSC CONFIRMS the slide → #14 read-only audit (no refresh — ALGO_WATCH + sleep-disorder/DBT in pro-input skip-list). If GSC = NOISE (as the 06-16 sleep-cluster read was) → close, no action. Likely partly composition ("what is a life coach" 9,429-impr page-2 surge dragged site avg pos 10.1→11.3). Validate-first; **no refresh pre-06-23 Sprint reads**. |
| ~~Sleep cluster: /blogs/how-anxiety-affects-sleep + /blogs/cognitive-behavioral-therapy-for-insomnia~~ ✅ **CLOSED 2026-06-16** | Confirmed via 06-16 GSC re-pull + cluster-history + git log (BACKLOG #1, Executor T11) | **DataForSEO tracker noise, NOT deindex.** All 3 siblings indexed; avg pos 32.8/10.1/41.5, *improved* WoW; signal=NOISE. CBT-i had its best week of the series (348 impr, pos 15.0, CTR 1.8%) inside the alleged-drop window. No recovery watch opened — no action needed. Log: `brain/memory/experiments/investigation-sleep-cluster-2026-06-16.md` |
| /treatments/life-coach-therapy | RECOVERY_PARTIAL, recheck 2026-06-25 | Learner evaluates "what is a life coach" + siblings; BACKLOG #6 SERP read feeds it |
| W11 homepage (check was due 2026-06-19) | Mixpanel access is BLOCKED (`memory/mixpanel-access-blocked.md`) | **Still deferred as of 06-20** — no homepage rank/impr regression in signals; full "Get the App = #1 hero CTA" conversion verdict remains **deferred** until Mixpanel MCP restored. Next conversion data flows from T15 (Wed 06-24) + T19 (Wed 06-24) *if* access is restored by then. Watch stays open; no action. |

## Closing rules

- Open watch ≥ check date → Learner runs evaluation
- 🟢 RECOVERED (within target) → log to PRINCIPLES.md, close watch
- 🟡 PARTIAL → extend 14 more days, note in BRAIN.md
- 🔴 FAILED → log to ANTI-PATTERNS.md or add follow-up brief to BACKLOG.md
- ⚫ WORSE → URGENT alert + escalate to manual review

## 2026-06-16 — Dry-begging CTR meta-rewrite (14-day)

- **URL:** /blogs/understanding-dry-begging-psychology-behind-indirect-requests
- **Hypothesis:** Meta-only rewrite lifts CTR on surging head term without body changes
- **Baseline (2026-06-15 weekly report):** 4,560 combined impr/wk (dry begging + dry begging meaning), positions 4.7-4.9, CTR ~0.4-0.6%
- **Target:** CTR ≥ 3% on "dry begging" head term
- **Expected impact:** +100-300 clicks/wk
- **Verdict due:** 2026-06-30 (14-day check)
- **Status:** ⚫ NOT FIRED — superseded. Page was already CTR-rewritten on 2026-06-09 (`7c3c2c4`, the W10 top-20 batch) and is inside the 14-day pause + open W10 watch. Re-rewriting would overwrite an in-flight experiment and muddy attribution. Sprint C-2 redirected to a genuinely clean target (W15, anxiety-neurosis) instead. Re-evaluate dry-begging via W10 on 2026-06-23.

## 2026-06-16 — Anxiety-neurosis CTR meta-rewrite (14-day) [W15]

- **URL:** /blogs/understanding-anxiety-neurosis
- **Commit:** `579bb7c` on branch `feat/ctr-harvest-2026-06` (meta-only; body/H1/schema/reviewer unchanged)
- **Hypothesis:** Meta-only rewrite lifts CTR on a page-1 query whose title lacked a click hook
- **Baseline (queries-2026-06-15.csv):** "anxiety neurosis" 764 impr/wk, position 4.6 (improving from 5.7), CTR 0.9%
- **Change:** title → "Anxiety Neurosis (GAD): Symptoms, Causes & Treatment | Mindtalk"; description leads with the GAD definition instead of "Explore the comprehensive overview of…"
- **Target:** CTR ≥ 3% on "anxiety neurosis"
- **Expected impact:** +15-25 clicks/wk from this query (smaller pool than dry-begging; clean-target substitute)
- **Selection note:** Chosen after excluding the entire W10 06-09 top-20 set (14-day pause), dry-begging (open watch), and life-coach (hard block). Page not under any watch, not algo_watch HOLD, last modified 2026-05-25.
- **Verdict due:** 2026-06-30 (14-day check)
- **Status:** OPEN

## ⚠ 2026-06-16 — Vercel deploy attribution block (INFRASTRUCTURE)

**Discovered:** During anxiety-neurosis CTR meta-rewrite ship (W15)

**Symptom:** Vercel blocks deployment with error "The deployment was blocked because Venkat-P7 does not have a Vercel account linked to their GitHub account."

**Affected commits already on origin/main:**
- `579bb7c` — anxiety-neurosis CTR meta-rewrite (the W15 target — NOT YET LIVE)
- `d988260` — merge commit

**Most likely cause:** Venkat-P7 owns the Vercel GitHub App installation on the immersepe12 GitHub org / mindtalk repo. Vercel attributes ALL webhook-triggered deploys to the integration owner, regardless of commit author or pusher.

**This blocks the entire autonomous loop:**
- T9 Auto-Ship NEW blogs (next: Tue 3 PM) — will hit same block
- T11 Executor refresh ships (next: Tue 4:30 PM) — same
- Any manual Claude Code ships — same

**W15 status correction:** Watch is OPEN but ⚠ PENDING DEPLOY — anxiety-neurosis page is NOT live yet. 14-day clock has NOT started. Resume when Vercel deploys.

**Resolution paths (Kushal investigating):**
1. Reconnect Vercel→GitHub integration under Kushal's Vercel account
2. Have Venkat-P7 activate their Vercel account (free, 30 sec)
3. Manual redeploy from Vercel UI as one-off unblock today

**Status:** OPEN — investigation in progress.

## ✅ 2026-06-16 14:25 IST — Vercel attribution block RESOLVED

**Root cause confirmed:** Local `.git/config` in mindtalk repo had `user.email = kushal@cadabams.com`. That email wasn't verified on Kushal's `immersepe12` GitHub account (which uses `kushal@exar.fit`). GitHub falls back to mapping the email to whoever DOES have it verified — a user called "Venkat-P7" — which is either Kushal's forgotten old GitHub identity or a Cadabams team member. Vercel sees Venkat-P7 as the commit author, blocks because they don't have a Vercel account on the immersepe12 team.

**Fix applied (2026-06-16 14:25 IST):**
1. Local repo config updated: `user.email = kushal@exar.fit` (still keeps `user.name = Cowork Task 9 Auto-Ship` for traceability)
2. Empty commit `89e293a` pushed to main as new HEAD authored by Kushal
3. Vercel re-triggered → deployment proceeding

**W15 status:** PENDING DEPLOY → expected to flip to OPEN once Vercel confirms `89e293a` deploys successfully. Anxiety-neurosis meta change rides along since `579bb7c` is now in main's history being deployed.

**Cleanup needed (not blocking):**
- Run audit across all Cowork-managed repos to verify they don't have the same `cadabams.com` email override
- Investigate https://github.com/Venkat-P7 — determine if it's a real person or Kushal's forgotten old account

**Loop status:** All future Cowork-driven commits in this repo (T9, T11, T16, etc.) will now use kushal@exar.fit → mapped to immersepe12 → Vercel accepts. The autonomous deploy pipeline is unblocked.

## ✅ 2026-06-16 14:35 IST — W15 LIVE + ticking

Verified deployed via direct fetch of https://www.mindtalk.in/blogs/understanding-anxiety-neurosis:
- title: "Anxiety Neurosis (GAD): Symptoms, Causes & Treatment | Mindtalk" ✅
- meta description: "Anxiety neurosis is an older term for generalised anxiety disorder (GAD): chronic worry, restlessness and tension. Understand symptoms, causes & treatment." ✅
- og:title, og:description, twitter:title, twitter:description all match ✅

14-day clock: STARTED 2026-06-16 14:35 IST. Verdict due 2026-06-30.

Vercel attribution block: RESOLVED — empty commit 89e293a triggered fresh deploy, new commit author kushal@exar.fit mapped to immersepe12 GitHub on the Vercel team. Deploy proceeded normally. The full autonomous loop deploy pipeline is unblocked.

T9 Auto-Ship at 15:06 IST (in 30 min) is now expected to ship cleanly. T11 Executor at 16:35 IST same.

## 2026-06-21 — Learner weekly evaluation stamp

**Watches with check date in the past 7 days (06-15 → 06-21):** 2 — W11 (due 06-19) and W16 (due 06-18).

- **W11 (homepage conversion)** → ⏸ **DEFERRED** — Mixpanel access blocked, verdict unmeasurable (not a strategy failure). No rank/impr harm. Stays open. Log: `memory/experiments/deferred-W11-2026-06-21.md`.
- **W16 (10 pos-100 URLs)** → already ✅ CLOSED 06-18 by daily reconcile (confirmed DataForSEO noise). No re-close needed.

**No watches closed on the merits this week** → recovery-rate denominator unchanged. The first real recovery reads (Sprint A/B/C, W1-W10) land **2026-06-23**; W15 06-30; W12-W14 07-01.

**Pattern codified this run:** the exact-position-100 DataForSEO sentinel is now its own anti-pattern (**AP8**) — 3+ closed confirmations (sleep-cluster 06-16, W16 06-18, 06-19 set reconcile). See ANTI-PATTERNS.md.

**Escalation check:** 0 watches verdicted 🔴/⚫ this week → no `⚠ LEARNER FLAG`.

## 2026-06-22 — Strategist daily stamp (Monday)

**Watch board:** 15 open. **W1-W10 (Sprint A/B/C) fire their 14-day checks TOMORROW (06-23)** — the quarter's pivotal read. W15 (anxiety-neurosis CTR) due 06-30. W12-W14 (NEW-blog indexation) due 07-01. W11 (homepage) stays ⏸ deferred (Mixpanel blocked). None breached today.

**Closed today:** 06-19 pos-100 set → confirmed DataForSEO noise (5th AP8 confirmation; zero overlap with the 06-22 set, `comm -12` empty).

**Opened today:** (1) 06-22 pos-100 set (13 URLs) → re-check Tue 06-23, assume rotating noise per AP8. (2) Sleep-disorder + stress cluster GSC slide (12 cluster drops, 5 sleep) → GSC-validation pending Task 2 06-23, then read-only diagnostic #14. No refresh (ALGO_WATCH + pro-input skip-list + prior 06-16 noise precedent).

**Escalation check:** 0 CRITICAL/MAJOR daily drops; 0 watches breached; broad cluster slide is validation-pending + likely composition (life-coach head-term surge). No `⚠ STRATEGIST FLAG`.
