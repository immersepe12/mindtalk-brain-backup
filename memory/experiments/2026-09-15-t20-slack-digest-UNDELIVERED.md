# T20 Auto-Remediation 2026-09-15 — Slack digest UNDELIVERED (4th consecutive scheduled run)
Channel intended: #seo-workflow-mindtalk (C0AUAPS4J83). `slack_search_channels` and `slack_send_message` were both auto-declined ("no one was available to approve it during this scheduled run"). Kushal: approve the Slack tool for the `mindtalk-auto-remediation` scheduled task, or paste the block below.

---

🔧 **Auto-Remediation 2026-09-15**
**Deploy health:** ✅ READY (`0001be1` — T9 15:19 IST, 6 /doctors/ listings + /blogs/anxiety-counselling; all 7 live 200, one build, edge-cache age 7.6 h). Vercel MCP auto-declined (5th run) → content-proof.

**Fixed: 6** — 7 shipped pages had no tracking-db record / keyword-map entry and their briefs were still queued → records opened (window 10-27), keyword-map 309→316, 7 briefs archived-as-shipped · bipolar brief archived (sibling `psychologist-for-bipolar-disorder` live 09-09 carries the same outline) · `couples-therapists-in-bangalore` brief archived (plural twin of the live singular) · alcohol brief HOLD → 10-06 (refresh the listing first).

**False positives closed: 2**
• **B8-HYD** (T11's "only 2 clinicians → near-empty Hyderabad page, choose A/B/C") — main has had `filterCity: null` since 08-05 (`7113261`) and the live page shows "Showing 5 professionals" (= Bangalore's roster). T11 read the stale local checkout (`feb506b`, 161 commits behind). Option B was done 41 days ago. Nothing to decide.
• **B24** ("run T12 manually today?") — T10 already set T12 09-20; T4 had already QDF_BLOCKED all 4 to 10-27. GSC truth logged for T12.

**Escalated: 4 (fix pre-written)**
• 🚨 **`/doctors/child-psychologists-in-bangalore` (Tier A, shipped today) renders ZERO clinicians** — `filterAgeGroup: "Child"` matches no profile; roster value is `"Children"` (18 would match). One-word fix in `dev-specs/2026-09-15-child-psychologists-bangalore-empty-cohort-fix.md` → T11 IMMEDIATE (Verifier: safety pause doesn't apply to a same-day ship correction).
• **BURNOUT-CANNIBAL-01** — two live blogs split "burnout treatment" (~1,600 impr / 1 click). Consolidation call, recommendation in BACKLOG; after 09-16 W-B7 check.
• **HFA-CANNIBAL-01** — old `understanding-high-functioning-anxiety` holds 795/796 impr at pos 10.5 / 0 clicks; the 08-18 page built for that query sits at pos 52. Decide with W43 (09-29).
• **WHITEFIELD-LISTING-01** — 7 clinicians carry `subLocation: Whitefield`, paid converts on "psychologist whitefield"; no listing exists and `/centers/whitefield` is 404. **Kushal: confirm Whitefield is Mindtalk-bookable in person** → T5 authors the area page.

**Brief queue: 4 shippable /blogs/ (refilled +0)** — below floor 6, refill fired: google-ads miner (281 terms) + 75k-row GSC decision-shape mine + ownership pulls → every family with impressions already has a Mindtalk holder, so 0 new briefs; demand filed as 4 CTR rows for T10 instead — headline **THERAPISTS-DELHI-CTR-01: `/doctors/therapists-in-delhi` 6,928 impr / 3 clicks / pos 9.6 in 15 days** (+ alcohol / drug-addiction / OCD specialists listings, ~1,400 impr / 1 click). Verifier: sweep incomplete — 3 more families next run.

Standing: WEBSITE-CHECKOUT-CORRUPT-01 now causes false escalations (⬆), B22, B12, B15, PAT plaintext, GSC integrity. Verifier 6 APPROVE / 3 CORRECTION / 0 VETO. Log: `brain/memory/remediation-log.md` 2026-09-15.
