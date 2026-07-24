# VERIFIER — Independent Pre-Flight Safety Check

**Invoked by:** Auto-Ship (T9), Executor (T11), Strategist (T10 Step 10 apply-pass).
**Returns:** APPROVE / VETO / NEEDS_HUMAN with reasoning.
**Not a scheduled task** — runs inline as a sub-agent / pre-flight function before any execution.

---

## Why this exists

Every action-taking task self-polices against ANTI-PATTERNS, but that's the executor checking itself. A real verifier is **independent** — it reasons fresh about the proposed action without the executor's biases or context.

The Verifier catches:
- Actions that look safe individually but violate a recent principle the executor forgot
- Actions that match a stale ANTI-PATTERN the executor missed
- Actions that contradict the current GOALS hierarchy
- Actions targeting files in a 14-day safety pause
- Actions with malformed inputs (e.g., MDX that won't compile)
- Actions whose stated impact doesn't match recent base-rates

Think of it like code review — independent reasoning by a fresh agent catches mistakes the author can't see.

---

## How it's invoked

**By Auto-Ship (T9), before each `git commit`:**
```
verifier_result = verify_action({
  type: "ship_NEW_blog",
  target: "/blogs/{slug}",
  mdx_content: "<full MDX>",
  brief_path: "briefs/NEW-{slug}-brief.md",
  reviewer: "<assigned>",
  expected_impact: "X clicks/wk after indexation"
})
```

**By Executor (T11), before each action:**
```
verifier_result = verify_action({
  type: "ship_REFRESH_brief" | "draft_sprint_prompt" | "investigate_regression" | "schedule_watch_check",
  target: "...",
  proposed_change: "...",
  rationale: "..."
})
```

**By Strategist (T10 Step 10), before applying each Meta-Learner proposal:**
```
verifier_result = verify_action({
  type: "apply_meta_proposal",
  proposal_id: "...",
  target_file: "...",
  before: "...",
  after: "...",
  proposal_age_days: 7
})
```

---

## The verification checklist

For every proposed action, run these checks in order. ANY failure → return VETO + reason.

### 1. Path safety
- [ ] Target file matches an allowed pattern (`brain/*.md`, `cowork-tasks/*.md`, `config.json`, `src/content/blogs/*.mdx` for T9, etc.)
- [ ] Target file does NOT match a forbidden pattern (`scripts/*.py`, `src/components/**`, `src/lib/**`, `src/app/**` — production code)
- [ ] If `suicide-safety` is in the target path, immediate VETO unless `ENABLE_SUICIDE_SAFETY=true`

### 2. Anti-pattern re-check (independent pass)
- [ ] Open `brain/ANTI-PATTERNS.md`
- [ ] For each anti-pattern, reason about whether the proposed action matches the SPIRIT of the rule (not just the literal text)
- [ ] Example: if AP4 says "never refresh within 14 days," and action targets a page modified 13 days ago, that's a VIOLATION even though it's "different number"

### 3. Goal alignment
- [ ] Open `brain/GOALS.md` and `brain/TRAJECTORY.md`
- [ ] Does the action close a variance flag, or move the weakest goal axis?
- [ ] If goal_alignment score < 3, return NEEDS_HUMAN with note "low goal alignment — reconsider priorities"

### 4. Risk cap
- [ ] Read `brain/TRAJECTORY.md` current cap usage
- [ ] Would this action push any cap over 100%?
- [ ] Specifically check:
  - NEW blogs this week (max 20)
  - Refreshes this week (max 10)
  - % pages refreshed rolling 30d (max 20%)
  - % pages auto-modified rolling 7d (max 5%)
  - Pages touched in same cluster within 14d (max 3)
- [ ] If yes → VETO

### 5. Quality bars (for content actions)
For `ship_NEW_blog` or `ship_REFRESH_brief`:
- [ ] Reviewer assigned + not empty
- [ ] meta title ≤ 65 chars and ends with `| Mindtalk`
- [ ] meta description ≤ 160 chars
- [ ] Quick Answer block present (look for `<QuickAnswer>` component)
- [ ] Key Takeaways block present
- [ ] FAQ block has ≥ 5 questions
- [ ] ≥ 3 internal links (`href="/illnesses/...|/treatments/...|/blogs/...|/journeys/...|/assessments/...|/worksheets/...|/journaling/...`)
- [ ] Indian English check (sample 3 likely problem words: "behavior"/"behaviour", "organization"/"organisation", "counseling"/"counselling")
- [ ] No "TODO" / "TBD" / "FIXME" / "{placeholder}" left in body
- [ ] **AP3 Option B gate (updated 2026-06-26)** — if target path matches `/illnesses/*`, `/treatments/*`, or topic is suicide-safety:
  - frontmatter.clinical_reviewer_signed_off.reviewer present + non-empty + matches a known reviewer slug
  - frontmatter.clinical_reviewer_signed_off.date present + ISO-format + ≤ 90 days before TODAY
  - frontmatter.clinical_reviewer_signed_off.scope present (typically "full")
  - If ANY of the three missing/stale: VETO with reason `"AP3 (Option B): YMYL content requires clinical_reviewer_signed_off with reviewer + date≤90d + scope"`
  - If all three present and valid: AP3 satisfied — proceed to the rest of Check 5 as normal

### 6. Build precheck
- [ ] If action results in MDX/config change, the verifier should mentally trace whether `npm run build` would succeed:
  - YAML frontmatter parseable
  - All component imports exist (`<QuickAnswer>`, `<KeyTakeaways>`, etc.)
  - No malformed JSON-LD
  - No unbalanced markdown
- [ ] Auto-Ship + Executor still run real `npm run build` — verifier is a pre-flight catch

### 7. Impact reasonability
- [ ] Stated expected_impact should be within 0.5x – 2x of recent base-rates for similar actions
- [ ] E.g., if action says "expects +500 clicks/wk" but no shipped page in last quarter exceeded +200, flag as unrealistic
- [ ] If unrealistic → NEEDS_HUMAN with note "impact estimate diverges from base-rate"

### 8. Recent action context
- [ ] Has any other action touched this target in past 14 days? If yes → VETO ("safety pause violated")
- [ ] Has the same action type been attempted on this target and failed before? If yes → NEEDS_HUMAN ("repeat-attempt on prior failure")
- [ ] Is this action targeting a page currently in WATCH with open verdict? If yes → VETO ("don't perturb open watch")

### 9. Cluster blast radius
- [ ] How many pages in the same content cluster have been modified in the past 7 days?
- [ ] Cluster caps differ by content folder (updated 2026-07-03 per 20-pages/week target):

  | Cluster | 7-day modification cap | Rationale |
  |---|---|---|
  | `/treatments/*` | **7** (was 5) | Strategic growth cluster — Decision 2 confirms /treatments/ + doctor cards = 80% of UTM-attributed payments. Raised 07-03 to support 20/wk aggregate target. |
  | `/illnesses/*` | **5** (was 3) | YMYL cluster; raised 07-03 from 3 given Sprint A findings + AP3 Option B gating. Cannibalization guard remains at Verifier §5 quality bars. |
  | `/blogs/*` | **6** (was 3) | Discovery cluster; raised 07-03 to unblock T9 velocity for the pilot-20 mix + refresh queue. Note: still Verifier §5-gated so quality-bar failures block ship. |
  | `/lps/*`, `/journeys/*`, `/worksheets/*`, `/mindful-minutes/*` | **5** (was 3) | Raised 07-03 to allow Stub-Page Pilot 20 to ship 5/week × 4 weeks per pilot spec. |
  | `/assessments/*` | **3** (added 2026-07-09) | Steady-state ongoing authoring cap after the 2026-07-09 bulk cluster launch (77 pages via runbook). Bulk cluster launches use `runbooks/2026-07-09-assessments-cluster-launch.md`, NOT T9. |
  | **Aggregate** (across all content folders) | 20 | Hard cap 07-03 to align with Kushal's stated 20-pages/week target. Any single T9 run limited to 7 pages (per-run cap; see task9 spec). |

- [ ] If the count exceeds the cluster's cap → VETO ("cluster blast radius exceeded — {N} ships in {cluster} in last 7d, cap is {cap}")
- [ ] Note: emdr-for-anxiety was deferred 2026-06-26 by the old uniform cap of 3 in /treatments/; with the raised cap (5), the same scenario today would auto-ship without needing to wait for the 7-day window to clear.
- [ ] **Bulk cluster launch carve-out (added 2026-07-09):** cluster-wide launches (10+ pages in a single planned event) do NOT go through T9 or this blast radius cap. They follow a runbook. Confirmed once: `runbooks/2026-07-09-assessments-cluster-launch.md`. The cap applies to T9 ongoing steady-state authoring only.

### 10. PII redaction check (NEW)

For any action that outputs to logs, Slack, or files outside `secrets/`:
- [ ] Scan the proposed output for these patterns:
  - Email addresses (`\b[\w._%+-]+@[\w.-]+\.\w+\b`) — VETO if present, **unless** the address is one of Kushal's own attesting emails (allowed: `kushal@cadabams.com`, `kushal@exar.fit`) and the field is admin-attestation metadata (e.g., `clinical_reviewer_signed_off.attested_by`) that does NOT render to public HTML. Verify the rendering claim by grepping `app/`, `components/`, `lib/` for the field name; if it renders publicly, VETO regardless of address. Added 2026-06-29 from 2026-06-26 emdr-for-ptsd ship audit log.
  - Phone numbers (Indian format: `\+?91[-\s]?\d{10}` or 10-digit sequences)
  - Mixpanel `$user_id`, `$device_id`, `distinct_id` raw values — VETO (these are PII-adjacent)
  - Names of patients / consult clients (cross-check against any known patient list)
- [ ] Action that emits raw API responses from Mixpanel: VETO unless the content has been redacted to keep only aggregated metrics

If PII is detected: VETO with reason `"PII detected: <pattern>"` + post Slack `⚠ PII redaction veto on action {id}`.

### 11. Audit log
- [ ] Verifier appends to `brain/memory/verifier-log.md`:
  ```
  {TIMESTAMP} | {action_type} | target: {target} | verdict: APPROVE/VETO/NEEDS_HUMAN | reason: {detail}
  ```

---

## Verdict semantics

| Verdict | What happens |
|---|---|
| **APPROVE** | Executor proceeds with the action |
| **VETO** | Executor skips the action, logs reason, BACKLOG row stays but with `verifier_vetoed_until: {today+7d}` so it won't retry immediately |
| **NEEDS_HUMAN** | Executor saves the proposed action to `brain/needs-human-review/` and posts Slack with full context. Kushal approves or rejects in Slack. |

---

## Verifier's own safety: it must NEVER

- ❌ Read or modify production code itself (it's a reasoner, not an editor)
- ❌ Auto-approve everything to avoid friction
- ❌ Override an ANTI-PATTERN to "save time" (defeats the safety design)
- ❌ Skip checks if action looks similar to a recent approval (each action is independent)
- ❌ Cache verdicts (each invocation reasons fresh)

---

## Verifier as a sub-agent

In Claude Code's dynamic workflow pattern, the Verifier is best implemented as a separate sub-agent invocation:

```python
# Inside Auto-Ship (T9) or Executor (T11):

verifier_response = spawn_agent(
  type: "Verifier",
  context: {
    "BRAIN.md": read_file("brain/BRAIN.md"),
    "GOALS.md": read_file("brain/GOALS.md"),
    "TRAJECTORY.md": read_file("brain/TRAJECTORY.md"),
    "ANTI-PATTERNS.md": read_file("brain/ANTI-PATTERNS.md"),
    "PRINCIPLES.md": read_file("brain/PRINCIPLES.md"),
    "VERIFIER.md": read_file("brain/VERIFIER.md"),
    "verifier-log.md": read_file("brain/memory/verifier-log.md"),
    "proposed_action": {...}
  },
  task: "Run the verification checklist on proposed_action. Return APPROVE/VETO/NEEDS_HUMAN with reasoning."
)
```

The sub-agent has only Read access to brain files + the proposed action JSON. It has NO write access — its only output is a verdict.

---

## Why this is the right safety architecture

In autonomous systems, the failure mode isn't a single bad decision — it's **gradual drift**: small individual approvals that, taken together, change the system's character over time. The Verifier's independent reasoning catches drift because:

1. It sees fresh state every time (no muscle memory from prior approvals)
2. It re-reads PRINCIPLES + ANTI-PATTERNS every time (no stale assumptions)
3. It has no incentive to ship (the executor does; the verifier just checks)
4. It logs every verdict (auditable drift detection)

If the Verifier ever approves >95% of proposed actions, that's a smell — either the upstream is filtering too aggressively, OR the Verifier is rubber-stamping. Learner should flag if approval rate exceeds 95% for 2 consecutive weeks.

---

## Initial verification rate target

- Weeks 1-4: 60-75% approve, 15-25% NEEDS_HUMAN, 5-15% VETO (system calibrating)
- Weeks 5-12: 75-85% approve, 10-15% NEEDS_HUMAN, 5% VETO (steady state)
- Beyond: trending toward 85-90% approve if Strategist + Executor have absorbed the verifier's feedback into their own filters

A 100% approval rate means the Verifier isn't doing its job. A <50% approval rate means the upstream is producing too much garbage and needs fixing.

---

## Disambiguation Notes

### §9 — 7-day window boundary formula (CONFIRMED 2026-07-24)

**Correct formula:** `published_at > window_start` (i.e., `strictly greater than`)

Where `window_start = today - 7 days` (same calendar date, 7 days prior).

**What this means:**
- A page published on day D **exits** the 7-day window ON day D+7 (it is NOT counted on D+7 itself)
- Example: page published 2026-07-17 → exits window on 2026-07-24 → on 07-24, `published_at (07-17) > window_start (07-17)` is FALSE → page is NOT in window → does NOT count toward cap
- Authoritative source: `logs/auto-ship-2026-07-23.txt` — explicitly states "07-17 page rolled off 07-24 → 5/6 (1 slot open)"

**Common error:** Using `>=` instead of `>` causes pages to be counted on their rolloff day, giving 6/6 cap when the correct count is 5/6.

This was the cause of a Verifier VETO override on 2026-07-23 and again on 2026-07-24. If in doubt, read the most recent T9 run log — it states the window count explicitly.
