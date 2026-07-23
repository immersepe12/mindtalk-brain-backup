# flag_for_human on CANNIBAL-PUSH-01 (ESCALATED) — 2026-07-21

## What we did

Fired flag_for_human for CANNIBAL-PUSH-01 (T11 Executor, 4:30 PM IST run). Posted combined Slack to #seo-workflow-mindtalk documenting the ESCALATED conflict state found on local main. This item was escalated beyond its original scope due to T9 running before the Executor's window.

## Conflict state at time of flag (ESCALATED)

**Original CANNIBAL-PUSH-01 scope (from BACKLOG):**
- Commit 59c3c5a (07-20) on local main, not pushed to origin
- 3 blog→treatment 301 redirects + T17-8 free-therapy section
- Blocked on `npm run build` verification (AP6)

**ESCALATED: Additional conflicts found during investigation:**

1. **T9 re-created the 3 retired slugs.** CANNIBAL-BLOG-01 (commit 59c3c5a, 07-20) moved these to `.retired-2026-07-20/`:
   - `src/content/blogs/what-is-act-therapy.mdx`
   - `src/content/blogs/what-is-biofeedback-therapy.mdx`
   - `src/content/blogs/what-is-rtms-treatment.mdx`
   
   T9 (07-21 at ~16:20-16:27) created NEW versions of these SAME slugs as fresh blog pages, creating a direct conflict on local main.

2. **`redirects.mjs` does NOT exist.** Commit 59c3c5a references adding redirects to `src/redirects.mjs`, but this file was never created. `next.config.ts` also has no redirects for these slugs. The 3 intended blog→treatment redirects are MISSING from the site entirely.

3. **5 `.tmp_merge` files in working tree** (from T9's feature branch merge):
   - `src/content/blogs/common-relationship-issues.mdx.tmp_merge`
   - `src/content/blogs/how-to-choose-a-de-addiction-centre-in-india.mdx.tmp_merge`
   - `src/content/blogs/what-is-act-therapy.mdx.tmp_merge`
   - `src/content/blogs/what-is-biofeedback-therapy.mdx.tmp_merge`
   - `src/content/blogs/what-is-rtms-treatment.mdx.tmp_merge`

4. **Git state:** Local main at `feb506b` (07-21 16:27), 11 commits ahead of origin/main at `3a82ca1` (07-17). `npm run build` has NOT been run on any of these commits.

## Production status

**SAFE** — origin/main is at `3a82ca1` (07-17). Nothing broken is on production. All conflicts are local-only.

## Action required (Mac Mini)

**Decision A — CANNIBAL wins (retire the 3 slugs, recommended):**
```bash
git rm src/content/blogs/what-is-act-therapy.mdx
git rm src/content/blogs/what-is-biofeedback-therapy.mdx
git rm src/content/blogs/what-is-rtms-treatment.mdx
rm src/content/blogs/*.tmp_merge
# Create redirects in next.config.ts (redirects.mjs doesn't exist)
npm run build
git add -A && git commit -m "fix: resolve T9/CANNIBAL conflict, add missing redirects"
git push origin main
```

**Decision B — T9 content wins (drop the CANNIBAL retirements for these 3):**
```bash
git rm "src/content/blogs/.retired-2026-07-20/what-is-act-therapy.mdx"
git rm "src/content/blogs/.retired-2026-07-20/what-is-biofeedback-therapy.mdx"
git rm "src/content/blogs/.retired-2026-07-20/what-is-rtms-treatment.mdx"
rm src/content/blogs/*.tmp_merge
npm run build
git add -A && git commit -m "fix: keep T9 new blogs, drop CANNIBAL retirements for 3 slugs"
git push origin main
```

**Either way:** redirects.mjs must be created OR the redirects added to next.config.ts — the blog→treatment canonical flow is broken regardless.

## Verifier pre-flight

**Verdict: APPROVE** — flag_for_human has zero blast radius. No content changes, no push, no code modifications. All action is Slack notification and BACKLOG row update.

## Slack

https://cadabamsgroup.slack.com/archives/C0AUAPS4J83/p1784632535682619

## Notes

- Root cause of escalation: T9's brief queue contained briefs for the 3 CANNIBAL slugs (older than the CANNIBAL-BLOG-01 decision). T9 had no visibility into the local-main retirement state when it ran.
- Prevention: T9 spec should check `.retired-*` directories before creating new MDX files for the same slug.
- The CANNIBAL-BLOG-01 commit (59c3c5a) had a note "npm run build NOT run" — this is what blocked it from being pushed via T9's normal build gate, leaving it in an intermediate local-only state.
