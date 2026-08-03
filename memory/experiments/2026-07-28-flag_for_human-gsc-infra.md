# flag_for_human — GSC-INFRA-01-PERMANENT-FIX — 2026-07-28

## What we did
Executor T11 posted a Slack flag to #seo-workflow-mindtalk alerting Kushal to the GSC infrastructure disk issue.

**Slack message delivered:** ts: 1785238453.834979

## Context
- /sessions disk: 9.4G/9.8G — 0 bytes free
- 3rd recurrence (previous: 2026-07-20 first detection, 2026-07-24 workaround, 2026-07-27 recurrence)
- /tmp/pylibs_gsc workaround non-persistent: each session must reinstall google-auth from scratch; takes time and is fragile
- Stale GSC cache: last real pull was 2026-06-11 (~47 days old) — ALL GSC validations unreliable
- Blocked pipelines: WEEKLY-DROPS-BATCH-GSC-01, ONLINE-THERAPY-W18-DROP-01, STRESS-MGMT-GSC-AUDIT-01, all future T2 runs

## Options presented to Kushal
- **Option A:** Permanently clear disk space on /sessions volume — get df -h/du -sh listing, delete stale large files
- **Option B:** Move pylibs_gsc install to a persistent location outside /sessions (e.g., pip install --target=~/pylibs_gsc or user site-packages)

## Expected outcome
Kushal confirms one fix path. On next T2 run after fix: fresh GSC pull, WEEKLY-DROPS-BATCH-GSC-01 and STRESS-MGMT-GSC-AUDIT-01 unblock.

## Watch
None — this is an infrastructure flag, not a content action. T2 handles GSC pulls automatically once disk is clear.

## Notes
This is the 3rd time this flag has been raised. Without a permanent fix, every T2 run is at risk of falling back to stale data silently. The /tmp/pylibs_gsc workaround should be documented in BRAIN.md for T2 to apply as a fallback, but is not a substitute for the permanent fix.
