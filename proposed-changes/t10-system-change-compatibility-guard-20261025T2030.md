# Proposal: Add system-change compatibility check to Strategist Step 10 apply loop

**Proposed:** 2026-10-25T20:30 IST
**Source:** T13 Meta-Learner run 2026-10-25
**Apply on:** 2026-11-01T20:00 IST
**Status:** preview

## Issue detected

Strategist's Step 10 apply loop has a **Before-block mismatch gate** (step 3a) and a **forbidden-path check** (step 2), but **no check for system-change compatibility**. Result: a proposal written before a major system change (e.g., Vercel → Amplify migration on 2026-10-21) can auto-apply even when it references superseded infrastructure.

**Evidence:** Proposal `t9-vercel-preflight-build-block-20261018T2030.md` was queued to auto-apply on **2026-10-25T20:00 IST** — tonight — but it imports `from mcp_vercel import get_project`, which is now wrong because the system moved to Amplify on 2026-10-21. The Before-block mismatch gate would NOT have caught this because the proposal targets a block of new text (an insertion), not a replacement of existing text. T13 caught it and vetoed manually, but the detection was accidental. Without a compatibility check, any future post-migration proposal could apply harmful stale logic.

**Pattern:** The Vercel → Amplify migration is documented in `brain/BRAIN.md` as a dated system-change event. Proposals predate it (Proposed: 2026-10-18) but have Apply on: dates after it (2026-10-25). This date gap is the signal that should trigger a compatibility review before applying.

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task10-strategist.md`
**Edit type:** line-edit (insert between step 2 and step 3 in the Step 10 apply loop)

### Before

```
2. If path matches `scripts/*.py`, `src/**`, or any other production code path → SKIP and post `⚠ FORBIDDEN PATH IN PROPOSAL` to Slack. Never apply.
3. Snapshot target file to `brain/before-snapshots/{basename}-{TIMESTAMP}.bak`
```

### After

```
2. If path matches `scripts/*.py`, `src/**`, or any other production code path → SKIP and post `⚠ FORBIDDEN PATH IN PROPOSAL` to Slack. Never apply.

2b. **System-change compatibility check:** Read `brain/BRAIN.md`. Extract all dated entries between the proposal's `Proposed:` date and today. If any entry contains the word "REPO MOVE", "MIGRATION", "DEPRECATED", "REPLACED BY", or "SYSTEM CHANGE" → flag the proposal as potentially stale:
   - If proposal text contains any of: `vercel`, `netlify`, `heroku`, `mcp_vercel`, `list_deployments`, or any tool/import name that corresponds to the superseded system → **SKIP and post** to Slack `#seo-workflow-mindtalk`:
     ```
     ⚠️ COMPATIBILITY BLOCK — proposal {id}
     Proposed: {date}
     System change detected in BRAIN.md between {proposed_date} and today: {change_entry}
     Proposal text references superseded system ({matched_term}).
     Auto-apply BLOCKED. Manual review required.
     T13 Meta-Learner should write a replacement proposal for the new system.
     ```
   - If proposal text does NOT contain any superseded-system reference → proceed normally (the system change may be unrelated to this proposal's scope).

3. Snapshot target file to `brain/before-snapshots/{basename}-{TIMESTAMP}.bak`
```

## Rationale

The Before-block mismatch gate catches proposals where the *target text* no longer exists (meaning the file was independently edited). The system-change compatibility check catches proposals where the *proposed new text* references a system that is no longer in use — a distinct failure mode the mismatch gate cannot detect for insertion-type proposals.

The check is conservative: it only blocks if BOTH a system-change entry exists in BRAIN.md AND the proposal text contains a term associated with the superseded system. False positives are extremely unlikely. False negatives (a stale proposal that slips through) are less harmful than before — the system-change event is at least documented in BRAIN.md, so manual review is one grep away.

## Risk assessment

Low-medium. The check adds one file read (`brain/BRAIN.md`) and a string match per proposal per Strategist run. No writes, no API calls. The only risk is a false-positive block if "vercel" appears in a proposal for a legitimate reason (e.g., a proposal that *removes* a Vercel reference) — but that proposal would warrant human review anyway.

## Rollback

`cp brain/before-snapshots/task10-strategist-{TIMESTAMP}.bak cowork-tasks/task10-strategist.md`
The inserted block (step 2b) is clearly delimited and can be removed manually in < 60 seconds.

## Veto instructions

To veto: rename this file to `t10-system-change-compatibility-guard-20261025T2030.vetoed.md` and add a `## Veto reason` section.
To approve early: rename to `t10-system-change-compatibility-guard-20261025T2030.approved.md`.
