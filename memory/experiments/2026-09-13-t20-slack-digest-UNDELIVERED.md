# T20 Slack digest — 2026-09-13 — UNDELIVERED (slack_search_channels + slack_send_message auto-declined in the scheduled run; 2nd consecutive day)
Intended channel: #seo-workflow-mindtalk (C0AUAPS4J83). Paste-ready:

🔧 Auto-Remediation 2026-09-13 (T20, 22:57–23:45 IST)
Deploy health: ✅ READY (content-proven, HEAD d5b6443 unchanged since 09-11; Vercel MCP auto-declined again)

Fixed: 4
• Stale .git/index.lock on both repos renamed (104 h / 24 h, 0 B) → T16 committed + pushed brain snapshot 71922c5 at 23:09 — first off-site backup since 09-11. (Git can't unlink on FUSE, so a lock re-spawns after every git op — renamed again at run end; T16 must rename-not-rm.)
• GSC works from the sandbox: HOME=/tmp XDG_CACHE_HOME=/tmp TMPDIR=/tmp PYTHONPATH=.pip-packages python3 scripts/gsc-pull.py --url … — refreshed the 4 watch files + the 4 Day-42 URLs due 09-15 (B24 unblocked).
• Bhojpuri listing brief archived — 0 of 62 profiles speak Bhojpuri → empty page. Roster pre-flight filed.
• B8 pre-check: both therapists-in-* listing MDX exist (dir is src/content/doctors-listings/).

False positives / mis-routed closed: 2
• T12's "zero-impression cohort" (W36/W37/W-PSYCH-BLR/W-COUN-BLR) — all four impress daily through 09-11 (95 / 50 / 790 / 105 impr/day). Pull-side error, not disk. Data in WATCH.md; verdicts stay with T12 (09-20). Verifier re-pulled independently.
• B23 is not a Kushal decision — cap enforcement is spec text (0 hits in scripts/*.py; task9 L160; VERIFIER §9). Re-routed to T10's apply-pass with corrections (the proposal's 3/3 YMYL caps contradict §9's 7/5).

Escalated to Kushal/dev: 0 new — standing only (B22 reviewer line in src/**, B12/B15 calls, Vercel + Slack MCP approvals for scheduled runs, PAT plaintext, audit-unshipped-briefs.py L21/61 one-liner below).

Real finding: the 14 Tier A /doctors/ briefs are code-path-blocked, not cap-blocked. Listing pages are MDX in src/content/doctors-listings/ rendered at /doctors/<slug> (281 live) — content-only ships — but T9 Step 1 + scripts/audit-unshipped-briefs.py only know blogs|treatments|illnesses, so they're mislabelled /blogs/ and cap-skipped every run. Companion proposal t9-doctors-listings-scope-20260913T2330 (apply 09-20) adds the dir + a ≥1-matching-profile gate + online-only framing for non-open cities. One dev line: scripts/audit-unshipped-briefs.py L21 add "doctors-listings", L61 print resolved prefix.

Brief queue: 7 shippable /blogs/ (refilled +0, floor met) · 13 viable /doctors/ Tier A waiting on the above · cap resets 09-15 → T20 refills Monday night.
Log: brain/memory/remediation-log.md 2026-09-13 · Verifier 4 APPROVE / 2 CORRECTION / 0 VETO.
