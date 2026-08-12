# flag_for_human on SCHEMA-MEDICAL-TYPES-01 — 2026-08-12

## What we did
Escalated persistent schema gap (8 consecutive T14 runs with zero progress) to dev team via Slack (#seo-workflow-mindtalk, ts: 1786533030.375569). Verifier sub-agent verdict: APPROVE (zero-risk operational notification).

**Slack message included:**
- FAQPage template regression: illness/treatment page templates not reading `faqs:` frontmatter (blog templates do correctly — this is a component-level regression or oversight)
- Single template fix = FAQPage schema on ~50+ YMYL pages simultaneously
- MedicalWebPage + MedicalCondition missing from illness page templates (pure E-E-A-T signals, no clinical sign-off required)
- MedicalWebPage missing from treatment page templates
- ItemList + BreadcrumbList missing from homepage
- Priority order for dev: FAQPage regression first → MedicalWebPage/MedicalCondition → ItemList/BreadcrumbList
- Deadline: 2026-08-26 Core Update (14 days)

## Expected outcome
Dev team implements template-level fixes before Aug Core Update. FAQPage schema on ~50+ illness/treatment YMYL pages = FAQ rich results + MedicalWebPage E-E-A-T signal. Conservative estimate: +5-15% CTR on FAQ-rich-result eligible queries.

## Watch
None opened (dev action required — T14 will detect schema gaps cleared on next weekly run).

## Notes
- These gaps have been present in every T14 run since 2026-06-24 (8 consecutive runs)
- FAQPage gap is highest-leverage: data already exists in frontmatter, just not being rendered by templates
- No clinical sign-off required — purely structural code changes
- Verifier: APPROVE — all §1–§10 checks pass or N/A for flag_for_human type
