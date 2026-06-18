# NEEDS_HUMAN — ERT round-2 recovery research — 2026-06-16

**Raised by:** Executor (T11) 16:35 IST · **Verifier verdict:** NEEDS_HUMAN
**BACKLOG row:** #5 · **Decision owner:** Kushal

---

## What was proposed (BACKLOG #5)

A **read-only** round-2 investigation of `/treatments/exposure-response-therapy-ert`:
- SERP + entity analysis for "exposure and response prevention therapy" / "ERP therapy OCD" (which entity Google associates, who ranks).
- Read the existing follow-up brief + gsc-data + git log to understand why the round-1 body fix failed.
- Evaluate the structural hypothesis that the **slug + title carry the wrong entity** ("-ert" vs the canonical "ERP").
- Output a recommendation (e.g. staged 301 → `/exposure-and-response-prevention-erp` + title/H1 rewrite) — **for human sign-off only**. No migration, no edit, no push.

## Why the Verifier routed it to you (not auto-run)

The research itself is path-safe and not a literal AP3/AP1 breach (nothing on the YMYL page changes; output goes to `brain/memory/`). **But three factors converge:**

1. **§8 prior-failure rule.** Round-1 (a body-content fix, commit `ff7f459`, 2026-05-28) already **FAILED** its 14-day evaluation on this exact target (06-11 RECOVERY_FAILED). The Verifier treats a second recovery pass on a page that already failed one remediation as a human-gated decision.
2. **YMYL "manual only" gate.** This is a `/treatments/` page. Round-2's entire purpose is to tee up a **301 + title/H1 migration** on a YMYL URL — one step from an AP1-class staged-rollout risk that the engine must never fire autonomously.
3. **algo_watch hold.** The page is in the current "Held this cycle" list (May core update receding; resume ~06-23). Acting now adds ranking-attribution noise mid-rebound.

Plus a drift-prevention concern: letting the loop autonomously run "round-2 recovery research" on a failed YMYL page normalises it steering its own YMYL strategy. That should be a Kushal-surfaced step.

## What I need from you (pick one)

- [ ] **Approve the research only** — I (or a future Executor run) may do the read-only SERP/entity analysis and write a recommendation. Migration still needs a separate explicit sign-off.
- [ ] **Approve research + pre-authorise a *staged* migration** — research, then ship the 301 to a 10% sample first with a 7-day rank-stability check before full rollout (AP1-compliant).
- [ ] **Hold until after 06-23** — let the core update finish settling first (recommended; matches the algo_watch hold on this page).
- [ ] **Drop it** — deprioritise round-2 entirely.

## Context / evidence pointers

- Prior-failure brief: `briefs/recovery-followup-exposure-response-therapy-ert-2026-06-11.md`
- Round-1 commit: `ff7f459` (2026-05-28, body fix)
- BACKLOG row: `brain/BACKLOG.md` #5 (now tagged ESCALATED)
- Verifier full reasoning: `brain/memory/verifier-log.md` (2026-06-16 16:35 IST line)
- algo_watch hold list: `brain/BACKLOG.md` → "Held this cycle"

**No action taken on the page. Awaiting your call.**

---

## DECISION — 2026-06-17 12:30 IST (Kushal)

**Verdict: HOLD until 2026-06-23**

Reasoning: Sprint A/B/C 14-day readouts arrive 06-23. That data will reveal which lever works during YMYL algo settle. Round-1 already failed — repeating without new information ≠ different outcome. Waiting 6 days is free, page hasn't disappeared.

After 06-23 Strategist re-reads ERT context with Sprint readout evidence + decides between:
- meta-only round (if Sprint C recovered)
- reviewer/E-E-A-T treatment (if Sprint A recovered)
- AI Overview defense (if Sprint B recovered)
- structural URL migration (if all 3 sprints stayed flat)

**Status:** ESCALATED → HELD until 2026-06-23
