# Proposal: T5 — Add filterCity null-default instruction for virtual/online doctor listings

**Proposed:** 2026-11-08T14:41:00+05:30
**Source:** META-LEARNER T13 weekly run 2026-11-08T1441 (issue: CITY-LISTING-BRIEFS-FILTERCITY-FIX-01)
**Apply on:** 2026-11-15T14:41:00+05:30
**Status:** preview
**Target file:** `cowork-tasks/task5-new-content-discovery.md`
**Human-review-only:** ❌ (task-spec template instruction only)

---

## Issue detected

**BACKLOG entry CITY-LISTING-BRIEFS-FILTERCITY-FIX-01 (paraphrased from BACKLOG.md):**
> Doctor-listing briefs for virtual/online-only specialists (e.g. "online psychiatrist India", "teletherapy nationwide") must not set a city filter — there is no geographic city to constrain. T5's DOCTOR_LISTING brief template step currently has no explicit instruction for `filterCity` on virtual/online queries; without it, the task may either omit the field (breaking the MDX schema) or set it to a city name that restricts an otherwise nationwide listing.

**Root cause (BACKLOG note):** T5 Step 4's new DOCTOR_LISTING branch (Proposal 1 of this run) adds the branch but does not explicitly address the virtual/online edge case. When the SERP keyword contains "online" or "virtual" rather than a city name, the brief template should set `filterCity: null` and `serviceMode: virtual` rather than inferring a city.

**Evidence from briefs/NEW-*.md files:** Several BACKLOG-sourced keywords include purely virtual/online queries. Without explicit instruction, the brief author has no guidance for the `filterCity` field on those queries, leading to omitted or incorrect values.

---

## Proposed change

**Target:** `cowork-tasks/task5-new-content-discovery.md` — Step 4, DOCTOR_LISTING brief template instruction block (the block being added by Proposal 1 of this run)

### Edit — Append virtual/online edge-case rule to DOCTOR_LISTING brief template instruction

**Addition to Step 4 DOCTOR_LISTING branch (append after the age-group exclusion rule):**
```
Virtual/online edge case:
  - If the keyword contains "online", "virtual", "teletherapy", or "nationwide"
    (no specific city name), set:
      filterCity: null
      serviceMode: virtual
  - If the keyword names a specific city, set filterCity to that city name and
    omit serviceMode (defaults to in-person).
  - If ambiguous, default to filterCity: null and add a <!-- TODO: verify city --> comment.
```

---

## Why this is safe

- Additive instruction to task spec; no production code altered.
- The null-default is strictly safer than inventing a city name — a null field on a nationwide listing is semantically correct and renders without breaking the MDX schema.
- Recoverable: if a brief is generated with an incorrect filterCity, human can edit the MDX before Kushal merges.

---

## Rollback path

If the virtual/online rule causes incorrect brief generation:
1. Remove the virtual/online edge-case instruction block from T5 Step 4 DOCTOR_LISTING branch.
2. Strategist applies rollback at next 8 PM run.
3. Any already-generated briefs with incorrect filterCity: null are manually corrected.

---

## Diff summary

```diff
 cowork-tasks/task5-new-content-discovery.md
 Step 4, DOCTOR_LISTING branch:
 
   [age-group exclusion rule (from Proposal 1)]
+
+  Virtual/online edge case:
+    - keyword contains "online"/"virtual"/"teletherapy"/"nationwide" →
+        filterCity: null, serviceMode: virtual
+    - keyword names specific city → filterCity: <city>, no serviceMode
+    - ambiguous → filterCity: null, add <!-- TODO: verify city -->
```
