# Experiment Log: W-BLOG5-INDEX-0921 — DEFERRED (Zero-Data Guard)
**Date:** 2026-10-25 (check date was 2026-10-22)  
**Evaluated by:** T12 (LEARNER)  
**Verdict:** ⚠ ZERO-DATA GUARD — DEFERRED to 2026-10-28

---

## Context
5 blogs shipped 2026-09-09 (Day-46 at time of evaluation). Expected Day-42 final check date: 2026-10-22. These blogs are past the Day-42 window.

**URLs in cohort:**
1. /blogs/adhd-diagnosis-bangalore
2. /blogs/psychiatrist-for-anxiety
3. /blogs/psychologist-for-schizophrenia
4. /blogs/therapist-for-depression
5. /blogs/psychologist-for-bipolar-disorder

---

## GSC Data: Oct 15–22, 2026
| URL | Impressions | Clicks | Position |
|---|---|---|---|
| /blogs/adhd-diagnosis-bangalore | 0 | 0 | — |
| /blogs/psychiatrist-for-anxiety | 0 | 0 | — |
| /blogs/psychologist-for-schizophrenia | 0 | 0 | — |
| /blogs/therapist-for-depression | 0 | 0 | — |
| /blogs/psychologist-for-bipolar-disorder | 0 | 0 | — |

**Previous window (Oct 8–15): also 0/0/0 for all 5 URLs.**

---

## Zero-Data Guard Applied
Per hard constraint (verbatim): *"If ALL watches in a batch show 0 impressions, treat as measurement error and post ⚠ LEARNER WARNING: zero-impression cohort — possible GSC pull format bug before recording any verdicts. Do NOT write 🔴 or ⚫ verdicts on zero-impression data."*

**Cohort: 5/5 URLs = 0 impressions. Guard TRIGGERED.**

However, this is NOT a GSC pull format bug — the same pull session returned:
- yoga-for-anxiety: 1,531 impressions ✅
- anxiety-therapists-in-kolkata: 140 impressions ✅
- types-of-group-therapy: 346 impressions ✅

This suggests the 5 blogs genuinely have 0 GSC impressions — potentially an indexation issue rather than a measurement artifact. However, WATCH.md T10 note (2026-10-21) explicitly states: *"0 GSC impressions. Status: pending_evaluation by T12 (10-22). Check: URL Inspection coverage state before any content change; re-pull GSC page-dim 2026-10-28."*

**Decision: Apply zero-data guard as instructed, defer to Oct 28 re-pull.**

---

## Possible Causes (NOT CLASSIFIED — investigation deferred to T20)
1. **Indexation lag / crawl delay** — pages may not yet be indexed (unlikely at Day-46 but possible)
2. **Indexation failure** — pages may have been excluded (noindex tag, orphaned, sitemap missing)
3. **Keyword demand mismatch** — queries may genuinely have near-zero India search volume
4. **REPO MOVE confound** — www.mindtalk.in migrated from Vercel to AWS Amplify ~Oct 14; possible temporary indexation disruption during migration window

---

## Status
DEFERRED — NOT CLOSED. Re-evaluate at 2026-10-28 (per T10 instruction).  
Do NOT write 🔴 or ⚫. Do NOT modify content. Do NOT close watch.

**⚠ LEARNER WARNING posted to Slack — see digest 2026-10-25.**
