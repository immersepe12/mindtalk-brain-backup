# flag_for_human on CLINICAL-FAQ-SIGN-OFF-01 — 2026-08-18

## What we did
Escalated clinical FAQ sign-off requirement to Kushal via Slack (#seo-workflow-mindtalk).

- Action type: `flag_for_human`
- Backlog ID: CLINICAL-FAQ-SIGN-OFF-01
- Trigger: Schema PR #23 live as of 2026-08-17 (T20 Cowork). MedicalCondition + FAQPage now emit on illness/treatment templates. Clinical sign-off is the sole remaining blocker for W36🔴+W37⚫ recovery.
- Verifier verdict: APPROVE (§1-§10 all pass; zero-risk notification action)

## Expected outcome
Kushal forwards `faqs-pending-clinical-review/CLINICAL-REVIEW-PACKET.md` to clinical team.
One clinician sign-off on one YAML block → FAQPage + MedicalCondition schema go live on that page instantly (no additional dev work required).

Priority order: depression (/illnesses/depression, W36🔴) → anxiety (/illnesses/anxiety, W37⚫) → remainder of 41 pages.

Expected impact once FAQPage emits: +400–800 impr/wk across 41 YMYL pages.

## Slack delivery
✅ SUCCESS — ts: 1787051560.673189, channel: C0AUAPS4J83 (#seo-workflow-mindtalk)
Link: https://cadabamsgroup.slack.com/archives/C0AUAPS4J83/p1787051560673189

## Watch
- Day-42 deadline: 2026-09-11 (W36/W37 watch closes)
- Effective content deadline: ~2026-08-25 (changes after this may not index in time for Day-42 eval)
- T11 next run: check if Kushal has actioned — if no sign-off received by 2026-08-22, re-escalate with urgency flag

## Notes
- 164 Q&As staged across 41 YMYL pages in faqs-pending-clinical-review/
- CLINICAL-REVIEW-PACKET.md contains 41 paste-ready YAML blocks
- Schema PR #23 confirmed live by T20 Cowork 2026-08-17 — templates now emit schema, waiting only on frontmatter population
- Root cause of W36🔴+W37⚫: SCHEMA-MEDICAL-TYPES-01 gap (diagnosed T12 2026-08-16); schema gap now closed at template level
