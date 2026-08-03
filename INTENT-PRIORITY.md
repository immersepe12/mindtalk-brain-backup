# INTENT-PRIORITY — What the engine is allowed to build

**Created:** 2026-07-30 (Kushal-directed: *"fix it at the core and it has to run super high intent keywords and grow majorly there"*)
**Status:** 🔒 CORE POLICY. Binds T3, T5, T9, T10, T11. Protected from Meta-Learner revision (see §7).
**Owner:** Strategist (T10) enforces · Learner (T12) may promote/demote tiers on ≥3 weeks of evidence.

---

## 0. Why this exists

The engine was optimising the **volume axis** (impressions) and had drifted into building content that
generates impressions and **zero bookings**.

Evidence at time of writing (GSC week 2026-07-21→27, Mixpanel W31):

| Query | Impressions | Clicks | What it is |
|---|---:|---:|---|
| `what is a life coach` | **26,449** | **0** | not even mental health — ~9% of all site impressions |
| `dominant` | 1,745 | 0 | dictionary lookup |
| `what is fomo` | 1,552 | 0 | dictionary lookup |
| `what does dominant mean` | 765 | 0 | dictionary lookup |
| `trust issues meaning in hindi` | 914 | 0 | dictionary lookup |

Meanwhile the queries that actually produce patients sit **below the click threshold**:

| Query | Impressions | Clicks | Position |
|---|---:|---:|---:|
| `therapist near me` | 1,230 | 9 | 11.2 |
| `psychiatrists near me` | 945 | **0** | 8.1 |
| `psychologist near me` | 783 | 13 | 8.9 |
| `psychiatrist near me` | 772 | 3 | 10.5 |

And the conversion engine has confirmed, over **five consecutive weeks**:
- **Pattern 1** — language-specific doctor pages convert at **70–95% intent**
- **Pattern 2** — `/doctors` hub is a high-intent qualification funnel
- **Pattern 3** — **blogs produce 0 direct booking intent** (confirmed anti-signal)
- Doctor card = **13 payments/week, stable 5 weeks** — the most reliable attribution signal in the system

Despite Patterns 1+2 being explicitly unlocked for T5 at *"+30 priority, fire immediately"*, the
2026-07-27 T5 run produced **9 briefs, none of them doctor pages**. The engine knew what converts and
kept building what doesn't.

**Root cause: the target metric was wrong.** Chasing a raw impressions goal makes vocabulary terms the
cheapest way to "win", so the engine rationally built them. Fix the metric, fix the behaviour.

---

## 1. The three tiers

### 🟢 TIER A — BOOKING INTENT · **build aggressively · ≥60% of every brief run**
The user is looking for a person to book. Highest revenue per page in the system.

- `/doctors/*` variants: **language** (kannada, hindi, malayalam, bengali, marathi…), **city**
  (bangalore, hyderabad, mumbai, delhi, pune, chennai, kolkata), **specialty**
  (psychiatrist, clinical psychologist, counsellor, child psychiatrist)
- Query shapes: `{professional} near me`, `{professional} in {city}`, `best {professional} {city}`,
  `{language} speaking {professional}`, `online {professional} india`
- Booking-intent treatment queries: `online therapy india`, `book a psychiatrist`, `therapy cost india`
- **Proven:** 70–95% intent rate · 13 payments/wk sustained 5 weeks

### 🟡 TIER B — CONDITION & TREATMENT · **build selectively · ≤30%**
Someone experiencing a problem, seeking help. Feeds Tier A.

- `/illnesses/*`, `/treatments/*` — anxiety, depression, OCD, trauma, relationship issues, burnout
- Query shapes: `{condition} treatment`, `{condition} therapy`, `how to treat {condition}`,
  `{therapy type} for {condition}`
- **Mandatory:** every Tier B page must internally link to ≥2 Tier A pages (doctor/booking surfaces).
  A Tier B page that doesn't route to a booking surface is a Tier C page wearing a costume.

### 🔴 TIER C — INFORMATIONAL / VOCABULARY · **hard cap 10% · default REJECT**
Definition and curiosity lookups. Generates impressions, ~0 clicks, 0 bookings, and drags site CTR.

- Query shapes: `what is {term}`, `{term} meaning`, `{term} definition`, `{word} vs {word}` where
  neither is a clinical condition, slang/vocabulary terms
- Examples already proven dead: life coach, fomo, dry begging, dominant/dominating,
  trust issues meaning in hindi
- **Permitted ONLY if both hold:**
  (a) an existing page already ranks **top-5** for it, AND
  (b) that page has a **measured** internal-click path to a Tier A surface
  Otherwise: reject and log.

---

## 2. The Intent Gate — run BEFORE any brief is created

Every candidate keyword must pass, in order:

