# Proposal: T5 Step 2 + Step 7 — Enforce 12-brief floor as mandatory gate and fix output header
**Proposed:** 2026-07-19T20:30:00+05:30
**Source:** task13-meta-learner-2026-07-19
**Apply on:** 2026-07-26T20:00:00+05:30
**Status:** ✅ APPLIED EARLY 2026-07-20T11:45:00+05:30 (Kushal-directed Cowork session — 7-day preview waived, same precedent as 2026-07-10 hardening pass. Reason: T5's 07-20 scheduled run hit this exact bug again — "5/5 quota" pattern repeated verbatim — one day into the preview window, with the `/blogs/` cap resetting 07-21 and T9 needing a fresh runway. Waiting for 07-26 would have meant a second missed week.)

## Applied — with one extension beyond the original proposal

Edit A and Edit B applied verbatim as drafted below. **One addition made during apply** (not in the original Meta-Learner draft): an **INTENT/REDUNDANCY GATE** appended to the end of the BRIEF COUNT GATE block. Rationale: while topping up this week's queue by hand to diagnose the floor miss, an audit of `new-content-opportunities.json` (4,681 OPPORTUNITY-status entries) found the cached queue itself is heavily contaminated — a large fraction of high-impression "opportunities" are GSC long-tail query variants of pages that **already cover that exact topic** (e.g. "dominating" / "dominant man meaning" / "being dominant meaning" all pointing at the same existing `understanding-dominant-personality-and-dominating-nature` blog), or are the AP9 cannibalization pattern the system already learned to avoid (e.g. "emdr full form", "psychotherapist" pointing at `/treatments/psychotherapy` — restating the treatment's own name). Tier-expanding volume thresholds alone (the original proposal's fix) would surface *more* of this contamination, not genuinely new topics, because Step 3b (live SERP research, which would normally catch this) never runs in cached mode. The redundancy gate closes that hole without needing live SERP research — it's a cheap slug/keyword overlap check plus the existing AP9 rule, run at candidate-selection time instead of relying on downstream triage that cached mode skips.

**Also found:** today's 5 briefs (what-is-group-therapy, what-is-couple-therapy, common-relationship-issues, what-is-meditation-therapy, types-of-counselling) were generated before this gate existed — 4 of the 5 have triggering pages that are `/treatments/{same-modality}` and would not have passed the new gate. Flagged to Kushal for a keep/redo decision; not auto-reverted (these are still in BRIEF_CREATED status, not yet shipped by T9, so there's a review window before any production risk).

---

## Issue detected

**Log evidence:** `logs/new-content-2026-07-13.txt` header reads `"Keywords Selected This Week (5/5 quota)"` — T5 selected only 5 keywords and treated "5/5" as a full quota, despite the 12-brief floor added to the spec on 2026-07-10.

**Root causes (two separate gaps):**

1. **Step 2 — no hard enforcement gate.** The floor is written as a `**bold note**` block AFTER the filter logic and AFTER "Take the top 20…" instruction. When T5 ran in cached mode (discovery script failed → google-auth not installed → fell back to existing new-content-opportunities.json), the agent selected 5 matching candidates, saw "5 is the best I can do", and exited. The floor note says "create a MINIMUM of 12 unless queue is genuinely exhausted" but provides no actionable gate to enforce this before proceeding.

2. **Step 7 — output header has no reference to floor or correct cap.** The Step 7 template says: "Keywords selected this week with their type and search volume / Running count of new content briefs created this month". No mention of floor (12) or cap (20). The agent generated "5/5 quota" from its own internalized old spec. The output template must match the cap + floor to anchor the agent's self-reported count format.

**Hardening verification 2026-07-17:** FAIL #2 — "The raised floor never made it into the T5/T3 task prompts — they're still operating on 5/wk NEW + 10/wk combined." Action item: `T5-FLOOR-12-01`. This proposal is the fix.

## Proposed change
**File to edit:** `cowork-tasks/task5-new-content-discovery.md`
**Edit type:** two line-edits (Step 2 floor block + Step 7 body)

### Edit A — Step 2: Add mandatory BRIEF COUNT GATE immediately after the floor note

#### Before (lines 82–89)
```
Take the top **20 highest-priority opportunities this week** (unchanged cap).

**FLOOR (added 2026-07-10, Kushal-directed): create a MINIMUM of 12 briefs per weekly run** unless the filtered queue is genuinely exhausted. Recent runs produced only 5/week while the 20-pages/week live target requires T9 to never starve (runway rule: keep ≥15 unshipped briefs in tracking-db at all times — T16 now monitors this). If you create fewer than 12, the run log MUST state exactly why (e.g., "queue exhausted after filters: only 9 passed"). Quality bars are unchanged — the floor is met by processing MORE opportunities, never by lowering §5 pre-check standards.

> **Cap:** 20 new-content briefs per week (config.json `max_new_content_per_week=20`). Refreshes have a separate 20/week cap — see Task 3. Combined ship target: 20 pages/week live via T9 (Kushal 2026-07-03).

Check `~/Seo-workflow-mindtalk/mindtalk-setup/tracking-db.json` for any entries with `type: "NEW_CONTENT"`
created this week — don't exceed 20 new briefs per week.
```

