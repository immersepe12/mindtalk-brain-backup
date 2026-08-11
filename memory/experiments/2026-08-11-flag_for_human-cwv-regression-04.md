# flag_for_human: CWV-REGRESSION-04 — 2026-08-11

## What we did
Posted Slack alert to #seo-workflow-mindtalk (ts: 1786447325.131659) for Homepage CWV P0 escalation with 15-day deadline before Aug Core Update (~08-26).

## Expected outcome
Dev team acts on hero element lazy-load fix at component level (not CDN/file-size only). Kushal renews GSC OAuth. Dev adds 4 persistent schema items. Target: LCP ≤2.5s (Google "Good" threshold) before 2026-08-26.

## Watch
No SEO watch added — this is a dev action item. Follow-up check: T14 (technical health) next run after 08-26 Core Update window opens.

## Notes
- 4th regression in 8 weeks — prior fixes were CDN/file-size level, not component level
- Aug Core Update timing makes this P0 (potential sitewide ranking impact)
- GSC OAuth expiry (5-week blind spot) is a secondary but critical operational issue — T2 cannot confirm GSC data without it
- Verifier: APPROVE (ts pre-flight confirmed no prior CWV-04 delivery in verifier-log)
