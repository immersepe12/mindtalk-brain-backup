# ANTI-PATTERNS — What NOT to do

**Read by:** Strategist before every decision. Action MUST NOT match any anti-pattern.
**Written by:** Learner (Task 12) after closed watch windows that showed harm.

---

## AP1. Never bulk-rewrite ranking content without staged rollout
- Counter-example seen: 2026-04-14 doctor URL migration redirected 80% of URLs to 404 pages. Site lost ~376 unique URLs from index. Took 24 days + middleware fix to recover.
- Rule: any change affecting >10 pages must ship to a 10% sample first; check rank stability over 7 days before bulk rollout.

## AP2. Never wrap consult.cadabams.com destinations in `/login?returnTo=`
- Counter-example: original `buildReturnToUrl` did this; the auth-redirect chain stripped the `returnTo` param entirely. Every CTA across 64+ pages went to a generic login page.
- Rule: use direct destination URLs only. Let the target site handle auth flow internally.

## AP3. Never auto-ship YMYL content without prior clinical sign-off
- Counter-example: hypothetical — auto-shipping an illness brief without clinical review could publish incorrect medical guidance, harming users and getting demoted by Google.
- Rule: auto-shipper script must skip any brief targeting `/illnesses/*`, `/treatments/*`, or suicide/self-harm topics **UNLESS** the brief frontmatter has a valid `clinical_reviewer_signed_off` field — i.e., a named clinician + date ≤90 days old. With a valid sign-off, auto-ship proceeds (the clinician has already reviewed the content; the ship is just the publish step).
- Updated 2026-06-26: previously a hard block (Option A). Moved to conditional sign-off gate (Option B) after Sprint A (55 YMYL pages, all with named reviewers) proved the named-reviewer pattern works and the hard block created throughput bottleneck (T9 shipped 0/20 W26 — every queued brief was YMYL with no path to ship).
- Verifier check (T9 step 5): `if path matches /illnesses/* or /treatments/* or suicide-safety topic: require frontmatter.clinical_reviewer_signed_off.reviewer + frontmatter.clinical_reviewer_signed_off.date AND date ≤ 90 days ago. If missing or expired → VETO with reason "AP3: missing clinical sign-off".`

## AP4. Never refresh a page within 14 days of its last refresh
- Counter-example: if life-coach-therapy was refreshed 2026-05-28 (commit `58b7e39`), don't refresh again until 2026-06-11 (first opportunity).
- Rule: check `last_modified` of target MDX before queuing refresh.

## AP5. Never assume a rank "drop" is real without checking spike vs baseline
- Counter-example: 2026-06-02 "Reduce Stress Daily" -92% — was actually regression to mean after spike, position improved during the "drop"
- Rule: if the prior week's value is >3x the 4-week median, treat the "drop" as normalization and skip action.

## AP6. Never push to main without successful build
- Counter-example: hypothetical malformed MDX would break the entire site build and Vercel deploy, taking everything offline.
- Rule: hard `npm run build` gate before every push. If build fails, revert the offending commit and quarantine the brief.

## AP7. Never queue brief generation for a URL already in BRIEF_CREATED status
- Counter-example: Task 2 was re-confirming /treatments/psychotherapy 1 day after its brief was created, would have caused duplicate briefs with conflicting recommendations.
- Rule: workflow already handles this (logged 2026-06-12) — Strategist double-checks tracking-db before fire.

## AP8. Never treat an exact position-100 reading from the DataForSEO single-keyword tracker as a deindex/drop signal
- Specific sub-case of AP5. "Position 100" from the DataForSEO single-keyword tracker is a "not-in-top-100-on-this-pull" **sentinel value**, not a measured Google rank. The quarantined exact-100 set **rotates run-to-run** (different URLs every pull) — proof it is an API/parsing artefact, not real ranking movement.
- Evidence (3+ closed confirmations):
  1. **Sleep-cluster investigation 2026-06-16** — 3 siblings flagged at pos 100; GSC re-pull found all indexed, positions *improved* WoW; signal = NOISE (`memory/experiments/investigation-sleep-cluster-2026-06-16.md`).
  2. **W16 closed 2026-06-18** — the 06-16 ten recovered (none in the 06-18 pos-100 set); 06-18 produced a *different* 15-URL set → rotates = noise.
  3. **06-19 reconcile** — zero overlap (`comm -12` empty) between the 06-18 and 06-19 pos-100 sets → 4th confirmation.
- Rule: auto-quarantine any pull with ≥4 uniform exact-100 readings; assume noise by default and take **no content/deindex action**. Escalate to a genuine deindex investigation ONLY if the **same ≥4 URLs** report exactly 100 across **two consecutive pulls**. (Open carry: the 06-19 set re-checks Mon 06-22 — assume noise until then.)
- Established: 2026-06-21 (Learner), 3 closed confirmations.

