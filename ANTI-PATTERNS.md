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

## AP3. Never auto-ship YMYL content (illness / treatment / suicide-safety)
- Counter-example: hypothetical — auto-shipping an illness brief without clinical review could publish incorrect medical guidance, harming users and getting demoted by Google.
- Rule: hard block in code. Auto-shipper script must skip any brief targeting these directories.

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

---

(Learner appends new anti-patterns when closed watch windows reveal harmful actions to avoid.)
