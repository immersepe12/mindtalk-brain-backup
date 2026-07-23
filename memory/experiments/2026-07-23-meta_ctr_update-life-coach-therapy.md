# meta_ctr_update on /treatments/life-coach-therapy — 2026-07-23

## What we did
Executed LIFE-COACH-CTR-01 (score 125, highest on BACKLOG): P11 meta title + keyword-forward description + FAQ H3 upgrade on `/treatments/life-coach-therapy`.

**Branch:** `feat/exec-ctr-life-coach-therapy-2026-07-23`
**Commit:** `675dc26`
**Push method:** PAT push of feature branch directly to main (`feat/exec-ctr-life-coach-therapy-2026-07-23:main`) — standard git checkout and merge both blocked by FUSE EPERM on local unlink of MDX file. Same infrastructure constraint as T9 2026-07-14.

### Changes made

**Meta title** (65 chars):
- Before: `Life Coach Therapy: Types, Benefits, and How it Works - Mindtalk`
- After: `What Is a Life Coach? 7 Types, Benefits & How It Works | Mindtalk`
- Pattern: P11 (number added = Sprint C confirmed winner), keyword front-loaded, `|` separator

**Meta description** (159 chars):
- Before: `Discover what a life coach does, types of coaching, and how it differs from therapy. Get expert life coaching at Mindtalk in Bangalore, Hyderabad & Mysore.`
- After: `What does a life coach do? Explore 7 types, benefits & how coaching differs from therapy. Book a session at Mindtalk — trusted mental health platform in India.`
- Pattern: keyword-forward, value prop, CTA, national (not city-list)

**FAQ format** (5 questions):
- Before: `**Q: ...** **A: ...**` bold format (extractFaqs() ignores this — no FAQ schema output)
- After: `### Question text` H3 format (extractFaqs() picks this up → FAQPage JSON-LD emits)
- Questions: what does a life coach do · life coach vs therapist · cost in India · anxiety/depression · when to choose coaching vs therapy

## AP6 build gate — infrastructure fallback
`npm run build` failed 4 times with FUSE EPERM on `.next/` files (cannot unlink on FUSE mount). This is the same recurring blocker from T9 2026-07-14. Established precedent: Vercel prod HTTP 200 serves as AP6 confirmation when local build is FUSE-blocked. Push made; Vercel auto-deploy in progress.

## Expected outcome
- CTR: 0.02% → ≥0.3% = +65 clicks/wk minimum target (at 21,757 impr/wk baseline)
- FAQ schema: FAQPage JSON-LD now emits → PAA box capture opportunity
- Watch period: 14 days → check 2026-08-06 (W23)

## Watch
W23 — check 2026-08-06. Evaluate: GSC CTR for "what is a life coach" query group, click delta vs baseline 5 clicks/wk.

## AP6 / AP10 outcome — CORRECTED (see below)
- Vercel deployment `dpl_EgXFWBztGv95pWTBR375vciecMBj` → **READY** ✅ (commit `e1cc784`)
- Initial AP10 check (curl for `<title>`) showed the OLD title — attributed to CDN propagation delay at the time. **This was wrong.** Re-verification via GitHub's git Trees API (not just curl/Vercel status) found that commit `675dc26`'s change to `life-coach-therapy.mdx` was NOT actually present in `e1cc784`'s tree, despite `e1cc784` correctly listing `675dc26` as its git parent. The follow-up fix commit (`e1cc784`, made to resolve the rtms-treatment MDX bug) was built from a stale local working tree — almost certainly a side effect of the FUSE-recovery maneuvers earlier in the session (checkout failures, `.next` renames, `HEAD.lock` clearing) — that no longer had 675dc26's uncommitted local file state. Git allows a commit's parent pointer and its actual tree content to diverge like this; `git commit` records whatever's in the working tree/index at commit time, not "parent tree + intended diff."

### Corrective action (2026-07-23, same day)
Re-applied the identical diff directly via GitHub's Git Data API (blob → tree → commit → ref), bypassing the broken local checkout entirely:
- New blob sha `2032bc56b211296e6dd263e63dfd8504cf2a756c` — cross-checked against the ORIGINAL 675dc26 diff's predicted "after" blob hash (`2032bc5...`) — **exact match**, confirming the reconstructed content is byte-for-byte identical to what should have shipped originally.
- New commit: **`6d2fe76`** (parent = e1cc784, i.e. current main HEAD at the time).
- Verified BEFORE declaring success, using three independent checks: (1) git Trees API re-queried post-push — main HEAD's blob for this path matches the new hash; (2) Vercel deployment `dpl_JS6Xjh8xBM9cqRKJj1tCAnW2BwmQ` reached READY; (3) live curl against `https://www.mindtalk.in/treatments/life-coach-therapy` — both `<title>` and meta description now show the correct P11 copy.
- Slack correction posted (ts: 1784797770.923619) explaining the discrepancy to Kushal, who had asked directly whether both pushed commits were actually live — that question is what surfaced this.

**The live/authoritative commit for this action is `6d2fe76`, not `675dc26`.**

## Bonus fix included in this push
Discovered during run: `/blogs/what-is-rtms-treatment` had a pre-existing MDX syntax error (`<0.1%` on line 131 — MDX parses `<` as JSX element start, `0` is invalid tag-name character) that had been causing ALL Vercel builds to ERROR since T9 merge on 07-21 (`feb506b`). Production was pinned at `269e387` (07-22). Fixed with `&lt;0.1%` in commit `e1cc784`. This means the 5 T9 Jul-21 blogs (what-is-biofeedback-therapy, what-is-rtms-treatment, how-to-choose-de-addiction, what-is-act-therapy, common-relationship-issues) deployed to production for the first time via this push.

## Notes
- Verifier: APPROVE (AP3 formally N/A for meta_ctr_update; AP4 clear; no clinical claims; score 125)
- FUSE EPERM workaround: `os.rename(.next, .next.bak)` then background FUSE watcher — still blocked because FUSE creates new unlink-blocked files during build process
- PAT push confirmed: remote SHA `675dc263f3cc633f2992ad12948345817802d38b` = local HEAD `675dc26` ✅ (this was true — the commit itself was correct; the problem was a LATER commit losing this change from the tree)
- Commit chain (as intended, but see correction above): `675dc26` (LIFE-COACH-CTR-01) → `e1cc784` (rtms-treatment MDX fix, silently dropped 675dc26's change) → `6d2fe76` (corrective re-apply via GitHub Git Data API) → all on main

## Process lesson (important for future FUSE-fallback runs)
When local build is FUSE-blocked and a PAT/API push is the only path to production, **"Vercel deployment READY" proves the tree built successfully — it does not prove the tree contains the changes you intended.** Especially risky when a SECOND commit is created on top of a FUSE-affected local session (e.g., a follow-up bug fix), since that commit's working tree may have silently lost earlier uncommitted local state. Going forward: after any FUSE-fallback push, verify the actual git blob/tree content at the deployed commit via GitHub's Trees API (not Contents/raw API — those can lag briefly; Trees API via direct SHA was reliable here) before marking the action complete, not just Vercel status + a single curl.
