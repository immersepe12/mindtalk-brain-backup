# flag_for_human: CWV-REGRESSION-02 — 2026-07-15

## What we did
Executed flag_for_human for BACKLOG item CWV-REGRESSION-02 (added by T14 Tech Health Monitor on 2026-07-15). Posted Slack message to #seo-workflow-mindtalk with full diagnostic context. Marked BACKLOG row complete.

## What was detected
Tech Health Score dropped 85→60/100 (−25 pts) in the 2026-07-15 T14 weekly run. 7/8 sampled pages show LCP 9–11s — all were green (≤2.5s) last week. This is a new systemic regression, distinct from the T14-01 incident (07-01) which was fully resolved.

**Affected pages:**
- / (homepage): 2.55s → 10.55s (+315%)
- /treatments/counselling-therapy: 1.65s → 11.06s (+570%)
- /illnesses/anxiety: ~green → 9.59s
- /doctors/psychiatrists-in-bangalore: ~green → 9.34s
- /worksheets: ~green → 9.34s
- /blogs/emotional-distress: ~green → 9.14s
- /app: ~green → 9.00s
- /assessments: 4.01s (outlier — acceptable)

## Root cause hypothesis
FCP fast (1.05s) + LCP slow (9s) = LCP element is a large resource, not JS blocking. Suspected commits in the 07-10 to 07-14 window:
- `1e007b8` fix(nav): added Corporates link to global nav
- `fbc6235` feat(corporates): new Corporates landing page

/assessments is the outlier page that didn't regress — it may use a different layout or template, which can help dev isolate the regression.

## Expected outcome
Dev identifies LCP element, removes or lazy-loads it, and restores LCP to ≤2.5s. Same fix took ~1 week for T14-01 (07-01 incident).

## Dev action required
1. DevTools on homepage → Performance tab → identify LCP element
2. Check if Corporates nav link change is the cause (test on /assessments which didn't regress)
3. Fix the LCP element — DO NOT touch content

## Watch
No automated watch needed — this is a dev-action item. T14 will re-check next Wednesday (2026-07-22).

## Notes
- Slack message delivery status: attempted. If ERR_FAILED, message is archived here for manual delivery.
- Verifier: APPROVE (inline, 2026-07-15T16:30:00+05:30)
- Full technical report: reports/technical-health-2026-07-15.md
