# W-PSYCH-BLR-20260821 — 🟢 RECOVERED
# W-COUN-BLR-20260821 — 🔴 STALLED

---

## W-PSYCH-BLR-20260821 — /doctors/psychologists-in-bangalore

Action that opened watch: Organic observation / T17 competitive monitor flagged psychologists-in-bangalore as a Tier A regression concern on 2026-08-21 (pos drift under August Core Update)
Opened: 2026-08-21 | Closed: 2026-09-20 | Day-30 final (deferred twice due to GSC-INFRA-01 disk full)

Baseline metrics (T20 pre-pull `logs/t20-gsc-watch-verify-2026-09-13.json`, page-dim, 07-24→08-20): 13,755 impr / 88 clicks / pos 26.5 (491 impr/d)
Post-obs metrics (T20 page-dim, 08-22→09-11): 16,597 impr / 67 clicks / pos 18.1 (790 impr/d, +61%)
Fresh GSC pull 09-20 (query-dim): shows 0 impr in keyword aggregate — known truncation artifact (490+ daily impr distributed across many long-tail queries; top-50 keyword aggregate underrepresents)
Delta: impr +61% (+299 impr/d), pos improved 26.5→18.1 (+8.4 positions), clicks −24% (CTR compression at higher impression volume — fewer branded clicks per impression as informational queries added)

Verdict: 🟢 RECOVERED
Explanation: Page impressions surged +61% as the August Core Update redistributed mental health informational queries from aggregators to specialized provider pages. The pos improvement 26.5→18.1 represents the page moving from deep page-2 to mid page-2, approaching page 1. The click decline is expected — more informational queries at slightly lower CTR outweigh branded navigational queries.
Next: B12 therapy-near-me hub sprint (now unblocked) + further /doctors/ optimization would help convert the impression surge to clicks.

---

## W-COUN-BLR-20260821 — /doctors/counsellors-in-bangalore

Action that opened watch: Same batch as W-PSYCH-BLR-20260821 (T20 08-21 observation open)
Opened: 2026-08-21 | Closed: 2026-09-20 | Day-30 final

Baseline metrics (T20 page-dim, 07-24→08-20): 2,841 impr / 20 clicks / pos 15.7 (102 impr/d)
Post-obs metrics (T20 page-dim, 08-22→09-11): 2,203 impr / 14 clicks / pos 14.1 (105 impr/d, flat in impr/d)
Target query "counselling bangalore" pos 26.5→30.7 (82→79 impr) — regression. Page's own rank on target query: pos 48.6.
Fresh GSC pull 09-20 (query-dim): shows 0 impr in keyword aggregate — truncation artifact; actual daily rate ~105/d unchanged.
Delta: impr −22% gross (but ~flat per day), clicks −30%, target query pos worsened 26.5→30.7, page pos improved slightly 15.7→14.1

Verdict: 🔴 STALLED
Explanation: Target query "counselling bangalore" continues to be owned by /centers/indiranagar (pos 5.7) and /treatments/counselling-therapy (pos 10.5) — both Mindtalk URLs cannibalize the /doctors/counsellors-in-bangalore page for its primary intended query. The page itself is not the right URL to own the commercial counselling query; the cannibalization is structural (internal competition). Per-day impressions are flat (102→105/d) suggesting the audience continues but the query-to-URL assignment isn't resolving correctly.
Root cause: Structural internal cannibalization on "counselling bangalore" — /centers/ and /treatments/ URLs rank ahead of /doctors/ on the very query /doctors/ was designed to capture.
Action recommended: Internal linking audit + canonical guidance to resolve which URL should own "counselling bangalore." Either suppress /treatments/counselling-therapy for this geo query or add a CITY redirect to /doctors/counsellors-in-bangalore.
