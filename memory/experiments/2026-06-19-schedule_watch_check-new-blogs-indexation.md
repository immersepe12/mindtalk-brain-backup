# schedule_watch_check on W12-W14 (3 NEW blogs indexation) — 2026-06-19

## What we did
Created a one-time Cowork scheduled task `mindtalk-watch-new-blogs-indexation-2026-07-01` (fireAt 2026-07-01 09:00 IST, auto-disables after firing) to run the +14-day indexation/ranking evaluation on the three NEW blogs shipped 2026-06-17 (commit `549dac3`):
- W12 → /blogs/couple-therapy-techniques
- W13 → /blogs/how-to-find-a-therapist-for-ocd
- W14 → /blogs/how-to-find-a-therapist-in-india

The WATCH.md rows W12-W14 already existed (opened 06-17) but there was **no scheduled task** to actually fire their 07-01 check — verified against `list_scheduled_tasks` (only the 06-23 Sprint A/B/C one-time checks existed). This action filled that gap. WATCH.md W12-W14 status updated `open → scheduled`. BACKLOG row 9 marked complete.

## Expected outcome
Per BACKLOG #9: +1.5k–3k impr/wk after 4–6wk indexation. The 07-01 task is an EARLY (14d) read, not the final verdict — it confirms the 3 NEW pages are indexed, in the sitemap, and beginning to impress. A 🔴 (not indexed / 404 / sitemap-missing) would escalate immediately; 🟡 (~0 impr at 14d) is normal for NEW pages and keeps the watch open to the 4–6wk final.

## Watch
W12-W14 → status `scheduled`; evaluation fires 2026-07-01 09:00 IST.

## Verifier
APPROVE (independent sub-agent, full §1–§11 checklist). Key reasoning: writes only to a scheduled-task SKILL.md + brain/*.md (allowed set); zero production code; AP3 N/A (additive /blogs/ NEW pages, nothing shipped); AP4 N/A (no page modified, only a future read scheduled); §8 not perturbed (scheduling a watch's own due-date evaluation is the intended lifecycle); PII-clean. Logged to verifier-log.md.

## Notes
The 07-01 task prompt is fully self-contained (re-reads WATCH.md/BRAIN.md, pulls DataForSEO + GSC aggregated metrics only, no content/code changes, no push, posts Slack). `notifyOnCompletion=false` to avoid noise. Coordinates with Learner (T12) which formally closes watches at the 4–6wk final.
