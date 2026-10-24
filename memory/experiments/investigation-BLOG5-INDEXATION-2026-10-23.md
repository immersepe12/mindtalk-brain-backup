# investigate_regression on BLOG5-INDEXATION-VERIFY-01 — 2026-10-23

## What we did (read-only; no edits, no push)
Verifier: APPROVE (conditions: read-only, AP8-safe, recommend only, link-only follow-up via separate PR).
Live curl with cache-buster on the five 2026-09-09 blogs (adhd-diagnosis-bangalore, psychiatrist-for-anxiety, psychologist-for-schizophrenia, therapist-for-depression, psychologist-for-bipolar-disorder):
- All 5: HTTP 200, robots "index, follow", **self-referencing canonical** (re-verified by piping curl straight to grep; an earlier "all point to bipolar" reading was a temp-file artefact).
- All 5 present in https://www.mindtalk.in/sitemap.xml (944 locs).
- GSC local pull (window 2026-10-11..10-18): 0 impressions, 0 clicks, no keywords for all 5. (Evidence is GSC impressions, NOT pos-100 tracker values — AP8.)

## Conclusion
Not a technical block (200, indexable, canonical OK, in sitemap). Most likely "discovered/crawled, not indexed" = low-authority new-page problem. Volumes are low (~100-150 for three; therapist-for-depression ~500; adhd-diagnosis-bangalore ~1000) so only the last two are real test cases.

## Not done / NEEDS_HUMAN
GSC URL Inspection (coverage state, last crawl, Google-selected canonical) is not reachable via API from here. Kushal to run URL Inspection in Search Console for adhd-diagnosis-bangalore and therapist-for-depression first.

## Recommended next action (not executed)
If Inspection shows not-indexed: add 2-3 link-only internal links from already-indexed Tier A/B hubs (doctors/illnesses) to these pages via a separate PR (Kushal merges); must pass AP4/AP12 on source pages and blogs cluster cap. No clinical copy changes (YMYL-adjacent).

## Watch
None added.
