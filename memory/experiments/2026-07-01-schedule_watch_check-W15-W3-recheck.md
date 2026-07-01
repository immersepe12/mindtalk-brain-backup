# schedule_watch_check for W15 + W3 PTSD re-verify — 2026-07-01

## What we did

Created one-off Cowork scheduled task `mindtalk-watch-W15-W3-recheck-2026-07-01` to fire at 21:00 IST tonight (2026-07-01T15:30:00Z).

Both checks (W15 and W3) were due 2026-06-30 but deferred due to infrastructure failure:
- DataForSEO API timed out (no fresh rank data)
- GSC google.auth missing in obs sandbox

BACKLOG #22 was created by Strategist to track this deferral and schedule the retry on 07-01.

### W15 — Anxiety Neurosis CTR Verdict

- Page: `/blogs/understanding-anxiety-neurosis`
- Change: Sprint C-2 meta-rewrite (commit `579bb7c`, 2026-06-16)
- Baseline: "anxiety neurosis" 764 impr/wk, pos 4.6, CTR 0.9%
- Target: CTR ≥ 3%
- Gates: BACKLOG #17 (CTR staged v2, P11 implementation)

### W3 — PTSD 21-Day Re-Verify

- Page: `/illnesses/posttraumatic-stress-disorder-ptsd`
- Background: Sprint A added reviewer + reviewedBy JSON-LD (commit `270cf0c`, 2026-06-09)
- 14-day check showed: impr 803→241 (−70%) but query count ROSE 57→61, rank STABLE ~10
- Concern: Rising queries + stable rank + falling impressions = possible GSC under-report, NOT content failure
- Gates: PTSD brief scope in BACKLOG #18 (heavy rewrite vs E-E-A-T additions only)

## Expected outcome

Tonight's task (21:00 IST) pulls fresh DataForSEO + GSC data, evaluates both watches, and posts verdicts to Slack. Results will:
1. Unlock or gate BACKLOG #17 (W15 verdict)
2. Clarify PTSD brief depth for BACKLOG #18 (W3 re-verify verdict) — the #18 batch fires 07-02 after ALGO_WATCH clears

## Watch

- Task ID: `mindtalk-watch-W15-W3-recheck-2026-07-01`
- Fires: 2026-07-01 21:00 IST (one-time, auto-disables)
- WATCH.md W15 → status updated to `📅 SCHEDULED`
- WATCH.md W3 → re-verify flag updated to `📅 SCHEDULED`

## Notes

- Verifier APPROVE (all 10 checks pass — scheduling observation check, no blast radius)
- BACKLOG #22 marked COMPLETED
- If APIs are still down at 21:00 IST tonight, the task is instructed to log the failure + post Slack rather than fail silently
- Jun-9 cohort midpoint (6 URLs) was also deferred from 06-30 but is NOT included in this task — it requires the obs-monitor script (separate Task pipeline), not a generic watch check
