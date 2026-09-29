# Proposal: t5-gate-enforcement-mandatory-log

**Proposal-ID:** t5-gate-enforcement-mandatory-log-20260927T2030
**Raised-by:** T13-Meta-Learner
**Issue-category:** Gate bypass / silent pass
**Raised-on:** 2026-09-27
**Apply-on:** 2026-10-04T20:00:00+05:30
**Affects-task:** T5 (new-content-discovery)
**Priority:** HIGH
**Rollback:** Revert Step 5.5 gate lines in task5-new-content-discovery.md to the previous `[PASS/FAIL]` notation.

---

## Issue

T20 tagged `T5-GATE-NOT-APPLIED-01` on 2026-09-22: "T5 ran on 09-21 with gates in spec but applied neither; 4 briefs re-authored as duplicates; cap appeared '20/20' but was really '16/20'."

Root cause: the current spec uses `[PASS/FAIL]` placeholder notation for the query-ownership and collision checks. This notation does not require any actual log output — a run can write `[PASS]` against every brief without performing the lookup. There is no machine-verifiable evidence that either gate ran. T5 can silently pass all briefs, pollute the tracking-db with duplicates, and exhaust the weekly cap on invalid entries.

---

## Proposed Change

**File:** `cowork-tasks/task5-new-content-discovery.md`

**Action:** Replace the two `[PASS/FAIL]` gate lines in Step 5.5 with mandatory log-line enforcement.

### Before:

```
- [PASS/FAIL] **Query-ownership gate:** no live URL holds the query on page 1 (owner + numbers logged)
- [PASS/FAIL] **Collision check:** slug absent from all content collections, live route 404, no queued brief for the same file
```

### After:

```
- [ ] **Query-ownership gate (MANDATORY — log line required):** Pull GSC for this exact query (rowLimit 25, dateRange 28d). If any URL returns ≥50% CTR share at position ≤15, **SKIP** this brief. Log line MUST appear in `logs/new-content-{TODAY}.txt` for every brief: `"OWNERSHIP: /page/X {pct}% @ pos {n} → SKIP"` OR `"OWNERSHIP: no page-1 holder → PROCEED"`. A run log that omits this line for any brief = gate not run = that brief is INVALID and must not be counted toward the floor or cap.
- [ ] **Collision check (MANDATORY — log line required):** grep `src/content/**/*.mdx` slugs + `briefs/*.md` Suggested-File fields + tracking-db BRIEF_CREATED keys. Log line MUST appear for every brief: `"COLLISION: {match in source} → REJECT"` OR `"COLLISION: no collision → PROCEED"`. A run log that omits this line for any brief = check not run = that brief is INVALID and must not be counted toward the floor or cap.
```

---

## Filters

- **Forbidden-path check:** PASS — `cowork-tasks/task5-new-content-discovery.md` is an allowed path
- **Anti-pattern check:** PASS — AP7 ("never queue brief for URL already in BRIEF_CREATED") is the motivating principle; this enforces it more strictly
- **Duplicate check:** PASS — the applied `t5-query-ownership-gate-20260920T2030` proposal added the gate to the spec; this proposal strengthens enforcement to require log output. Different scope, no 30-day duplicate conflict.
- **INTENT-PRIORITY.md protection:** PASS — not related to intent classification

## Rollback Path

Revert the two gate lines in `cowork-tasks/task5-new-content-discovery.md` to the original `[PASS/FAIL]` notation. No other files affected.
