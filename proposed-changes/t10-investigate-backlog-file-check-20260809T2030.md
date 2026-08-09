# Proposal: T10 Strategist — require MDX file existence confirmation before queuing investigate_regression
**Proposed:** 2026-08-09T20:30:00+05:30
**Source:** task13-meta-learner-2026-08-09
**Apply on:** 2026-08-16T20:00:00+05:30
**Status:** preview

## Issue detected

**Category 3: Missing signal — Strategist queues investigation on inferred (unconfirmed) URLs**

Root cause of STRESS-COPE-01 (BRAIN.md 2026-07-24):

> *"Lesson: investigate_regression entries must confirm the MDX file exists before queuing."*

T10 Strategist currently specifies `investigate_regression` in its action type table as:

> `| investigate_regression | Executor spawns worker | Specific cluster or URL showing drop |`

There is no constraint requiring T10 to verify that the target URL's MDX file actually exists in the repo before adding the BACKLOG row. In STRESS-COPE-01, T10 inferred a "likely" URL from a GSC keyword cluster where no MDX existed — then T11 burned a full action slot on a FALSE_SIGNAL diagnostic.

**Note:** Proposal `t11-investigate-mdx-precheck-20260809T2030.md` adds a pre-check in T11 to catch FALSE_SIGNALs before running diagnostics. This proposal fixes the root cause upstream — preventing bad BACKLOG entries from being created in the first place.

## Proposed change

**File to edit:** `cowork-tasks/task10-strategist.md`
**Edit type:** line-edit

### Before
```
| `investigate_regression` | Executor spawns worker | Specific cluster or URL showing drop |
```

### After
```
| `investigate_regression` | Executor spawns worker | Specific cluster or URL showing drop. **⚠ Before queuing: confirm the target MDX file exists in `src/content/{blogs,treatments,illnesses}/{slug}.mdx`. Do NOT queue investigate_regression for inferred/likely URLs where the file has not been verified in the repo.** If the file cannot be confirmed, queue `flag_for_human` instead with the GSC cluster data. |
```

## Rationale

T10 runs before T11 and is the source of all BACKLOG entries. Catching non-existent file targets at the Strategist level prevents FALSE_SIGNAL entries from ever entering the BACKLOG. This is strictly better than the T11 pre-check (which also exists as a defense layer) because it avoids polluting BACKLOG with dead rows in the first place.

The fix is minimal: one sentence added to the action-type constraint column. T10 already has access to the repo filesystem and can verify file existence with a 2-line bash check before writing the BACKLOG row.

## Risk assessment

Very low. This only adds a constraint to when `investigate_regression` can be queued — it does not change what happens when it is queued. The worst case is that a legitimate investigation is accidentally blocked because T10 can't reach the repo at that moment; in that case, T10 should queue `flag_for_human` instead, which is the safe fallback.

## Rollback

Snapshot: the exact "Before" block above is the pre-change table row. Revert by re-applying Before→After in reverse.
