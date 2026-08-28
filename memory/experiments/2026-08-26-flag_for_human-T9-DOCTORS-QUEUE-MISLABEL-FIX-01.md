# flag_for_human on T9-DOCTORS-QUEUE-MISLABEL-FIX-01 — 2026-08-26

## What we did
Posted Slack flag to #seo-workflow-mindtalk (ts: 1787742524.651529) notifying Kushal and dev team of the T9 cap-routing bug: 43 Tier A /doctors/ briefs are mis-classified as /blogs/ and cap-blocked. Explained root cause (T9 regex labels all candidates /blogs/ regardless of Suggested URL), impact (43 HTTP 404 pages, +100-200 Tier A clicks/wk once fixed), and recommended dev action (fix cap-routing so /doctors/ Suggested URL briefs flow to /doctors/ cluster cap).

## Expected outcome
Dev fixes T9 cap-routing regex → T9 next run auto-ships /doctors/ briefs → +100-200 Tier A booking-intent clicks/wk at P12 ≥80% page-1 rate within 42 days.

## Watch
No watch opened (dev fix triggers T9 auto-ship directly).

## Notes
Verifier: APPROVE (zero-risk operational notification, no content touched).
Slack delivered: ts 1787742524.651529, #seo-workflow-mindtalk.
BACKLOG row marked COMPLETE this run.
