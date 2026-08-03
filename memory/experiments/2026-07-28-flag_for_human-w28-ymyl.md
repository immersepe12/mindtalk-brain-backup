# flag_for_human — W28-YMYL-BATCH-REVIEWER-CONFIRM — 2026-07-28

## What we did
Executor T11 posted a Slack flag to #seo-workflow-mindtalk requesting Kushal's decision on the AP3 clinical gate for 4 YMYL refresh briefs.

**Slack message delivered:** ts: 1785238458.421209

## Context
T3 fired on 2026-07-27 and created 4 W28 YMYL refresh briefs:
- `briefs/depression-brief.md` (reviewer: Dr. Arun Kumar V, Sprint A 2026-06-09 = 48d ago)
- `briefs/anxiety-brief.md` (reviewer: Dr. Krishna K R, Sprint A 2026-06-09 = 48d ago)
- `briefs/alzheimers-brief.md` (reviewer: Dr. Arun Kumar V, Sprint A 2026-06-09 = 48d ago — YMYL_RECOVERY_FAILED tag)
- `briefs/narrative-therapy-brief.md` (reviewer: Sufia Nusrat, Sprint A 2026-06-09 = 48d ago)

All 4 pages are Core Update YMYL demotion recovery targets (P1 + AP9).

## Decision requested from Kushal
**Option 1:** Existing Sprint A sign-offs (48 days old, within the 90-day AP3 Option B window) cover the W28 refresh content → T11 can ship immediately on next eligible run.

**Option 2:** Refresh content is substantially new → each brief needs a fresh reviewer sign-off with a new date before T11 fires.

## Special note: Alzheimers brief
The alzheimers brief has a `YMYL_RECOVERY_FAILED` tag (this is the 2nd refresh attempt). Per AP9, a reviewer-only update is insufficient — the brief MUST include substantial content-depth refresh (new evidence, expanded clinical sections, additional E-E-A-T signals). Kushal should verify the alzheimers brief includes this before approving.

## Expected outcome
Kushal confirms Option 1 or Option 2. If Option 1: T11 ships all 4 YMYL refreshes on next eligible run. If Option 2: team assigns fresh reviewer + sign-off date to each brief; T11 fires after confirmation.

## Watch
W30 watch to open on ship for each brief (check date: ship date + 14d).

## Notes
Depression and anxiety are likely Mindtalk's top-2 impression-earning illness pages. Full YMYL recovery from Core Update demotion = estimated +200-400 impr/wk per page (historical baseline vs. current demoted position). This is a high-leverage batch.
