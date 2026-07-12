# Proposal: T10 Step 10 — Verify "Before" block matches current file content before applying any proposal
**Proposed:** 2026-07-12T20:30:00+05:30
**Source:** task13-meta-learner-2026-07-12
**Apply on:** 2026-07-19T20:00:00+05:30
**Status:** preview

## Issue detected

Strategist Step 10's apply sequence goes:
1. Snapshot the target file
2. **Apply the edit per the proposal's "Before"/"After" blocks**
3. Verify (cat the modified file, check the change took effect)

There is no step between (1) and (2) that verifies the "Before" block still matches the current file content. The only safety net is the "Hard rule" at the bottom of Step 10: _"If you encounter ANY unexpected behaviour during apply (file not found, edit syntax doesn't match Before block, etc.), STOP."_

The problem: the LLM running Step 10 may not reliably detect a mismatch when instructed to "apply the edit." A partial match or a close-but-not-exact match can be silently accepted and result in an incorrect apply.

**Evidence — this already happened once:**

From `brain/memory/applied-history.md` (2026-07-05 apply of t9-tracking-db-observation-fields):

> _"Minor Before-block mismatch on t9 (proposal used `/blogs/{slug}`, file uses `/{target_dir}/{slug}`; `verified_live_at` preserved — documented in applied-history.md). Applied field changes as intended."_

The apply went through despite the mismatch, and the changes were applied "as intended" — but only because the Strategist inferred the intent and adapted. In a more complex proposal, "applying as intended" despite a mismatch could silently corrupt a task spec. The 7-day preview window exists precisely to prevent regressions; a silent mismatch-and-adapt during apply defeats that safety.

**Why mismatches happen:** A proposal filed on day 0 captures a snapshot of the "Before" text. Between day 0 and day 7, the target file may be legitimately edited by:
- Another proposal's apply
- A Kushal-directed Cowork session (e.g., 07-10 hardening session that directly edited task9, task11, task5, task16 specs)
- A T12/T16 spec amendment

If the file changed and the "Before" block no longer exactly matches, the apply could:
1. Apply in the wrong location (false positive match on similar but not identical text)
2. Apply a now-incorrect correction (the issue the proposal fixes may have already been fixed differently)
3. STOP and escalate correctly — only if the LLM reliably detects the mismatch

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task10-strategist.md`
**Edit type:** line-edit (Step 10 apply sequence — add 3a between current steps 3 and 4)

### Before

```
3. Snapshot target file to `brain/before-snapshots/{basename}-{TIMESTAMP}.bak`
4. Apply the edit per the proposal's "Before"/"After" blocks
5. Verify (cat the modified file, check the change took effect)
```

### After

```
3. Snapshot target file to `brain/before-snapshots/{basename}-{TIMESTAMP}.bak`

3a. **Before-block verification (mismatch gate):** Read the current target file content. Search for the exact "Before" block text from the proposal. The Before block must appear **verbatim** in the current file.
   - If found verbatim: proceed to step 4.
   - If NOT found verbatim: **STOP.** Do NOT apply. Post to Slack `#seo-workflow-mindtalk`:
     ```
     ⚠️ APPLY MISMATCH — proposal {id}
     File: {path}
     The "Before" block no longer matches the current file content.
     The file may have been edited since this proposal was filed.
     Manual review required before this proposal can be applied.
     Proposal left in queue as: {id}.md (unchanged, not applied, not vetoed)
     ```
     Then skip this proposal and continue to the next one. Document the mismatch in `brain/memory/applied-history.md`:
     ```
     {TIMESTAMP} | MISMATCH-SKIP | proposal: {id} | file: {path} | reason: Before block not found verbatim in current file — manual review required
     ```

4. Apply the edit per the proposal's "Before"/"After" blocks
5. Verify (cat the modified file, check the change took effect)
```

## Rationale

Adding an explicit Before-block verification step converts the current implicit "apply and hope" into an explicit check-then-apply. The mismatch gate fires before any change is made (snapshot is already taken but file is unchanged). The Slack notification gives Kushal visibility to resolve the mismatch manually (either update the Before/After blocks in the proposal to match the current file, or veto the proposal if the issue was already fixed differently).

This directly closes the gap documented in applied-history.md where a mismatch was silently handled by intent-inference. The one-time overhead (one extra file-read per proposal per apply) is negligible.

## Risk assessment

Low. The change only adds a READ step (file content check) between snapshot and apply. It cannot corrupt any file. The only downside: if the Before block has trailing whitespace or line-ending differences that prevent exact matching, a valid proposal could be blocked. Mitigation: the mismatch Slack post includes the specific proposal ID so Kushal can re-file with corrected Before/After blocks if the block is merely a whitespace mismatch.

## Rollback

Snapshot: `brain/before-snapshots/task10-strategist.md-{TIMESTAMP}.bak`

To revert: copy snapshot back. Effect of rollback: return to the current apply behavior (no Before-block verification). Any proposals that were skipped due to the mismatch gate would need to be manually applied or re-filed.

## Veto instructions

To veto: rename this file to `t10-apply-before-verify-2026-07-12-2030.vetoed.md` and add a `## Veto reason` section.
To approve early: rename to `t10-apply-before-verify-2026-07-12-2030.approved.md`.
