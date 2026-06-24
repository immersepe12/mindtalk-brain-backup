# flag_for_human on Tech-Health batch (TH-1 / TH-2 / TH-3) — 2026-06-24

**Executor run:** 2026-06-24 ~16:30 IST
**Verifier verdict:** APPROVE (independent sub-agent; cross-checked all figures verbatim against `reports/technical-health-2026-06-24.md`; audit line in `brain/memory/verifier-log.md`)

## What we did
Posted ONE consolidated `flag_for_human` Slack message to `#seo-workflow-mindtalk` surfacing the three human/dev-review findings from Task 14's inaugural Technical Health run (site score 78/100). Executor took **no** code or content action — all three fixes live in human-controlled production paths (`src/app/**`, `src/components/**`, schema emitters), which Executor must never auto-modify.

Findings flagged:
- **TH-1 (🔴 CRITICAL)** — Homepage LCP = 10.95s (4.4× over ≤2.5s), perf 62/100 (threshold 75). Homepage-specific (all other sampled pages: LCP avg 1.82s, perf 96.6, CLS 0). Likely oversized hero image / render-blocking JS. **Must fix before Meta ads restart.**
- **TH-2 (🟡)** — FAQPage JSON-LD missing on `/treatments/counselling-therapy` (YMYL) and `/blogs/understanding-dominant-personality` (2 of 10 sampled). Losing FAQ rich-result eligibility. Check systemic. (dominant-personality is the Sprint B W7 page that just reclaimed AIO citation.)
- **TH-3 (🟡)** — `reviewedBy` present in HTML but not serialized into JSON-LD on `/blogs/emotional-distress` (YMYL; the Sprint B W9 page). Lost E-E-A-T signal. Check systemic class of YMYL blogs.
- (Noted, low priority: homepage also missing ItemList + BreadcrumbList schema.)

Slack permalink: https://cadabamsgroup.slack.com/archives/C0AUAPS4J83/p1782299568807949

## Expected outcome
Human/dev remediation (not autonomous): homepage perf 62 → 80+, FAQ rich-result eligibility restored on treatment/blog pages, YMYL `reviewedBy` E-E-A-T signal restored. No site change attributable to this run.

## Watch
None opened (flag-only; outcomes depend on dev action). Task 14 re-runs weekly (Wed) and will show whether the homepage LCP + 4 schema issues clear in next baseline-vs-week comparison.

## Notes
- AP3-compliant: TH-2 + TH-3 touch YMYL pages but only as flags — no autonomous YMYL edit.
- These were the three top-priority BACKLOG rows, all `flag_for_human`, produced this morning by Task 14. Bundled into one notification (one logical execution unit, zero blast radius) per the flag_for_human dispatch pattern.
- Recurrence-hardening idea for Meta-Learner: if Task 14 keeps emitting the same schema-emitter gaps (FAQPage / reviewedBy serialization), that's a single code fix in the schema layer, not N per-page flags — worth a one-time dev ticket rather than weekly re-flagging.
