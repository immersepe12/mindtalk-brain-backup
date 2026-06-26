# investigate_regression: Alzheimers ↔ Dementia Cannibalization — 2026-06-26

## What we did
Read-only cannibalization diagnostic on `/illnesses/alzheimers` and `/illnesses/dementia`. Analyzed MDX content overlap, cluster-history.json trajectory for both pages, WATCH.md evaluation notes (W1/W2), recovery brief `briefs/recovery-followup-alzheimers-2026-06-23.md`, and git log for last-touched dates.

---

## Cannibalization signal: CONFIRMED — HIGH OVERLAP

### Content overlap audit

**Alzheimers page overlaps into dementia territory:**
- Full section: "Alzheimer's vs Dementia: Key Differences" (comparison table)
- Full section: "How does Alzheimer's Lead to Dementia?" (~100 words)
- Stage names use "Mild Dementia / Moderate Dementia / Severe Dementia" — these appear in both pages
- Same reviewer: dr-arun-kumar (identical E-E-A-T signal to Google for both pages)

**Dementia page overlaps into Alzheimer's territory:**
- "Alzheimer's Dementia" subsection: "The most common type… accounts for 60-80% of cases"
- "The difference between Alzheimer's and Dementia" framing in multiple sections
- "Protein Build-Up in Alzheimer's Disease" section under Causes
- Multiple "Alzheimer's dementia" references: 9+ occurrences in body
- Same reviewer: dr-arun-kumar

**Verdict:** Two YMYL pages, same reviewer, sharing the same semantic territory around "alzheimers vs dementia / alzheimers dementia" queries. Classic low-differentiation duplication profile that May 2026 Core Update demotes.

---

## SERP trajectory: Google chose Dementia as the winner

| Page | Apr 18 impr | May 2-16 PEAK impr | May 24+ | Jun 13 | Direction |
|---|---:|---:|---:|---:|---|
| /illnesses/alzheimers | 10 | 372 (pos 3.5) | 29 | **23** (pos 13.1) | 🔴 WORSE |
| /illnesses/dementia | 57 | 643 (pos 3.3) | 82 | **75** (pos 4.9) | 🟡 PARTIAL recovery |

Both pages spiked in the SAME weeks (May 2–16) — this was a temporary co-ranking event, not a structural win for either. The May 2026 Core Update collapsed both, then chose dementia as the stronger of the two. Google is now routing "alzheimers dementia" shared queries to /illnesses/dementia (pos 4.9) while /illnesses/alzheimers sits at pos 13.1 with only 6 active queries/week.

---

## SERP co-presence analysis

Alzheimers query count collapsed: **257 → 73 → 11 → 6 queries/week** from May. Dementia held: 420 → 159 → 42 → 33. The ratio of alzheimers:dementia query coverage went from 0.6:1 (May 9) to 0.18:1 (Jun 13). Google stripped query coverage from alzheimers while dementia retained its query base — textbook winner/loser cannibalization pattern after a Core Update disambiguation.

---

## Consolidate vs Differentiate decision

### ❌ CONSOLIDATE (301 alzheimers → dementia): NOT RECOMMENDED

Reasons to reject:
1. Alzheimers is a major standalone illness (60-80% of all dementia). It warrants its own indexed page.
2. Alzheimers page contains genuinely distinct content that dementia does NOT cover:
   - 7-stage Reisberg model (GDS staging) — not in dementia page
   - Early-onset / Late-onset / Familial (FAD) / Sporadic type taxonomy — not in dementia page
   - Specific Alzheimer's medications: cholinesterase inhibitors (donepezil, rivastigmine, galantamine) + monoclonal antibodies (aducanumab, lecanemab) — not in dementia page
   - APOE-e4 / APP / PSEN1 / PSEN2 genetic factor specificity — not in dementia page
3. Dementia page is currently recovering (pos 4.9). Folding a worsening page (pos 13.1) into it risks destabilising the recovering page.
4. Distinct search intents exist: "alzheimer's symptoms early" ≠ "dementia vs alzheimer's" ≠ "dementia types"

### ✅ DIFFERENTIATE (recommended)

**What to REMOVE from alzheimers page** (these are cannibalizing the dementia page's stronger signal):
- "Alzheimer's vs Dementia: Key Differences" table — this belongs on the dementia page, not here. Reducing it to a 1-sentence cross-link frees Google to route this query to dementia uncontested.
- "How does Alzheimer's Lead to Dementia?" — condense to 2 sentences with `[→ Learn about all types of dementia](/illnesses/dementia)`.
- Stage names: rename "Mild/Moderate/Severe Dementia" stages to "Stage 4: Mild Cognitive Impairment phase" etc. (use GDS numbers / clinical stage names) to stop the page from competing for "stages of dementia" queries.

**What to ADD to alzheimers page** (to build differentiated depth Google rewards):
1. India-specific data: ARDSI India prevalence stats (4.1M+ cases, set to double by 2036), regional diagnosis gap
2. Expanded 7-stage section with GDS scale details and clinical indicators for caregivers
3. Early-onset Alzheimer's: India-specific resources, age-of-onset statistics, genetic testing context
4. Caregiver pathway in India: who to consult (geriatrician vs neurologist vs psychiatrist), NIMHANS resources, Cadabams Mindtalk specialist team
5. FAQ block: ≥5 Alzheimer's-specific questions (not dementia overlap questions)
6. Clinical sign-off: update `lastReviewed` + `clinical_reviewer_signed_off` for AP3 Option B compliance
7. Strong bidirectional internal link: dementia page → alzheimers page (currently absent from dementia MDX)

---

## Expected outcome post-differentiation

- Alzheimers page re-expands query base from 6 → 15+ queries/week within 21 days (success criterion from recovery brief)
- Dementia page's ranking for shared "alzheimers vs dementia" queries is no longer contested — its pos 4.9 should improve further
- Both pages benefit from clear topical scope signals

---

## Recommended BACKLOG update

Replace #19 with:

```
| 19-outcome | ship_REFRESH_brief | /illnesses/alzheimers — differentiation refresh | Cannibalization confirmed (DIFFERENTIATE verdict, not consolidate). Remove overlap sections (alzheimers-vs-dementia table, dementia-leads-from section), rename stage terminology off "Mild/Moderate/Severe Dementia", ADD: India prevalence data + India caregiver pathway + FAQ block + bidirectional internal link to /illnesses/dementia. Recovery brief at briefs/recovery-followup-alzheimers-2026-06-23.md needs update to reflect differentiation approach. YMYL → clinical sign-off (AP3 Option B). | Cluster query base re-expands 6→15+ queries/wk; dementia page pos improves further | H | L | 07-02 post-algo_watch + clinical sign-off |
```

Add to #18 batch: include alzheimers differentiation refresh in the 07-02 post-algo_watch YMYL batch.

---

## Watch
No new watch added (this is a diagnostic; the action it gates is #18 batch 07-02).

## Notes
- Both pages were last touched in commit `270cf0c` (Sprint A, 2026-06-09) — 17 days ago. AP4 14-day pause is satisfied as of 2026-06-23. No AP4 block on a 07-02 refresh.
- Recovery brief `briefs/recovery-followup-alzheimers-2026-06-23.md` exists but recommends "diagnose first." That diagnosis is now complete. Brief needs amendment to reflect DIFFERENTIATE (not consolidate) approach.
- Do NOT update the recovery brief until algo_watch clears (~07-02) and clinical sign-off is arranged.
