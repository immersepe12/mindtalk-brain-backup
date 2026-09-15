# T20 Auto-Remediation digest — 2026-09-14 — UNDELIVERED (slack_send_message auto-declined in the scheduled run, 3rd consecutive)
Channel intended: #seo-workflow-mindtalk (C0AUAPS4J83). Paste-ready:

🔧 Auto-Remediation 2026-09-14
Deploy health: ✅ READY, content-proven (HEAD d5b6443, no commits after on main/staging; Vercel MCP auto-declined 4th run)

Fixed: 7
• 🚨 P1 — tracking-db.json had a list-valued `new_content` key (T5 10:35) that crashes day42-evaluate-v2.py ('list' object has no attribute 'get', reproduced) → converted to spec NEW- entries. Tomorrow's 4 Day-42 finals (B24) are unblocked.
• 18/20 of today's T5 briefs archived with evidence — query-level GSC shows a live page already owns each query on page 1 (cptsd test → /assessments/itq 2,067 impr/52 clk/pos 9.3; couples therapy → /treatments/couples-therapy 2,130/3/8.4; childhood trauma test → identical live /assessments/ slug; dbt-therapists already 200). 2 kept after Verifier (national adhd-specialists, cbt-therapists listings — URL fixed from dead /doctors-listings/).
• Aug-04 Day-42 cohort baselines pre-answered (3 NEW pages = no prior by definition; narrative-therapy GSC pre-window backfilled 899 impr/5 clk/pos 16.7 → 443/4/14.8). Its DataForSEO series was tracking the OLD PAGE TITLE as the keyword → fixed; systemic finding filed (~233/309 keyword-map entries are title-derived).
• 6 missing primary_keywords filled; 3 Aug-04 blogs added to keyword-map; 81 stale BRIEF_CREATED rows reclassified (79 SHIPPED / 2 ARCHIVED) — T5 floor maths + T16 runway now count the real queue (18).

False positives closed: 3
• "DataForSEO outage" → transient: API 200 in 1.1 s at 22:59, balance $15.82; morning run had processed 17 URLs before the 3-min wall clock.
• "No baseline → flag for human" (observation monitor) → answered by evidence.
• DISCOVERY STALE (1.5 d) → deferred to 09-15 when it has a consumer.

Escalated to Kushal/dev: 0 new. Standing: B22 reviewer frontmatter (src/**, fix pre-written), B12/B15 decisions, Vercel MCP declined, PAT plaintext.
Routed: B26 COUPLES-THERAPY-CTR-01 → T10/T11 (/treatments/couples-therapy pos 7.8 on 1,672 impr / 0 clicks, title+meta pre-written); proposal t5-query-ownership-gate-and-trackingdb-shape-20260914T2330 → T13 (apply 09-21).

Brief queue: 7 shippable /blogs/ (floor 6 met, refilled +0). T9 takes up to 6 on 09-15 → T20 09-15 refills.
Verifier: 17 APPROVE / 6 CORRECTION (applied pre-write) / 0 VETO. Log: brain/memory/remediation-log.md 2026-09-14.