#### After
```
Take the top **20 highest-priority opportunities this week** (unchanged cap).

**FLOOR (added 2026-07-10, Kushal-directed): create a MINIMUM of 12 briefs per weekly run** unless the filtered queue is genuinely exhausted. Recent runs produced only 5/week while the 20-pages/week live target requires T9 to never starve (runway rule: keep ≥15 unshipped briefs in tracking-db at all times — T16 now monitors this). If you create fewer than 12, the run log MUST state exactly why (e.g., "queue exhausted after filters: only 9 passed"). Quality bars are unchanged — the floor is met by processing MORE opportunities, never by lowering §5 pre-check standards.

**🚫 BRIEF COUNT GATE (mandatory — execute before writing any briefs):**
After applying the priority filters above, count how many candidates you have.
- If count ≥ 12: proceed to Step 3 (pre-checks).
- If count < 12 AND you are in CACHED mode (discovery script fell back to existing JSON): lower the volume threshold in tiers and re-filter from the full opportunities list:
  - Tier 1: lower minimum volume threshold by 100 (e.g. BLOG_ARTICLE ≥500 → ≥400)
  - Tier 2: lower by another 100 (≥300)
  - Tier 3: lower by another 100 (≥200)
  - Stop when you have ≥12 OR the queue is genuinely empty below vol 200.
- If count < 12 after all tiers exhausted: continue with what you have, but the Step 7 summary MUST include: `⚠️ BRIEF FLOOR MISS: [N] of 12 minimum. Queue exhausted at vol > 200.` and this line must also be included in the Slack post (Step 8).
- NEVER write `5/5 quota` or any `N/5` denominator in any log or Slack message. The cap is 20. The floor is 12. Report as `N/20 cap (floor: 12)`.

> **Cap:** 20 new-content briefs per week (config.json `max_new_content_per_week=20`). Refreshes have a separate 20/week cap — see Task 3. Combined ship target: 20 pages/week live via T9 (Kushal 2026-07-03).

Check `~/Seo-workflow-mindtalk/mindtalk-setup/tracking-db.json` for any entries with `type: "NEW_CONTENT"`
created this week — don't exceed 20 new briefs per week.
```

---

### Edit B — Step 7: Replace summary body with explicit output format

#### Before (lines 314–319)
```
### Step 7 — Weekly new content summary

Append to `~/Seo-workflow-mindtalk/mindtalk-setup/logs/new-content-[WEEK-START].txt`:
- Keywords selected this week with their type and search volume
- Running count of new content briefs created this month
- Any keywords reclassified from new content → content refresh
```

#### After
```
### Step 7 — Weekly new content summary

Append to `~/Seo-workflow-mindtalk/mindtalk-setup/logs/new-content-[WEEK-START].txt` using this EXACT header format:

```
## Keywords Selected This Week ([N]/20 cap, floor 12)
[list each keyword with type + search volume]

## Monthly brief count: [M] briefs created in [MONTH]

## Reclassified (new → refresh): [list any, or "none"]

## Floor status: [✅ MET ([N] ≥ 12) | ⚠️ FLOOR MISS ([N] < 12) — reason: [reason]]
```

Rules:
- Always use `[N]/20 cap, floor 12` — never `[N]/5`, `[N]/10`, or just `[N]/N`
- If floor was missed, the Floor status line is MANDATORY and must match the Slack post (Step 8)
- If operating in cached mode, add a line: `## Discovery mode: CACHED (live script unavailable — fell back to new-content-opportunities.json)`
```

## Rationale

Two independent gaps let T5 exit with 5 briefs on 2026-07-13 without any error signal: the floor had no gate (agents only follow explicit branch logic, not prose aspirations) and the output template anchored the agent on the old "5" quota format. Both gaps must close together: the gate enforces the floor before brief creation, and the output template ensures the agent always reports in the correct N/20 format, making future regressions visible in the first log line.

## Risk assessment

Low-medium. The count gate adds a volume-threshold expansion step in cached mode, which will pick up lower-volume keywords. These are still within the existing filter criteria (they pass all type/intent filters, just at lower volume). If Kushal wants to veto low-volume topics, the expansion only kicks in when cached mode is detected — live discovery mode already surfaces 12+ candidates at current thresholds.

## Rollback

The Before blocks for both edits are preserved above. To revert:
- Restore Step 2: remove the BRIEF COUNT GATE block (between the FLOOR note and the Cap note).
- Restore Step 7: replace the new body with the original 3-bullet list.
Rollback snapshot: `brain/proposed-changes/t5-floor-12-output-enforcement-2026-07-19-2030.md` (this file).
