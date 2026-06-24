# flag_for_human on #16 Online-Therapy Hub path+reviewer decision — 2026-06-24

**Executor run:** 2026-06-24 ~16:30 IST
**Verifier verdict:** APPROVE (independent sub-agent; confirmed the action fires nothing and only requests the human decision; audit line in `brain/memory/verifier-log.md`)

## What we did
Posted a `flag_for_human` Slack message to `#seo-workflow-mindtalk` requesting Kushal's decision to unblock the already-drafted online-therapy hub sprint (`prompts/auto-drafted-sprint-online-therapy-hub-2026-06-23.md`, drafted by Executor 06-23). The sprint is human-gated (hard constraint 1: Executor NEVER auto-fires a sprint prompt) and **was not fired**.

Decision requested:
1. **Path** — `/blogs/` (informational, lower competition, faster index, non-YMYL) vs `/treatments/` (YMYL, needs named clinical reviewer + JSON-LD `reviewedBy`, higher authority).
2. **Reviewer** — assign clinical reviewer if `/treatments/` is chosen.

Context included in the flag: targets the `online therapy india / therapist online / online counsellor` cluster (~17k impr/mo) where Amaha/YourDOST/BetterHelp own the top 10 and Mindtalk has zero presence; commercial bucket where AI engines cite Amaha not Mindtalk → organic + AI-citation double win. Draft already carries P11 meta, AEO answer blocks, interactive therapist-matcher, AP2 direct CTAs.

Slack permalink: https://cadabamsgroup.slack.com/archives/C0AUAPS4J83/p1782299572647319

## Expected outcome
Once Kushal replies with path (+ reviewer), the sprint becomes fire-eligible on a subsequent Executor run. No autonomous site change this run.

## Watch
None opened (decision-request flag). The drafted sprint stays 🟡 DRAFT ONLY until the human reply arrives.

## Notes
- This is the natural next lifecycle step after the 06-23 draft (BACKLOG #12, completed). #16 remains a standing human dependency until answered; if no reply by next run it can be re-surfaced, but avoid spamming the channel — one clear ask is posted.
