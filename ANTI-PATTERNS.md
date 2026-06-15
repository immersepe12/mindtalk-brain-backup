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

---

(Learner appends new anti-patterns when closed watch windows reveal harmful actions to avoid.)
