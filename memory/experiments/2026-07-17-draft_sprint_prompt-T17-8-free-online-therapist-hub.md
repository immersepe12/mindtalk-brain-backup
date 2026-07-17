# draft_sprint_prompt: T17-8 — Free/Online Therapist Hub — 2026-07-17

## What we did
Drafted sprint prompt for a new hub page targeting the "free therapist online" + "online counsellor" cluster
(~33K/mo, YourDOST-owned, Mindtalk absent). Saved to:
`prompts/auto-drafted-sprint-free-online-therapist-hub-2026-07-17.md`

Key design decisions in the prompt:
1. Routing decision flagged for human — potential overlap with existing `/treatments/online-therapy` draft
   (2026-06-23, never fired). Recommended Option A (consolidate into existing draft) with Options B/C documented.
2. Differentiator: Mindtalk's free Riya AI sessions as the "free" gateway → converts free-intent traffic
   into paid-booking funnel. Contrasts with YourDOST's listener/EAP model.
3. AP3 Option B gate at fire time: outcome claims need Dr. Krishna K R sign-off (CBT pool, W29).
   Process/access claims (how to book, session format) do NOT need clinical sign-off.
4. FAQ spec: 5 questions min targeting "free therapist online", "free counselling online", "online counsellor
   vs therapist", "cheapest paid therapy India", "confidentiality".

## Expected outcome
Human reviewer reads the prompt within 24h, confirms routing (Option A/B/C), assigns reviewer,
and either fires via T9 or manual sprint.

## Watch
No WATCH entry until page fires. WATCH row template is included in the sprint prompt.

## Notes
- Verifier: APPROVE (2026-07-17) — draft-only, no AP violations, high goal-alignment (clicks −18% vs Q3)
- Slack notification sent (see final executor summary)
- BACKLOG: T17-8 remains active; `review_sprint_prompt` row added pointing to this prompt
- Key editorial risk: cannibalization with existing online-therapy draft — must resolve routing before fire
