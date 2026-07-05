# Proposal: T9 write verifier rejection notes back into brief file

**Proposed:** 2026-07-05T20:00:00+05:30
**Source:** task13-meta-learner-2026-07-05
**Apply on:** 2026-07-12T20:00:00+05:30
**Status:** preview

## Issue detected

When T9's safety filters reject a brief, the only record is in `logs/auto-ship-{TODAY}.txt`. The brief file itself (`briefs/NEW-{slug}-brief.md`) is left unchanged — there is no record inside the brief of why it was rejected or what needs to be fixed.

**Evidence from this week:**

- `logs/auto-ship-2026-07-03.txt` — `domineering-vs-dominating` rejected: §5 metaDesc >160ch + §9 cluster cap + word count est. <1,200. Now under `verifier_vetoed_until=2026-07-08`.
- `logs/auto-ship-2026-07-03.txt` — `what-is-de-addiction` rejected: §5 metaDesc >160ch + §5 FAQ 4 <5 + §9 cluster cap + word count est. <1,100. Same veto expiry.

Both briefs have been sitting in `briefs/` since at least 2026-07-01. When the veto lifts on 2026-07-08, Executor T11 or a human must fix the brief before T9 can ship it. But there is no note inside the brief file listing what to fix — the fixer must hunt through `logs/auto-ship-2026-07-01.txt`, `logs/auto-ship-2026-07-03.txt`, and `logs/auto-ship-week-2026-06-29.txt` to piece together the failure reasons. This is a direct contributor to the brief being stuck for 7+ days without a fix attempt.

The auto-ship log is authoritative but task-run-scoped. The brief file persists; the log scrolls off. Rejection notes belong in the brief.

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task9-auto-ship-new-blogs.md`
**Edit type:** line-edit

### Before

```
If a brief fails ANY safety filter, SKIP it (don't ship), log the reason to `logs/auto-ship-{TODAY}.txt`, but continue with the next brief.
```

### After

```
If a brief fails ANY safety filter, SKIP it (don't ship), log the reason to `logs/auto-ship-{TODAY}.txt`, **and append a T9 rejection block to the brief file itself** so that Executor T11 or a human fixing the brief can see the exact failure list without reading auto-ship logs:

Append to the end of `briefs/NEW-{slug}-brief.md`:

```markdown
---
## ⚠ T9 Verifier Rejection — {TODAY}
**Veto active until:** {verifier_vetoed_until date, or "N/A — fix required before retry"}
**Failure reasons:**
- {failure 1, e.g., §5 metaDesc length: 166ch (limit 160ch) — shorten by 6 chars}
- {failure 2, e.g., §5 word count est. ~1,050 (minimum 1,200) — expand body}
- {failure 3, e.g., §9 cluster cap: /blogs/ at 3/3 — wait until {date}}
**Fix these before next T9 run.** When fixed, T9 will retry automatically on next eligible run date.
```

After appending, continue with the next brief candidate.
```

## Rationale

Rejection reasons belong in the file being fixed, not in a time-stamped log file that the fixer must hunt. This change means:

1. Executor T11 can read `briefs/NEW-{slug}-brief.md` and immediately see what to fix.
2. Humans reviewing the briefs folder see rejection status at a glance.
3. No change to any Python script — the append is performed by the Claude agent running T9 (same as how T9 currently writes to `logs/auto-ship-{TODAY}.txt`).

With this change, the two currently-stuck briefs (domineering, de-addiction) would already have their fix list embedded. Estimated fix time for Executor: 5 minutes per brief vs ~20 minutes hunting logs.

## Risk assessment

Low. Appending to a brief file is additive and non-destructive. The worst case: the appended block is malformed (e.g., contains a stray `---` that confuses a downstream reader) — this is easily spotted and the brief file is not parsed by any script. The brief file is read by T9, Executor T11, and humans — all of whom can handle an appended markdown section.

One edge case: if a brief is rejected for a cluster-cap reason (§9) that will self-clear, the "Fix these" wording may be misleading. The template handles this by including the specific cap-clear date in the §9 failure line.

## Rollback

Snapshot: `brain/before-snapshots/task9-auto-ship-new-blogs.md-{TIMESTAMP}.bak`

To revert: copy snapshot back. Already-appended rejection blocks in brief files are harmless — leave them in place or delete manually. They do not affect T9 logic (T9 reads the brief's YAML/metadata, not the trailing rejection block).

## Veto instructions

To veto: rename to `t9-rejection-notes-to-brief-file-2026-07-05-2000.vetoed.md` and add `## Veto reason`.
To approve early: rename to `t9-rejection-notes-to-brief-file-2026-07-05-2000.approved.md`.
