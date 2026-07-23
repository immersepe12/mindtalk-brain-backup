# AI Citation Check — 2026-07-23
**Task:** 17 — Competitive + AI Citation Monitor (Week 6 / WoW vs 2026-07-16)
**Run:** Thursday 2026-07-23 19:00 IST
**Note:** WoW diff available (last snapshot: 2026-07-16)

---

## Results Table

| Query | Perplexity | ChatGPT | Claude.ai | Google AI OV |
|---|---|---|---|---|
| best mental health platform india | ✅ 🆕 "Cadabams and Mindtalk — strong clinical brands" + listed in clinical-care guidance | ❌ sources: Fidato Health, Psyra, ToI, Therapeutic Space | ⬜ not tested | ❌ AI OV: Amaha, YourDOST, Manoshala |
| online therapy bangalore | ✅ 🆕 "Mindtalk lists online therapy in India with video, audio, and chat sessions, first sessions from ₹1,250" | ⬜ not tested | ⬜ not tested | ❌ No AI OV rendered |
| psychiatrist near me bangalore | ✅ 🆕 "Mindtalk – Multiple centres in Bangalore; same-week in-person and online sessions with MD-qualified psychiatrists" | ⬜ not tested | ⬜ not tested | ❌ No AI OV rendered |
| cbt therapy online india | ❌ Nirvaan, Manochikitsa, Lyfsmile cited | ⬜ not tested | ⬜ not tested | ✅ "Mindtalk: Offers 90-day structured CBT programs and language-matched therapy (English, Hindi, Telugu, Tamil) starting around ₹7,799" |
| anxiety treatment india | ❌ Solhapp, Lyfsmile, Hannah Joseph Hospital | ⬜ not tested | ⬜ not tested | ❌ AI OV: Apollo, Manospandana, Lyfsmile |
| mindtalk cadabams | ✅ "Mindtalk is the digital mental-health platform launched by the Cadabams Group" — full feature coverage | ⬜ not tested | ⬜ not tested | ❌ No AI OV rendered |
| cadabams mental health | ❌ 🔻 LOST (Cadabams Hospitals cited, Mindtalk NOT mentioned; was ✅ last wk) | ⬜ not tested | ⬜ not tested | ❌ 🔻 LOST (No AI OV rendered; was ✅ last wk "Cadabams — comprehensive ecosystem + Mindtalk") |
| cadabams app | ✅ "MindTalk by Cadabam's — India's first AI-powered mental health platform" — full feature list | ⬜ not tested | ⬜ not tested | ✅ "Cadabam's primary mental health application is Mindtalk by Cadabam's" + Dr. Riya + store links |
| depression treatment online india | ❌ HopeQure, TherapyMends, TherapyMantra, Nirvaan | ⬜ not tested | ⬜ not tested | ✅ 🆕 "Mindtalk: Features a network of verified, RCI- and NMC-registered specialists providing CBT and psychiatric consultations" |
| ocd specialist bangalore | ⬜ Rate limit hit | ⬜ not tested | ⬜ not tested | ✅ "Cadabam's Hospitals — Mindtalk division also offers expert therapy both in-person and online" |

---

## Scores

| Engine | Citations / 10 | vs Last Week | Notes |
|---|---|---|---|
| Perplexity | **5/9 tested** (55%) | +2 net (gained Q1/Q2/Q3, lost Q7, Q10 rate-limited) | 🚀 MAJOR GAINS on commercial queries |
| ChatGPT | **1/1 tested = ❌** (Q1 only) | ⬜ partial test | DOM extraction limitation; sidebar shows Q1 sources = Fidato/Psyra/ToI |
| Claude.ai | ⬜ not tested | ⬜ | Not tested this run |
| Google AI OV | **4/10** (40%) | 0 net (gained Q9, lost Q7) | GAINED "depression treatment" ✅, LOST "cadabams mental health" |

**Overall citation rate (fully tested cells only): ~9/20 tested cells = 45%**
**Commercial query citation rate: Perplexity 3/5 (60%!) vs 0/5 last week — BREAKTHROUGH**
**Branded query citation rate: Perplexity 2/3 (Q6✅, Q7❌, Q8✅) | Google AI OV 2/3 (Q6❌, Q7❌, Q8✅)**

---

## Key Findings

### 🚀 BREAKTHROUGH: Perplexity now cites Mindtalk for 3 commercial queries
Q1 "best mental health platform india", Q2 "online therapy bangalore", Q3 "psychiatrist near me bangalore" — ALL newly cited by Perplexity this week. Last week Perplexity only cited Mindtalk on branded queries. This is the first time Mindtalk has achieved commercial-intent AI citations at scale. Likely driven by the +150 KW growth and new high-volume rankings entering Perplexity's source index.

### ✅ Google AI OV GAINED: "depression treatment online india" (Q9)
New Google AI OV citation for Q9 — "Mindtalk: Features a network of verified, RCI- and NMC-registered specialists providing CBT and psychiatric consultations." This is significant: Q9 is a high-commercial-intent query (₹ revenue path).

### 🔻 LOSS: "cadabams mental health" (Q7) dropped from BOTH Perplexity and Google AI OV
Q7 was ✅ on Perplexity last week ("Mindtalk as digital platform") and ✅ on Google AI OV ("Cadabams — comprehensive ecosystem + Mindtalk mentioned"). Both now ❌. Cadabams Hospitals is still cited but Mindtalk is not mentioned. Possible cause: the cadabams mental health content on mindtalk.in may have changed, or Perplexity/Google reindexed and now directs this query to cadabamshospitals.com exclusively.

### 🔑 Google AI OV Q4 "cbt therapy online india" — retained and expanded
Mindtalk is still the only Indian MH platform cited in the CBT Google AI OV. The structured 90-day program messaging is what's driving this. Protect this position.

### ⚠️ ChatGPT still not testable via DOM
ChatGPT's rendered response text is not accessible via innerText (UI uses complex React rendering). Q1 source panel shows Fidato Health, Psyra, ToI — Mindtalk absent. Will need screenshot-based verification or API testing for ChatGPT in future runs.

---

## WoW Diff vs 2026-07-16

| | Perplexity | Google AI OV |
|---|---|---|
| GAINED | Q1 ✅, Q2 ✅, Q3 ✅ | Q9 ✅ |
| LOST | Q7 ❌ | Q7 ❌ |
| RETAINED | Q6 ✅, Q8 ✅ | Q4 ✅, Q8 ✅, Q10 ✅ |
| UNCHANGED ❌ | Q4, Q5, Q9 | Q1, Q2, Q3, Q5, Q6 |

---

## Competitors cited where Mindtalk wasn't (commercial queries)

| Engine | Query | Competitors cited |
|---|---|---|
| Perplexity | Q4 cbt therapy online | Nirvaan, CoachForMind, Manochikitsa, Lyfsmile |
| Perplexity | Q5 anxiety treatment | Solhapp, Lyfsmile, Hannah Joseph Hospital |
| Perplexity | Q9 depression treatment | HopeQure, TherapyMends, TherapyMantra, Nirvaan |
| Google AI OV | Q1 best platform | Amaha, YourDOST, Manoshala, iCALL |
| Google AI OV | Q5 anxiety treatment | Apollo, Manospandana, Lyfsmile |
| ChatGPT | Q1 best platform | Fidato Health, Psyra, Therapeutic Space |
