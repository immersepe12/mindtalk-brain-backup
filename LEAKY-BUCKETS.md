# Leaky Buckets (T18 priority feed)

**Updated by:** T19 weekly (Wednesday 11:00 IST)
**Read by:** T18 Professional Input Briefs (Monday 14:30 IST) — these pages get +25 priority points
**Reasoning:** High-traffic, low-intent pages are exactly where real clinician voice converts informational visitors into bookers
**Last updated:** 2026-06-17 (INAUGURAL RUN — LIMITED_BASELINE: true)

| URL | Unique visitors/wk | Intent rate | Median × | Why leaking? | Last touched | Reviewer |
|---|---|---|---|---|---|---|
| / (homepage) | 298 | 0% | 0.0× | Highest traffic, 0 tracked book_appointment events. **Likely instrumentation gap, not real leak** — homepage CTA may fire a different event. VERIFY before T18 brief. | — | — |

## ⚠️ Not yet promoted to T18 (need instrumentation check first)
The following had 0 tracked booking intent but are probably tracking gaps, not genuine UX leaks — confirm event wiring before queuing for clinician input:
- /treatments/drug-deaddiction (32v, 0 intent) — treatment page with no tracked CTA
- High-traffic blogs (hamilton-anxiety-rating-scale 95v, liebowitz-social-anxiety-scale 46v) — these are top-of-funnel by design; only promote to T18 if they should carry a soft booking CTA.

## Note for next run
True leaky-bucket detection needs the homepage + treatment-page CTA instrumentation confirmed. Once lp_form/whatsapp/call are pulled per-page (deferred this week), several "0-intent" pages will likely reveal real intent and drop off this list.
