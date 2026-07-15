# Slack Archive — T14 Technical Health 2026-07-15
**Status:** ERR_FAILED (recurring Slack infra issue — see GSC-CRED-RESTORE-01 in BACKLOG)
**Intended channel:** #seo-workflow-mindtalk
**Archived:** 2026-07-15

---

⚠ CRITICAL 🔧 *Technical Health — 2026-07-15*

Overall: **60/100** (Δ **−25** vs last week's 85/100)

🔴 Critical:
- **CWV — 7/8 pages LCP 9–11s** (was green last week). Homepage: 2.55s→10.55s. Counselling-therapy: 1.65s→11.06s. Illness, doctors, worksheets, blog, app — all 9s+
- Suspected cause: global layout change from commits `1e007b8` (nav/Corporates link) or `fbc6235` (Corporates landing page) between 07-08 and 07-15
- Diagnostic: FCP is fast (1.05s) → LCP element itself is slow, not JS. Check what became the LCP element in DevTools.

✅ Healthy:
- Sitemap HTTP 200, robots.txt clean (all AI bots whitelisted)
- 0 broken internal links in production content
- HTTPS/canonical clean on all pages
- /assessments only green page (LCP 4.01s, perf 85) — use as layout diff clue

🟡 Watch:
- Schema: 4 persistent issues unchanged (MedicalWebPage on illness/treatment; ItemList on homepage)
- config.json `tracked_specialty_listings` uses `/doctors-listings/` prefix — actual URLs are `/doctors/[slug]` (tracking bug, not a live 404)
- Sitemap grew to 781 (+89 expected: 77 assessments + 5 T9 blogs + misc)

Top 3 actions required:
1. 🔴 **DEV: fix LCP regression** — open DevTools on homepage, find LCP element, check nav/corporates commits; target ≤3s LCP. DO NOT touch content.
2. 🟡 **config.json**: update `tracked_specialty_listings` paths from `/doctors-listings/` to `/doctors/`
3. 🚨 **GSC OAuth** (existing P0): still expired — fix on Mac Mini before Core Update 07-17 clearance

📎 Full report: `reports/technical-health-2026-07-15.md`
📎 BACKLOG: CWV-REGRESSION-02 added as CRITICAL
