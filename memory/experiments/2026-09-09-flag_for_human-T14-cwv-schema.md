# flag_for_human — T14-CWV-01 / T14-CWV-02 / T14-SCHEMA-01 — 2026-09-09

## What we did

Posted 3 T14 tech-health flag_for_human items to Slack #seo-workflow-mindtalk.

Slack ts: 1788952539.340619
Channel: C0AUAPS4J83

## Items flagged

### T14-CWV-01
- Page: /treatments/counselling-therapy
- Issue: LCP 4,879ms (both PSI samples), perf score 0.51 — worst CWV on site
- Recommended dev action: hero image preload + SSR above-fold content verification

### T14-CWV-02
- Pages: /blogs/understanding-dominant-personality + /blogs/emotional-distress-all-you-need-to-know
- Issue: Bimodal LCP (2,701ms warm / 10-11s cold) — both samples exceed 2.5s CRITICAL threshold
- Hypothesis: Edge CDN cache miss on cold requests
- Recommended dev action: investigate CDN cache behavior, consider stale-while-revalidate or prerender

### T14-SCHEMA-01
- Scope: ALL /illnesses/ and /treatments/ pages
- Issue: MedicalWebPage JSON-LD type not emitting from illness/treatment template (SCHEMA-MEDICAL-TYPES-01 persisting post PR #23)
- PR #23 (08-17) fixed FAQPage but not MedicalWebPage
- Recommended dev action: add MedicalWebPage to JSON-LD type array in src/ template

## Delivery

Slack SUCCEEDED (ts confirmed). All 3 BACKLOG rows marked DONE.

## Notes

These were queued by T14 (Tech Health) task due 2026-09-09. Executor posted them as part of
Action 2 in today's run (counting as second action alongside B7 Batch 2).

Recommended priority order posted to Kushal:
1. T14-SCHEMA-01 (widest impact — template fix, affects all YMYL pages)
2. T14-CWV-01 (conversion-critical page)
3. T14-CWV-02 (CDN investigation)
