# Watch W-PHOBIA-0918 — pending_evaluation (data error) / NEEDS_REFRESH = INDEXATION

URL: /blogs/phobia-treatment-in-bangalore
Action that opened watch: T9 auto-ship NEW blog — last /blogs/ non-cap-held ship at time of brief.
"No holder for 'phobia treatment in bangalore' family at time of brief."
Opened: 2026-09-18 | Day-21 check: 2026-10-09 | Day-42 check: 2026-10-30 | Evaluated: 2026-11-01

---

Baseline metrics (Day-0, 2026-09-18 note in WATCH.md):
  Impressions: 510 | Clicks: 0 | Avg Position: 22–52 (wide range, multi-query spread)
  Note: baseline here is PRE-ship page state; the new blog was shipped with improved content.

Day-21 check (T10 2026-10-09): "phobia-treatment-in-bangalore 0 impr at Day 21 -> index check queued (PHOBIA-BLR-INDEX-CHECK-01)"

Day-42 metrics (CW 2026-10-19 → 2026-10-26):
  Clicks: 0 | Impressions: 0 | Avg Position: — (no data)

Previous window (2026-10-12 → 2026-10-19):
  Clicks: 0 | Impressions: 0 | Avg Position: — (no data)

---

## Zero-data guard applied

Two consecutive GSC windows show 0 impressions (both 10-12→10-19 and 10-19→10-26).
However, per T10 Strategist 2026-10-30 note: "phobia-treatment-in-bangalore NEEDS_REFRESH = indexation (no watch)"
[Meaning T10 closed the watch note with NEEDS_REFRESH = INDEXATION classification]

T4 pre-classification (2026-10-30): NEEDS_REFRESH = indexation (NOT a content issue)

Per zero-data guard: DO NOT classify as 🔴 STALLED or ⚫ WORSE.
Verdict: pending_evaluation (data error) — NEEDS_REFRESH = INDEXATION

---

## Analysis

This blog was shipped 2026-09-18. After 42 days, 0 impressions = Google has not indexed or is not serving the page.
- Page confirmed live (200 status + in sitemap per T10/T14 checks)
- This is an INDEXATION FAILURE, not a content/relevance failure
- Join BLOG-INDEXATION-VERIFY-01 umbrella (BACKLOG ~58 priority)

Important note on baseline (510 impr / pos 22-52):
The 510 impr at "baseline" may have been for the OLD page content (pre-ship state) or a related query.
After new content shipped, the page appears to have dropped from Google's index entirely — consistent
with Google de-ranking a page it had cached when its content changed significantly (common for blog refreshes
on pages that weren't strongly indexed to begin with).

---

## P12 count exclusion

This page is NOT counted as a P12 failure per zero-data guard + indexation exception rules.
Indexation failures cannot be counted as ranking failures in P12 evidence.
P12 denominator unchanged.

---

## FAQ schema note (from WATCH.md line 1849)

BLOG-FAQ-KEY-MISMATCH-01: phobia-treatment-in-bangalore uses `question:`/`answer:` keys
where blog template reads `q:`/`a:`, so FAQ schema emits 0 Question nodes.
This is a dev-specs defect (dev-specs/BLOG-FAQ-KEY-MISMATCH-01.md).
Fix required before re-evaluating FAQ schema performance for this page.
However, FAQ schema fix is secondary to indexation fix — cannot evaluate either until indexed.