## AP9. Never treat a YMYL reviewer fix + reviewedBy JSON-LD alone as a content-recovery sprint for pages already ranking in top-20 positions
- **What happened:** Sprint A (commit `270cf0c`, 2026-06-09) added named clinical reviewers + `reviewedBy: Physician` JSON-LD to 55 YMYL illness/treatment pages. 14-day check (W1-W6): 4/6 watched URLs STALLED or WORSE despite verified implementation in prod (3/3 byline + 3/3 JSON-LD confirmed). All 4 failures were on pages starting at pos 7.5–17.6 (top-20 territory).
- **Evidence (4 closed-watch failures, same action class):**
  1. **W2 /illnesses/alzheimers** — ⚫ WORSE (pos 10.5→13.1, impr −20.7%) — cannibalization by dementia sibling compounded lack of content differentiation (`closed-W2-2026-06-28.md`)
  2. **W3 /illnesses/ptsd** — 🔴 STALLED (impr −70%, pos stable ~10, query count rising = GSC anomaly still open 06-30 re-verify) (`closed-W3-2026-06-28.md`)
  3. **W4 /illnesses/drug-addiction** — 🔴 STALLED (pos 17.6→19.4, impr −11.9%) (`closed-W4-2026-06-28.md`)
  4. **W5 /treatments/eclectic-therapy** — 🔴 STALLED (pos 10.2→9.9, impr −3.7%) (`closed-W5-2026-06-28.md`)
- **The exception (NOT an AP9 violation):** W6 /treatments/biofeedback-therapy at pos 31.9 (page-3+) RECOVERED with the same reviewer fix — suggesting the rule is position-conditional (see below).
- **Why it fails for top-20 pages:** Pages already positioned in top-20 are competing against established content that outranks them. Google's Core Update demotion was driven by **content depth deficit** — the pages lacked clinical detail, India-specific data, and structured expert evidence. Adding a reviewer name signals that a clinician exists, but does NOT add the content depth Google penalised them for. The E-E-A-T signal is necessary (P1) but insufficient alone.
- **Rule:** When a YMYL page is demoted by a Core Update AND is starting from pos ≤ 20 (top-20 territory), the recovery sprint MUST include **both** (1) reviewer + reviewedBy JSON-LD AND (2) a content-depth refresh (India-specific data, clinical detail, FAQ coverage, schema depth). Reviewer-only fix is an E-E-A-T baseline, not a recovery sprint.
- **Position condition (seeded, 1 data point — not yet a principle):** W6 (pos 31.9, RECOVERED with reviewer-only) suggests that for deeply buried YMYL pages (pos > 25), the reviewer fix alone may be sufficient because the quality gap there IS primarily E-E-A-T signal rather than content depth. This is a seed — needs 2+ more deep-page recoveries to confirm as P12.
- **Established:** 2026-06-28 (Learner), 4 closed-watch failures (W2/W3/W4/W5) — ≥3 threshold met.
- **Applies to:** Any action that adds reviewer metadata to a YMYL page without simultaneously refreshing content depth, on pages at pos ≤ 20. Do NOT replicate the reviewer-only playbook to Cadabams Hospitals or CDC YMYL pages without a paired content-depth sprint.

## AP10. Never trust local repo state as proof of production state
- Counter-example seen 2026-06-26: T9 auto-shipped 3 YMYL pages (emdr-for-ptsd, biofeedback-therapy-for-anxiety, talk-therapy-for-depression) by writing MDX + committing on `feat/auto-ship-blogs-2026-06-26`. T9's spec defined success as "git push succeeded." But the merge-to-main step never ran (or pushed to a stale remote silently), and the 3 pages sat at HTTP 404 on production for 3 full days. The brain (tracking-db.json + the next Strategist run) read the local repo and thought the pages were live; downstream observation pipeline (T4) was assigned to monitor pages that didn't exist. Discovered only because the user asked "are the YMYL pages live?" and a manual `curl -sIL` returned 404s. Manual merge + push 2026-06-29 resolved.
- Rule: any action that claims to publish or update production must verify production state directly before marking complete. Concretely:
  1. **T9 auto-ship** — Step 5.5 must `curl -sI` each shipped URL with up to 4 retries over ~7 min after Vercel deploy window; URLs that don't return 200 get `status: AUTHORED_PENDING_VERIFY` (not PUBLISHED) in tracking-db, plus a Slack escalation.
  2. **Executor (T11) sprint fires** — after any sprint that adds or modifies live pages, the Executor's run-summary MUST include a "production-verified" line listing the URLs and the HTTP codes observed; missing this line = run incomplete.
  3. **Strategist (T10)** — when reading tracking-db to assess inventory growth, treat `status: PUBLISHED` as authoritative ONLY if `verified_live_at` is populated and ≤30 days old. `status: AUTHORED_PENDING_VERIFY` rows count against the inventory backlog, not the inventory live count.
- The deeper principle: **the source of truth on what's live is the live web server, not a git ref, not a tracking file, not a Slack post.** Every brain action that depends on "page X is live" needs a direct verification step or an explicit fallback to AUTHORED_PENDING_VERIFY.
- Established: 2026-06-29 (after the 06-26 stuck-branch incident), 1 confirmed instance.

---

(Learner appends new anti-patterns when closed watch windows reveal harmful actions to avoid.)
