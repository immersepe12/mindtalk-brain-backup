# Proposal: Formalize AP12 — never modify a url_locked page during its open observation window
**Proposed:** 2026-08-30T20:30:00+05:30
**Source:** task13-meta-learner-2026-08-30
**Apply on:** 2026-09-06T20:00:00+05:30
**Status:** preview

## Issue detected

T11 Executor (2026-08-11) flagged AP12 with the note "AP12 PROPOSED (url_locked violation pattern confirmed) — Learner to formalize." As of 2026-08-30, T12 has not written AP12 to `brain/ANTI-PATTERNS.md`. The rule is sitting informally in BRAIN.md only.

Confirmed violation: CANNIBAL-BLOG-01 (commit `59c3c5a`, 2026-07-20) modified a url_locked MDX file (`/treatments/online-therapy`) 3 days after its Day-21 midpoint. T11 flagged this as potentially accelerating the Day-42 regression (W18 verdict: HIGH_PRIORITY_DROP + QDF_BLOCKED; `brain/memory/experiments/investigation-online-therapy-w18-2026-08-11.md`). This is the 1st confirmed instance, but the T11 Executor specifically called it out as a pattern that needs formalization.

Without a formal AP12 in ANTI-PATTERNS.md, T9 Verifier has no spec reference to check url_locked status before shipping, and T11 has no spec reference to cite when flagging future violations.

## Proposed change
**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/brain/ANTI-PATTERNS.md`
**Edit type:** append

### Before
```
- Established: 2026-06-29 (after the 06-26 stuck-branch incident), 1 confirmed instance.

---

(Learner appends new anti-patterns when closed watch windows reveal harmful actions to avoid.)
```

### After
```
- Established: 2026-06-29 (after the 06-26 stuck-branch incident), 1 confirmed instance.

## AP12. Never modify a url_locked page during its open observation window
- **What happened:** CANNIBAL-BLOG-01 (commit `59c3c5a`, 2026-07-20) modified `/treatments/online-therapy` 3 days after its Day-21 midpoint, while the watch (W18) was still open. T11 Executor flagged this as likely accelerating the QDF freshness decay and contributing to the Day-42 HIGH_PRIORITY_DROP verdict. The online-therapy page lost its primary keyword ranking ("online therapist") from Day-21 to Day-42; T11 noted internal modification during observation as a compounding cause (`memory/experiments/investigation-online-therapy-w18-2026-08-11.md`).
- **Why it harms:** A url_locked page is in a live observation window — any modification changes the treatment variable being measured. If the page recovers or regresses after modification, the verdict is confounded (we can't attribute the outcome to the original action). Additionally, freshness-sensitive pages may lose a QDF boost if re-crawled after a content change mid-window.
- **Rule:** Between a watch open date and its final Day-42 verdict date, no task (T9, T11) may modify the target MDX file. Concretely:
  1. **T9 Verifier** (Step 3): before shipping any page, check `tracking-db.json` for `url_locked: true` on the target path. If locked → VETO with reason "AP12: url_locked observation window active (closes {url_locked_until})."
  2. **T11 Executor**: before firing any sprint or refresh on a page, check tracking-db for `url_locked`. If locked and lock expiry is > today → defer action to `url_locked_until + 1 day` and add a BACKLOG row with that hold date.
  3. **Exception:** Emergency CWV or security fixes may proceed with explicit Kushal approval recorded in `brain/memory/decisions/`.
- **Established:** 2026-08-30 (Meta-Learner), flagged 2026-08-11 by T11, 1 confirmed violation instance (CANNIBAL-BLOG-01). Threshold for ANTI-PATTERN is ≥3 closed failures of same class, but this is a prevention rule (a 2nd violation would be hard to disentangle from other causes) — formalizing at 1 instance with T11 explicit flag.

---

(Learner appends new anti-patterns when closed watch windows reveal harmful actions to avoid.)
```

## Rationale
AP12 is already being cited by T11 in experiments files but has no formal entry in ANTI-PATTERNS.md. Without the formal entry, T9 Verifier and T11 have no spec reference and cannot enforce the rule systematically. The violation cost was a corrupted 42-day observation on a Tier A page (/treatments/online-therapy). Formalizing prevents future observation-window contamination across all content types.

## Risk assessment
Low. This is a documentation/formalization change only. The rule itself is already being applied informally. Slight risk of T9 over-vetoing if url_locked_until is populated incorrectly in tracking-db — but T9 already checks url_locked for other purposes.

## Rollback
Snapshot target file before apply: `brain/before-snapshots/ANTI-PATTERNS-20260906T200000.bak`
Remove the AP12 block (everything from `## AP12.` to `---`) to revert.
