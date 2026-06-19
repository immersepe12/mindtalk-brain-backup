# draft_sprint_prompt: Conversion Reorientation internal-link sprint — 2026-06-19

## What we did
Drafted (DRAFT ONLY — not fired) a sprint prompt that routes contextual internal links from high-traffic discovery blogs (which convert ~0 booking intent) into the real booking engine: `/doctors` (🟢 Goldmine, 321% intent), `/experts/expert-therapists` (62%), `/doctors/telugu-speaking-doctors` (95%), `/doctors/tamil-speaking-doctors` (91%). Saved to `prompts/auto-drafted-sprint-conversion-reorientation-2026-06-19.md`.

Source→target map covers 10 candidate blogs; the sprint mandates picking the **first 5–8 watch-free** sources at fire time. All links are direct same-domain `mindtalk.in` paths (AP2/P3 — no `/login?returnTo=` wrappers, no consult.cadabams.com auth URLs), inserted as in-context body anchors (≤2 per page), with no meta/title/H1/slug/frontmatter or target-page edits.

## Expected outcome
Per BACKLOG #8: routes existing blog authority toward pages that actually book consults. Modest absolute, high conversion-leverage. Primary success signal is **conversion tier movement** (do targets hold/gain intent in the next T19 read) + **source rank stability** (no harm) — NOT a position change from a handful of internal links.

## Watch
None opened by the draft itself. The sprint, IF fired, opens its own 14-day watch (source rank-stability + target intent-signal). Added a `review_sprint_prompt` row to BACKLOG for human review.

## Guardrails baked into the draft
- 🟡 DRAFT ONLY; **hard fire gate = human-confirmed AND on/after 2026-06-23** (after Sprint A/B/C 14d watch reads), so it cannot perturb open watches W7 (dominant-personality), W8 (20-quotes), or the trust-issues algo_watch HELD page — those candidate sources are flagged SKIP-if-still-open.
- AP1 staged: first sample = 5–8 pages only, then STOP + 14-day watch before expanding.
- LIMITED_BASELINE: T19 week 1 of 3 — defer full discovery-blog inventory until ≥3 weeks conversion data (T5/D9 gate).

## Verifier
APPROVE (independent sub-agent, full §1–§11). Reasoning: draft-only, zero page/code touched; AP1 5–8 page human-fired sample + AP2 direct internal links are written into the draft; §8 open-watch collision neutralised by the hard post-06-23 fire gate; serves GOALS conversion priority + P9 (Goldmine +50 / Rocket +30) and moves away from the vanity-metric anti-goal; output PII-clean. Logged to verifier-log.md.

## Notes
Per task spec 4b, the Executor does NOT auto-fire sprints (too-high blast radius). This draft awaits explicit human confirmation via the `review_sprint_prompt` BACKLOG row + 24h Slack preview.
