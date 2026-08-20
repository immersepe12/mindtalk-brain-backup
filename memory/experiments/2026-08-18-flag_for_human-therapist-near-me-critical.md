# flag_for_human on THERAPIST-NEAR-ME-CRITICAL-02 — 2026-08-18

## What we did
Escalated "therapist near me" SERP collapse to Kushal via Slack (#seo-workflow-mindtalk).

- Action type: `flag_for_human`
- Backlog ID: THERAPIST-NEAR-ME-CRITICAL-02
- Trigger: 2026-08-17 T10 weekly summary confirmed pos 13→79 (65.7% drop) in one week on "therapist near me" (60,500/mo, Tier A commercial query)
- Verifier verdict: APPROVE (§1-§10 all pass; zero-risk notification action)

## Expected outcome
Kushal decision on recovery path:
- Option A: Hub enhancement on existing ranking URL (once T2 confirms URL via GSC)
- Option B: New therapists-in-bangalore brief (Bangalore = 65% of booking intent, currently absent from city brief queue despite Chennai/Delhi/Kolkata/Mumbai/Pune existing)

Expected recovery: ~+200–400 clicks/wk (two 60,500/mo queries)

## Slack delivery
✅ SUCCESS — ts: 1787051554.686779, channel: C0AUAPS4J83 (#seo-workflow-mindtalk)
Link: https://cadabamsgroup.slack.com/archives/C0AUAPS4J83/p1787051554686779

## Watch
No watch created — awaiting T2 GSC URL confirmation and Kushal decision.
Next T11 run: check for Kushal response in thread; if none, re-escalate via THERAPIST-NEAR-ME-CRITICAL-03.

## Notes
- T17-8 backlog entry is superseded by this row (T17-8 was tracking pos 16/21; this is now a CRITICAL collapse at pos 79)
- URL is unknown — /doctors/ is programmatic React (not MDX-editable); cannot run investigate_regression without URL
- City brief gap: 5 city briefs exist (Chennai/Delhi/Kolkata/Mumbai/Pune) but Bangalore (highest booking intent) is absent
