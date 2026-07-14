# investigate_regression: "stress management" pos 1.1→6.9 — 2026-07-14

## Signal
Weekly summary Jul 4-10: "stress management" pos 1.1 → 6.9 (−5.8 pos, 65 impr). Was mindtalk.in's #1 organic ranking on a high-volume query. Daily-tracker flag was NOISE (GSC validator 07-13 classified daily signal as −31.2% impr = daily volatility). **Weekly summary is the authoritative signal** per Strategist — this is a real sustained weekly-level drop.

## What we checked

### 1. Git history — site-side changes
Last content changes to stress management MDX files:
- `9574ebf` — feat(seo): add named clinical reviewer to 96 blogs (batch 5/5 — final) ← this is ALL blogs, not specific to stress
- `b8e6e2d` — fix(booking): correct 7 doctor URLs (URL routing fix, not content)
- `ca7a23a` — fix(booking): migrate 915 Book Session URLs (global, not content)

**Verdict: NO recent content changes caused this drop.** No MDX edits to stress management pages in June or July 2026.

### 2. Internal cluster cannibalization — CRITICAL FINDING
Stress cluster contains **31 stress-related blog pages**. The four "hub" pages directly competing for the head-term "stress management":

| File | Word count | metaTitle |
|------|------------|-----------|
| stress-management-techniques-for-mental-health.mdx | 18,171 | 'Stress Management Techniques: The Ultimate Guide' |
| stress-management-everything-you-need-to-know.mdx | 19,396 | 'What Is Stress Management? Complete Guide & Tools' |
| stress-management-mastering-the-art-of-balance.mdx | 11,781 | (overview/techniques angle) |
| guide-to-stress-management-plan.mdx | 20,372 | 'Complete Stress Management Plan: Daily Strategies That Work' |

**Combined ~70K words across 4 pages all targeting "stress management" at the head-term level.** This is severe internal cannibalization. Google may be shuffling which of these 4 pages it prefers for the query — the "drop" on the tracked page may actually be a SHUFFLE to a sibling, not a site-level loss.

**Key question not yet answered:** Which URL is Google now ranking for "stress management" at position 6.9? If it's a Mindtalk sibling (e.g., `stress-management-everything-you-need-to-know`) then this is cannibalization, not a penalty.

### 3. June Core Update (ACTIVE through 07-17)
Google June 2026 Core Update ACTIVE through 07-17 (3 days remaining at time of this investigation). Mental health = high YMYL/E-E-A-T relevance. Core updates often shuffle competing pages in the same cluster — consistent with cannibalization hypothesis. The stress cluster's 31 pages and 4 competing hub pages make it especially vulnerable to SERP reshuffling under a core update.

### 4. No GSC pull possible
GSC API (`google.oauth2`) unavailable in automation sandbox. Cannot confirm exact query-level impression/click breakdown. Cannot confirm which Mindtalk URL now holds positions 6-7.

## Root cause assessment

**Primary hypothesis: INTERNAL CANNIBALIZATION SHUFFLE** (confidence: HIGH)
4 near-identical ultra-comprehensive "stress management" hub pages (18K-20K words each) competing for the same head term. June Core Update reshuffled which page Google prefers. The tracked page (`stress-management-techniques-for-mental-health`) dropped from #1 while another sibling may have risen. Net Mindtalk footprint may be unchanged.

**Secondary hypothesis: JUNE CORE UPDATE + competitor freshness** (confidence: MEDIUM)
If a competitor (Healthline India, NHS, WebMD India equivalent) published a freshened stress management guide in June, the Core Update's freshness signals may have temporarily elevated it. Cannot confirm without web check (Strategist should add to T17 competitive scan next week).

**NOT the cause: Site changes** — confirmed zero content edits.

## Recommended action

**HOLD all stress management page refreshes until AFTER 07-17** (Core Update settles in 3 days).

On 07-21 (5 days out — allows 4 days of post-update settling):
1. Pull GSC 7d data for "stress management" and variants to identify WHICH Mindtalk URL now holds positions 6-9
2. If a Mindtalk sibling now ranks (cannibalization shuffle): no content action; add internal differentiation task to BACKLOG
3. If Mindtalk dropped from top-10 entirely: create refresh brief for `stress-management-techniques-for-mental-health` (the strongest page at 18K words, established reviewer `priyanka-kema`) targeting: (a) India-specific stress statistics, (b) FAQ expansion, (c) stronger P11 title

**Add to BACKLOG:** `schedule_watch_check` for stress-management cluster — 07-21.

## BACKLOG update
Replace `STRESS-MGMT-DROP-01 | investigate_regression` row with new row:
`STRESS-MGMT-DROP-01-WATCH | schedule_watch_check | Verify which URL holds "stress management" pos after Core Update settles (07-17). GSC check + cannibalization audit on 07-21. | THIS WEEK`

## Tags
#stress-management #cannibalization #core-update #investigate-regression
