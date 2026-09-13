# T20 Auto-Remediation 2026-09-12 — Slack digest (UNDELIVERED)

**Delivery status:** `slack_send_message` to #seo-workflow-mindtalk (C0AUAPS4J83) and `slack_search_channels` were both
**auto-declined** in this scheduled run (no approver present). Same for the Vercel MCP (`list_deployments`). The digest
below is archived verbatim so it can be posted by the next interactive session or once the tools are approved for this task.
Precedent: "Slack ERR_FAILED (recurring) — messages archived in brain/memory/experiments/" (2026-07-14).

---

🔧 **Auto-Remediation 2026-09-12** (first run since 08-31; Verifier: 5 APPROVE / 4 VETO / 1 NEEDS_HUMAN / 6 CORRECTION — all applied)

**Deploy health:** ✅ READY (`d5b6443`, 09-11 16:07) — content-proven: /doctors/shweta-kiran-wani 200, 09-09 blogs 200, sucheta-saha reviewedBy live. ⚠️ Vercel MCP was auto-declined in the scheduled run, so I can't see ERROR-then-retry deploys — please approve it for this task.

**Fixed: 9**
• 7 shipped briefs archived (slugs 200) · 14 redundant `/doctors-listings/` briefs archived (targets live at `/doctors/` since de29c86; task5 spec line 43 still names the dead route → T13)
• keyword-map +7 (shipped pages were invisible to rank-pull) · tracking-db: psychiatrist-vs-psychologist had no status/window since 09-01 → populated; `url_locked` back-filled on the 09-09 cohort (T9 left it unset)
• Reviewer pool: 301-orphans `santanu-tripathy` + `dr-akanksha-bhor` removed (T9 re-assigned santanu-tripathy on 09-09)
• Discovery re-run (cache fresh; stock script exceeds the sandbox 180 s cap — ran its own functions with 25k-row pages) · google-ads-search-terms ran clean

**False positives closed: 3**
• B21 — 3 DataForSEO "CRITICAL pos→100" illness pages: GSC shows all three impressing daily (personality-disorder pos 24.6→15.8); tracked queries rank 7–11 via /doctors/ pages; domain-match sentinel noise (14/36 at 100)
• B20 — values-clarification-act already emits HowTo + FAQPage + reviewedBy (read the JSON-LD)
• B19 — domineering-vs-dominating is growing (+84% impr, 6→9 clicks); the "domineering meaning" rank drop 2.4→10.3 IS real but 0 clicks at pos 2 and at pos 10 → Tier C/AP11, no action

**Withdrawn: 1 (my own closure, vetoed)** — B8 "therapist near me" is REAL at query level: /doctors/therapists-in-bangalore pos 9.3→16.2 (7→4 clicks/wk), /doctors/therapists-in-hyderabad 10.1→49.5, 8 weeks. Re-opened & re-scoped for T11/T12.

**Escalated: 3 new**
• 🔴 B22 NEEDS_HUMAN — `/blogs/therapist-for-depression` (live 09-09) has NO reviewedBy (orphan reviewer). Fix = one frontmatter line → `reviewer: dr-sneha` in `src/content/blogs/therapist-for-depression.mdx`. Inside Day-42 window (to 10-21): apply now or hold?
• Vercel MCP declined in scheduled runs (Step 0 blind to failed deploys)
• DISCOVERY-AVG-POSITION-IS-NOT-QUERY-POSITION-01 — `scripts/new-content-discovery.py` averages per-page positions across every site URL on the SERP (reported pos 41.6 for a query the site holds at 4.7; demand inflated up to 6×). Every T5 brief inherits this. Fix: derive per-query stats at `dimensions=[query]`.
Standing (unchanged): PAT-in-git-config, gsc-pull.py window overlap, stale local clone, B12/B15/W38 decisions.

**Brief queue:** 10 shippable `/blogs/` by spec metric (7 authorable) — refilled +4 net (7 authored → Verifier vetoed autism / personality-disorder / ptsd: site already page-1 for those families; corrected & kept: which-doctor-for-alcohol-addiction, best-doctor-for-panic-attacks, anxiety-counselling, teenage-counselling). Target ≥12 → short by 2; covers T9's 09-15/09-16 slots. Tier A for /blogs/ is exhausted — 14 genuine `/doctors/` Tier A briefs wait on tomorrow's cap-separation proposal.

Full log: `brain/memory/remediation-log.md` · BACKLOG + BRAIN.md updated.
