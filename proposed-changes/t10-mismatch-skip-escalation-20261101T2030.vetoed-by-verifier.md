# Proposal: T10 Strategist — Add MISMATCH-SKIP auto-veto escalation after 5 consecutive skips

**Proposed:** 2026-11-01T20:30:00+05:30
**Source:** META-LEARNER T13 weekly run 2026-11-01T2030
**Apply on:** 2026-11-08T20:00:00+05:30
**Status:** preview

## Issue detected

The Strategist's Step 10 MISMATCH-SKIP mechanism has no escalation path. When a proposal
has a wrong "Before" block, the Strategist silently skips it every single daily run — forever.
Evidence: `t12-algo-watch-dual-sensor-tiebreaker-20261018T2030` accumulated 8 consecutive
MISMATCH-SKIPs (Oct 25 – Nov 1, 14 days of wasted daily runs) before T13 detected it.
Historical precedent: proposals `t16-read-pending-human-actions-2026-07-26-2030` and
`t5-floor-miss-brain-flag-2026-07-26-2030` both reached 20+ MISMATCH-SKIPs before Kushal
manually cleared them.

The existing stale-proposal scan (14-day overdue threshold) is date-based, not MISMATCH-SKIP
count-based. A proposal can accumulate MISMATCH-SKIPs for less than 14 days (e.g., 7 days of
daily runs = 7 skips, no stale alert yet). This created a gap: stuck proposals sit silently in
the queue for 1–3 weeks before any alert fires.

**Pattern:** Every stuck proposal in the history had a wrong "Before" block that T13 filed
incorrectly. The fix is: after 5 MISMATCH-SKIPs on the same proposal, auto-veto it and Slack
a re-file request. This catches stuck proposals faster than the 14-day stale alert (which
only fires after Apply-on + 14 days, not after N skips).

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task10-strategist.md`

**Edit type:** line-edit (append MISMATCH-SKIP escalation rule after the mismatch documentation block in Step 10 3a)

### Before

```
     Then skip this proposal and continue to the next one. Document the mismatch in `brain/memory/applied-history.md`:
     ```
     {TIMESTAMP} | MISMATCH-SKIP | proposal: {id} | file: {path} | reason: Before block not found verbatim in current file — manual review required
     ```
```

### After

```
     Then skip this proposal and continue to the next one. Document the mismatch in `brain/memory/applied-history.md`:
     ```
     {TIMESTAMP} | MISMATCH-SKIP | proposal: {id} | file: {path} | reason: Before block not found verbatim in current file — manual review required
     ```
     **MISMATCH-SKIP escalation (5-skip auto-veto):** After documenting, count the total MISMATCH-SKIP entries in `brain/memory/applied-history.md` containing this exact proposal ID string. If the count is ≥ 5:
     1. Rename the proposal file: `{id}.md` → `{id}.vetoed.md` (auto-veto — stuck proposals do not self-resolve).
     2. Post to `#seo-workflow-mindtalk` (channel `C0AUAPS4J83`):
        ```
        🚨 AUTO-VETO — proposal {id} stuck after {N} MISMATCH-SKIPs
        The "Before" block has never matched the target file content in {N} consecutive Strategist runs.
        Proposal auto-vetoed to clear the queue.
        Action required: T13 should re-file with a corrected "Before" block at the next weekly run.
        ```
     3. Append to `brain/memory/applied-history.md`:
        ```
        {TIMESTAMP} | AUTO-VETOED | proposal: {id} | reason: {N} consecutive MISMATCH-SKIPs — Before block never matched, proposal auto-cleared
        ```
```

## Rationale

Evidence from this system's history: stuck proposals accumulate silently until a human or T13
notices. The t12 proposal had 8 skips; prior proposals had 20+. The 5-skip threshold is
conservative (catches stuck proposals after ~5 daily Strategist runs, ~5 days) while giving
a legitimate proposal enough tries in case of transient file-read issues (rare but possible).
The auto-veto does not destroy the proposal's intent — T13 or a human can re-file with the
correct Before block. The Slack notification ensures visibility.

This closes the gap between "MISMATCH-SKIP" (single-run) and "STALE-ALERT" (14+ days overdue)
with a count-based escalation that fires before the date-based alert.

## Risk assessment

Low. The auto-veto only fires after 5 confirmed mismatches — not on the first skip. A proposal
with a valid Before block that temporarily fails (e.g., file temporarily unavailable) would not
hit 5 consecutive mismatches in practice. The worst case: a legitimate proposal with a subtly
wrong Before block gets auto-vetoed at skip #5 instead of persisting indefinitely. That is the
correct outcome — the proposal should be re-filed with the correct Before block.

## Rollback

Remove the **MISMATCH-SKIP escalation (5-skip auto-veto)** block from Step 10 3a. The Strategist
reverts to the previous behaviour: MISMATCH-SKIP → document → continue, with no escalation.
Any auto-vetoed proposals remain vetoed; they must be manually re-filed if still needed.

## Veto instructions

To veto: rename to `t10-mismatch-skip-escalation-20261101T2030.vetoed.md`.
To approve early: rename to `t10-mismatch-skip-escalation-20261101T2030.approved.md`.
