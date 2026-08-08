# Experiment: ship_REFRESH_brief — /blogs/yoga-for-anxiety
**Date:** 2026-08-05
**Task:** T11 Executor Run
**Backlog ID:** YOGA-FOR-ANXIETY-SHIP-01
**Commit:** `6c6d89e5d4508fa040bc36bf41df3e4f7b30b73f`
**Merge:** `e73f066659ce535c018bb58bdc1bb8f5732fc9aa`

## Context

CTR-led drop: yoga-for-anxiety clicks −33%, impressions +4.6% over 90 days. Classic title/meta mismatch + zero structured data. Prior VETO 2026-07-28 was for meta title 66 chars (off by 1 from brief's stated 65). Fixed to 57 chars. veto expired 2026-07-31. AP4 clear (last touch 2026-02-20, 166d).

## Changes Applied

| Change | Detail |
|---|---|
| metaTitle | "7 Poses That Actually Work" → "10 Poses That Calm Your Mind" (57ch) |
| metaDescription | Added NYU 2020 RCT signal, updated pose count (143ch) |
| quickAnswer | Added (533 chars, PNS mechanism + Yin/Restorative rec + 3-5x/wk evidence) |
| keyTakeaways | Added 5 items |
| faqs | Added 5 Q&As (FAQPage schema eligible) |
| New H2 | "Which Type of Yoga Is Best for Anxiety?" (~140w, Yin/Restorative/Hatha/Vinyasa) |
| New poses | Tree (Vrksasana), Bridge (Setu Bandhasana), Easy Pose (Sukhasana) — ~70w each |
| New H2 | "Can Yoga Help with Anxiety Attacks and Panic Symptoms?" (~130w, NYU RCT) |
| Removed | "Common Myths About Yoga for Anxiety" H2 (~100w) |
| Removed | "Embracing Yoga for Stress and Anxiety Relief as a Holistic Approach" H3 |
| Internal links | /illnesses/anxiety, /contact, /blogs/top-8-tips-for-immediate-anxiety-relief |

## Verifier Outcome
APPROVE — all 10 checks passed. Meta title 57ch independently verified. Veto expiry 07-31 confirmed (5 days clear). /blogs/ cap 4/6.

## Production Verification
- HTTP 200: `https://www.mindtalk.in/blogs/yoga-for-anxiety` ✓ (307→200 www-redirect)
- Vercel deploy: auto-triggered from merge `e73f066`
- Blob `167db42e` confirmed in main tree via GitHub Trees API ✓

## Expected Impact
+15-30 clicks/wk within 6 weeks. Mechanisms:
1. FAQPage schema → rich result eligibility (PAA box citations)
2. Title "10 Poses" vs competitor "11 Poses" — reduces CTR gap
3. New H2 covers #1 PAA query cluster ("which type of yoga is best for anxiety")
4. NYU 2020 RCT citation — E-E-A-T signal for "is yoga proven" query variant

## Watch
W39 — check 2026-08-19 (14d). Evaluate: CTR trend, rich result appearance, click delta.