1. **Classify** the primary query into Tier A / B / C using §1. Record the tier in the brief frontmatter
   as `intent_tier: A|B|C`. A brief without `intent_tier` is invalid and must not be shipped.
2. **Tier C → REJECT** unless the §1 exception applies. Log as
   `INTENT GATE REJECT: <query> — Tier C, no top-5 + no Tier A path`.
3. **Zero-click trap check** — if an existing site page already serves this query family with
   **≥1,000 impressions and <0.2% CTR**, REJECT. That family is proven dead; building more of it
   deepens the hole. (This is exactly what happened with life-coach and dry-begging.)
4. **Tier A bonus** — Tier A candidates get **+30 priority** (Patterns 1+2 unlock) and jump the queue
   ahead of any Tier B/C candidate regardless of raw volume.

---

## 3. Brief-run composition (T5, every weekly run)

Cap 20/week, floor 12/week (`config.json → thresholds.max_new_content_per_week`).

| Tier | Share of run | On a 20-brief run |
|---|---|---|
| 🟢 A | **≥60%** | ≥12 briefs |
| 🟡 B | ≤30% | ≤6 briefs |
| 🔴 C | ≤10% | ≤2 briefs (usually 0) |

If Tier A candidates are exhausted before hitting 60%, **do not backfill with Tier C.** Report
`⚠️ TIER A EXHAUSTED: only N found` and run short. A short run of high-intent pages beats a full run of
dictionary pages.

**Standing Tier A backlog** (from HIGH-CONVERTER-PATTERNS, unlocked and unbuilt as of 2026-07-30):
1. `/doctors/kannada-speaking-doctors` — Karnataka is 53% of all intent
2. `/doctors/hindi-speaking-doctors` — Delhi NCT +49.4%, 121 book clicks
3. `/doctors/malayalam-speaking-doctors` — Kerala rising (P8 wk2)
4. City doctor pages: mumbai (+36%), delhi (+49%), kolkata (+200%), pune, chennai
5. Specialty × city combinations for the `near me` cluster stuck at pos 8–11

---

## 4. The metric change (this is the actual core fix)

**Raw weekly impressions is deprecated as a primary target.** It rewarded the exact behaviour that
produced 26,449 impressions and 0 clicks.

| Metric | Status |
|---|---|
| Weekly impressions (raw) | 🟡 **diagnostic only** — still reported, no longer a goal to chase |
| **Weekly Tier A+B clicks** | 🟢 **PRIMARY volume target** |
| **Tier A intent rate** (book_appointment_clicked ÷ visitors) | 🟢 PRIMARY quality target |
| Weekly payments / bookings attributed to organic | 🟢 PRIMARY revenue target |

All weekly reporting (T6, T8, T10, T12) must **split impressions by tier**. An impressions rise driven
by Tier C is reported as a **regression**, not growth.

---

## 5. Refresh prioritisation (T3)

Refresh capacity follows the same order: **Tier A pages first**, then Tier B pages that already rank
5–15 (the position band where a refresh moves clicks), then everything else.

Special case — **the pos 8–11 cliff**: `therapist near me`, `psychologist near me`,
`psychiatrist near me`, `psychiatrists near me` all sit at positions 8.1–11.2 with near-zero clicks.
These are the highest-value refresh targets on the site: the authority is already earned and a few
positions converts directly into bookings. Treat as standing Tier A refresh priority.

---

## 6. Strategist scoring (T10)

`score = (Impact × Confidence × Goal_alignment) / (Effort × Risk)` — unchanged, but:

- `Goal_alignment` is now computed against **§4's primary targets**, not raw impressions.
- Apply an intent multiplier: **Tier A ×1.5 · Tier B ×1.0 · Tier C ×0.3**.
- An action whose only justification is raw impressions on a Tier C family scores **0** — reject.

This is consistent with **P9** (conversion-validated tiers outweigh impression-only signals), which
already existed but was not being enforced at the content-selection step.

---

## 7. Protected status (T13 Meta-Learner)

This policy is **protected**. The Meta-Learner may propose *refinements* (tier boundaries, percentages,
new query shapes) but **must not propose**:
- restoring raw impressions as a primary target
- removing or weakening the Intent Gate (§2)
- lowering the Tier A floor below 50%
- raising the Tier C cap above 10%

Any such proposal must be auto-marked `human-review-only` with the reason
`conflicts with INTENT-PRIORITY.md §7 (protected core policy)`.

Reversal requires explicit human sign-off from Kushal, recorded in `brain/memory/decisions/`.

---

## 8. Review

Learner (T12) reviews this policy monthly against measured outcomes. Promote a tier only on ≥3 weeks of
evidence. If Tier A pages stop converting at ≥50% intent for 3 consecutive weeks, escalate to human —
do not silently rebalance toward Tier C.
