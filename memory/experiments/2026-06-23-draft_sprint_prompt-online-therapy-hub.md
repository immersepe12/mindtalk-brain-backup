# draft_sprint_prompt: Online Therapy Hub Page — 2026-06-23

## What we did

Drafted a full sprint prompt for a new "online therapy india" hub page targeting the commercial cluster:
- therapy online india (~5k/mo)
- therapist online (~6k/mo)
- online counsellor (~3k/mo)
- psychological consultation online (~3k/mo)

Combined addressable: ~17k impr/mo at maturity. Mindtalk currently has zero presence on these terms.

Prompt saved to: `prompts/auto-drafted-sprint-online-therapy-hub-2026-06-23.md`

**NOT fired.** Human-gated before execution. Verifier APPROVED the draft action.

## Key design decisions in the prompt

1. **YMYL routing flag**: Kushal must decide /blogs/ vs /treatments/ path before fire. Prompt recommends /treatments/ for E-E-A-T alignment with competitors.
2. **P10 interactive element**: "What type of therapy do you need?" self-matcher (5–6 questions → routed results). Required for AEO/AI citation — FAQ-only insufficient (Sprint B precedent).
3. **P11 meta specificity**: "Online Therapy in India: 72+ Verified Therapists | Mindtalk" — number + credibility token, no geo-commercialisation.
4. **AEO structured-answer blocks**: Every FAQ is a complete standalone sentence; NIMHANS 2022 + ₹1,250 in plain text (not tables); entity clarity (Mindtalk + Cadabams Group mentioned).
5. **AP2 direct CTAs**: All booking links use direct `/doctors`, `/experts/expert-therapists`, `/doctors/telugu-speaking-doctors` paths — no auth wraps.
6. **6 required internal links**: /doctors, /experts/expert-therapists, telugu/tamil-speaking-doctors, /assessments.

## Expected outcome

Draft only → enables human-confirmed fire. At maturity (6+ months):
- 3,000–8,000 impr/wk on primary cluster
- 45–120 clicks/wk (commercial intent → higher CTR than discovery blogs)
- AI Overview citation on "therapy online india" within 4–8 weeks if interactive element included

## Watch

No watch opened (draft only, nothing shipped). Watch row to be added at fire time (14-day post-fire check).

## Notes

- This is the highest P9-weighted executable action: commercial booking-intent terms, Goldmine-feeder by design
- Sprint B precedent (P10): interactive content = AI citation reclaimed. This page must have interactive element.
- Sprint C caution (P11): bulk meta-rewrite inconsistency → net negative. Avoid inconsistent execution. The meta is fully specified in the prompt; follow it exactly at fire time.
- T17-4 AEO requirements folded into brief per Verifier condition #6.
