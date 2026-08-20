# NEEDS_HUMAN — Clinical sign-off required: `/blogs/therapy-for-gambling-addiction`

**Routed here:** 2026-08-18 by T20 Auto-Remediation, on Verifier VETO §F.
**Brief:** `NEW-therapy-for-gambling-addiction-brief.md` (in this folder).
**Do NOT auto-ship.** T20 and T9 must not pick this up from `briefs/` — it has been moved out of the active queue deliberately.

## Why it is here

The brief targets a `/blogs/` path, so it passes the *path* test that normally keeps T20 out of YMYL. But the Verifier judged the **content** to be YMYL regardless of path:

- H2 1 ("When Gambling Stops Being a Habit and Becomes an Addiction") + H2 2 ("Warning Signs in Yourself or a Family Member") together constitute a self-assessment screen for **Gambling Disorder, a named DSM-5 diagnosis**.
- H2 4 ("How CBT Works for Gambling Addiction") is a treatment-mechanism claim.
- H2 5 ("Treating What Sits Underneath: Anxiety, Depression, Debt Stress") is comorbidity treatment.

The brief's own guard ("no DSM-5 checklist, no success rates, no medication") contradicts the H2 structure it is attached to. Verifier's phrasing: *"a `/treatments/` page in a `/blogs/` costume."*

The brief already contains the correct trigger — *"If the draft requires any of these, stop and route the brief to the YMYL clinical sign-off queue"* — the Verifier's finding is that the trigger is met at **brief** stage, not draft stage.

## The decision Kushal / a clinician needs to make

**1. Sign-off (clinical).** Does a named clinician approve this scope, per AP3 Option B (`clinical_reviewer_signed_off`, named + dated ≤90d)? Proposed reviewer `santanu-tripathy` (addiction vertical, reviewed `/blogs/drug-addiction-symptoms`; load 2/5, within cap).

**2. Duty of care (Kushal).** The brief itself notes gambling debt correlates with suicidality, then — correctly, per the current feature flag — forbids any crisis pathway, helpline or safety content. That leaves a page which attracts distress traffic and offers no crisis route. That combination is a human call, not a verifier call. Options:
   - (a) Ship with the current no-crisis-content flag and accept the gap;
   - (b) Ship only once the suicide-safety feature flag is cleared for clinical sign-off, so a crisis block can be included;
   - (c) Narrow the page to non-clinical scope (recognition + where to get help only — drop H2 4 and H2 5), which takes it out of YMYL entirely and lets T9 ship it normally.

**T20's recommendation: (c)**, then (b) later as a fuller page. (c) preserves the opportunity — the cluster is genuinely uncontested — without asking a clinician to sign off on a blog.

## Evidence (verified, reconciles exactly to source)

- Paid: `therapy for gambling addiction near me` — **1.0 conversion**, 2 clicks, 30d, Google Ads account 2992649306. Source: `logs/t20-paid-terms-2026-08-18.json`.
- AP9 (**corrected** — the brief's original "no file matches 'gambl'" claim was FALSE and came from a filename scan of a stale checkout): 13 files mention gambling in passing. No dedicated page. Nearest are `/illnesses/addiction` (has a dedicated `Gambling Addiction:` bullet under types of addiction) and `/blogs/guide-to-overcoming-gaming-addiction` (gaming ≠ gambling, but adjacent to the brief's H2 3 and its `fantasy sports addiction` related keyword).
- If revived, the brief must carry: *"Must not restate the behavioural-addiction definition already on `/illnesses/addiction`; link to it."*

## Blocking note

Even if approved, `/blogs/` cluster cap is **7/6 for the 7 days from 2026-08-18** (T9 shipped 7 today). Nothing in this batch may ship before **2026-08-25**.
