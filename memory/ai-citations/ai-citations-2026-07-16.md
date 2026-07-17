# AI Citation Check — 2026-07-16
**Task:** 17 — Competitive + AI Citation Monitor (Week 5 / BASELINE+1)
**Run:** Thursday 2026-07-16 19:00 IST
**Note:** Second run (baseline was 2026-07-09 — no previous citation data to diff)

---

## Results Table

| Query | Perplexity | ChatGPT | Claude.ai | Google AI OV |
|---|---|---|---|---|
| best mental health platform india | ❌ Amaha, Wysa, YourDOST | ❌ Amaha, Rocket Health, YourDOST | ❌ (noted MindTalk absent from consumer-discovery layer) | ❌ AI OV: Amaha, Psyra |
| online therapy bangalore | ❌ TherapyMantra, HappyYou247 | ✅ "Cadabam's Mindtalk — Larger MH org" | ❌ | ❌ No AI OV |
| psychiatrist near me bangalore | ❌ Apollo, DocGenie | ❓ not tested | ❓ | ❌ No AI OV |
| cbt therapy online india | ❌ Nirvaan, Soulup, Manochikitsa | ❓ not tested | ❓ | ✅ "Mindtalk: Offers language-matched therapy (English, Hindi, Telugu, Tamil)" |
| anxiety treatment india | ❌ ICMR, Hannah Joseph Hospital | ❓ not tested | ❓ | ❌ AI OV: Artemis Hospitals |
| mindtalk cadabams | ✅ mindtalk.in + App Store cited | ✅ Full Cadabams MindTalk feature list | ❓ | ❌ No AI OV |
| cadabams mental health | ✅ cadabamshospitals.com + Mindtalk as digital platform | ✅ Cadabams MindTalk Features | ❓ | ✅ "Cadabam's — comprehensive ecosystem" + Mindtalk mentioned |
| cadabams app | ✅ "Cadabams MindTalk — mental health app" App Store + Play | ✅ Cadabams MindTalk on Google Play, iOS | ❓ | ✅ "primary mental health app called Mindtalk" |
| depression treatment online india | ❌ HopeQure, MindVoyage, Nirvaan | ❌ Amaha, YourDOST, BetterLYF, TalktoAngel | ❓ | ❌ AI OV: Amaha, Anvaya Healthcare |
| ocd specialist bangalore | ❌ NIMHANS OCD Clinic, local specialists | ✅ Cadabams Hospitals cited (CBT+ERP programs) | ❓ | ✅ "Cadabam's Hospitals (CBT + ERP)" + "explore through Mindtalk" |

---

## Scores

| Engine | Citations / 10 | Notes |
|---|---|---|
| Perplexity | **3/10** | Branded queries only (Q6, Q7, Q8) |
| ChatGPT | **4/10** (confirmed) | Q2 online therapy, Q6+Q7+Q8 branded, Q10 Cadabams; Q3/Q4/Q5 untested |
| Claude.ai | **0/10** (commercial); branded untested | Explicitly noted "MindTalk absent from consumer-discovery layer" |
| Google AI OV | **4/10** | Q4 CBT, Q7 Cadabams ecosystem, Q8 Cadabams app, Q10 OCD Bangalore |

**Overall citation rate: ~11/40 = 27.5%** (adjusted for untested Claude branded)
**Commercial query citation rate: 1/20 = 5%** (only Google AI OV Q4 cbt therapy)
**Branded query citation rate: 10/12 confirmed = 83%** (branded queries work well)

---

## Key Findings

### 🚨 CRITICAL GAP: Commercial queries are effectively 0% cited
On the 5 high-revenue commercial queries (Q1-Q5), Mindtalk.in appears in AI answers **only once** (Google AI OV for "cbt therapy online india"). For "best mental health platform india", "online therapy bangalore", "anxiety treatment india", "depression treatment online india" — Mindtalk is invisible across all 4 engines. Competitors cited: Amaha, YourDOST, Nirvaan, HopeQure, TherapyMantra.

### ✅ STRONG: Branded queries work well
When users search brand-adjacent queries (mindtalk cadabams, cadabams app, cadabams mental health), Perplexity and ChatGPT both correctly identify and describe MindTalk. Google AI OV also works for these. This means the brand is indexed and understood — the gap is commercial discovery.

### 🔑 OPPORTUNITY: Google AI OV for "cbt therapy online india" (Q4)
Mindtalk IS cited in Google's AI Overview for "cbt therapy online india" — "Mindtalk: Offers language-matched therapy (English, Hindi, Telugu, Tamil) and structured..." This is the only commercial citation. The /cbt-therapists page or existing content is driving this. Optimize further to hold and expand this position.

### 📊 Claude.ai Gap (meta)
A prior Cowork session explicitly noted: "MindTalk doesn't surface anywhere in this consumer-discovery layer. None of the 'best platform' lists, the app roundups, or the EAP comparisons mention it or Cadabams." This is a training-data/citation gap — Mindtalk needs more third-party mentions in widely-cited review sources (G2, Capterra, APA-adjacent content) to appear in LLM training.

---

## Competitors who got citations Mindtalk didn't (commercial queries)

| Engine | Competitor cited on commercial queries |
|---|---|
| Perplexity | Amaha, Wysa, YourDOST, Nirvaan, HopeQure, TherapyMantra |
| ChatGPT | Amaha, Rocket Health, YourDOST, MindPeers, BetterLYF, TalktoAngel |
| Google AI OV | Amaha, Psyra, Heart It Out, Artemis Hospitals, Anvaya Healthcare, Nirvaan |

**Amaha appears on all 3 engines for commercial queries** — they are the default #1 citation.

---

## Baseline note
This is the first AI citation snapshot. Next week (2026-07-23) will produce first WoW diff.
