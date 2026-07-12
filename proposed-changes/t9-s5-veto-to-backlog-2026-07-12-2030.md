# Proposal: T9 — Create BACKLOG fix_brief item when brief fails content-quality validation (not self-healing failures)
**Proposed:** 2026-07-12T20:30:00+05:30
**Source:** task13-meta-learner-2026-07-12
**Apply on:** 2026-07-19T20:00:00+05:30
**Status:** preview

## Issue detected

T9 has two classes of brief rejection:

**A. Self-healing rejections** — cluster cap (§9): the cap resets after 7 days, so the brief automatically becomes retry-eligible without any action required. T9 correctly logs and retries.

**B. Content-quality rejections** — word count < 1,200, metaDesc > 160 chars, FAQ < 5 questions (Step 3 sub-step 4 "Validate before write"): these require a **human or T11 Executor to edit the brief file** before the next T9 attempt. They do NOT self-heal.

Currently, both classes are treated identically: T9 logs the failure to `logs/auto-ship-{TODAY}.txt` and moves on. The pending `t9-rejection-notes` proposal (applying tonight, 2026-07-12) improves visibility by also appending the failure list into the brief file itself. But the brief file sitting in `briefs/` with a rejection block is still invisible to T11 Executor unless T11 explicitly reads every brief file. T11 reads BACKLOG.md, not brief files.

**Evidence:**

- `briefs/NEW-what-is-de-addiction-brief.md`: vetoed 2026-07-03 for §5 wc 1,126 < 1,200 + §9 cap. Vetoed again 2026-07-10 for §9 cap only (the §5 word count issue was never fixed). The brief has been stuck for **9+ days** with no BACKLOG item prompting anyone to fix it.
- No entry for "fix de-addiction brief word count" exists anywhere in BACKLOG.md.
- T11 Executor's BACKLOG-scanning loop will never see this brief needs fixing — it only sees items explicitly queued in BACKLOG.

**The gap:** content-quality fix tasks (class B) need to be in BACKLOG to enter T11's work queue. They currently aren't.

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task9-auto-ship-new-blogs.md`
**Edit type:** line-edit (Step 3 sub-step 4, add a step 4a after the validation block)

### Before

```
4. **Validate before write:**
   - Title char count ≤ 65, includes "Mindtalk"
   - Meta description ≤ 160 chars
   - FAQ has exactly 5 questions
   - At least 3 internal links present
   - Word count ≥ 1,200 (typical brief target)
   - All `<Component>` references actually exist in `src/components/`
```

### After

```
4. **Validate before write:**
   - Title char count ≤ 65, includes "Mindtalk"
   - Meta description ≤ 160 chars
   - FAQ has exactly 5 questions
   - At least 3 internal links present
   - Word count ≥ 1,200 (typical brief target)
   - All `<Component>` references actually exist in `src/components/`

4a. **If any Step 3/sub-step 4 validation check fails:** the brief fails a **content-quality failure** (not a self-healing cluster-cap failure). Do NOT write the MDX. Instead:

   - Log the specific failures to `logs/auto-ship-{TODAY}.txt` (as currently done).
   - Append the T9 rejection block to the brief file (as per `t9-rejection-notes` spec).
   - **Additionally, append a `fix_brief` action to BACKLOG.md** so T11 Executor sees and acts on it:

     Append under `## Operational items` in BACKLOG.md:
     ```
     | fix_brief | `briefs/NEW-{slug}-brief.md` | **Content-quality fix required before T9 can ship.** Failures: {failure-list, e.g., "wc 1,126<1,200 (need +74 words)" + "FAQ 4<5 (need 1 more question)"}. T9 retries automatically once the brief is updated — no manual ship trigger needed. First vetoed: {TODAY}. | Low effort per fix | H | L | T11 Executor — fix this week |
     ```

   - Cluster-cap rejections (Step 2 rule 5/6) are self-healing — do NOT add BACKLOG items for those. BACKLOG items are only for content-quality failures that require someone to edit the brief.

   - **Deduplicate:** before appending to BACKLOG, check if a `fix_brief` row for `briefs/NEW-{slug}-brief.md` already exists in BACKLOG. If it does, update the existing row's failure list and "First vetoed" date rather than adding a duplicate.
```

## Rationale

Content-quality brief failures require editorial action (expand word count, trim metaDesc, add an FAQ question). These tasks are exactly what T11 Executor is built for — but only if they appear in BACKLOG. Adding them to BACKLOG closes the feedback loop:

T9 rejects brief → BACKLOG item created → T11 reads BACKLOG → T11 fixes brief → T9 ships on next retry

Without this, the loop is:
T9 rejects brief → brief sits in `briefs/` → nobody fixes it → T9 rejects again next week

The de-addiction brief is the concrete example: 9+ days vetoed, no fix, no BACKLOG item, same failure each run. After this proposal applies, the next T9 rejection of an un-fixed brief will create a BACKLOG item, making the fix visible to T11 without anyone hunting through auto-ship logs.

The deduplication check (4a last bullet) ensures T9 doesn't flood BACKLOG with repeat entries on the same brief across multiple rejected runs.

## Risk assessment

Low. T9 is adding one BACKLOG.md append and a deduplication check — both read/write operations on brain files, not production code. Worst case: the BACKLOG append is malformed and adds a confusing row. T11 Executor sees clearly-labeled `fix_brief` rows and will skip any it can't parse. Rollback removes the rule; existing BACKLOG entries would need manual cleanup if rollback is needed urgently.

## Rollback

Snapshot: `brain/before-snapshots/task9-auto-ship-new-blogs.md-{TIMESTAMP}.bak`

To revert: copy snapshot back. Any `fix_brief` BACKLOG items already created would remain in BACKLOG but would stop being generated by future T9 runs. They can be manually removed from BACKLOG or left as informational.

## Veto instructions

To veto: rename this file to `t9-s5-veto-to-backlog-2026-07-12-2030.vetoed.md` and add a `## Veto reason` section.
To approve early: rename to `t9-s5-veto-to-backlog-2026-07-12-2030.approved.md`.
