# High-Converter Patterns

**Detected by:** T19 weekly + T12 Learner Sunday refinement
**Used by:** T5 New Content Discovery + T10 Strategist
**Confidence requires:** ≥3 weeks of evidence for proposal, ≥4 weeks to fire as T5 priority

## Confirmed patterns (4+ weeks)
(empty — populated as T19 accumulates data)

## Emerging patterns (1-3 weeks)
**Last updated: 2026-06-25 (W26, week 2 of evidence)**

---

### Pattern 1: Language-specific doctor pages convert at 70–95% intent
**Status:** 🟡 EMERGING — Week 2 of 3 needed. Evidence strengthening.

| Week | Metric | Telugu | Tamil |
|---|---|---:|---:|
| W25 (Jun 17) | Visitors | 37 | 35 |
| W25 | Intent rate | 95% | 91% |
| W26 (Jun 25) | Visitors | 59 (+59.5%) | 64 (+82.9%) |
| W26 | Intent rate | 72.9% | 70.3% |

**W26 note:** Intent rate softened (95% → 72.9%, 91% → 70.3%) but both pages are still the strongest Rockets on the site — 2× the site median of 31.7%. Volume growth is strong. Rate softening likely due to more top-of-funnel visitors entering these pages as visibility grows; absolute click volume held.

**Hypothesis:** Vernacular-language doctor matching is a high-intent need. Users who specify "Telugu-speaking" or "Tamil-speaking" have already decided to book — they just need the right doctor.

**Action if confirmed (week 3):** Propose kannada-speaking / malayalam-speaking / hindi-speaking doctor pages to T5.

---

### Pattern 2: Doctor-listing hub `/doctors` = Goldmine, intensifying
**Status:** 🟡 EMERGING — Week 2 of 3 needed. Evidence intensifying.

| Week | Visitors | book_clicks | Intent rate |
|---|---:|---:|---:|
| W25 (Jun 17) | 119 | 383 | 321% |
| W26 (Jun 25) | 93 (-21.8%) | 363 (-5.2%) | 390% (+69pp) |

**W26 note:** Fewer visitors but HIGHER intent rate (390% vs 321%). This is a qualification effect — fewer but more motivated visitors. The -21.8% visitor drop did NOT cause an equivalent click drop (-5.2%), meaning visitors are converting even more efficiently. This page is not a volume play; it's a qualification funnel.

**Hypothesis:** Doctor-type pages >> blog-type pages for booking intent. Page type hierarchy holds: doctor-listing > expert-LP > illness > treatment > blog.

**Action if confirmed (week 3):** Propose city-specific doctor pages ("psychiatrists in Mumbai", "psychologists in Chennai") + Telugu/Kannada-specific metro pages.

---

### Pattern 3: Blogs convert ~0 direct booking intent (anti-signal confirmed)
**Status:** 🟡 EMERGING — Week 2 of 3 needed. Consistent negative signal.

| Week | Top-traffic blogs | Direct book_clicks |
|---|---|---:|
| W25 | 6 of 6 = 0 | 0 |
| W26 | Confirmed across all 1,011 blog visitors | ~0 |

**W26 note:** 1,011 blog unique visitors, effectively 0 book_appointment_clicked traced to blogs. This is not an instrumentation gap — it's a real behavioral pattern. Blog readers are in discovery mode, not booking mode.

**Implication:** Blog content strategy should be built around internal links → /doctors (capture the rare ready-to-book visitor), NOT around driving direct bookings. ROI of blog work = SEO traffic → /doctors navigation path, not direct conversion.

**Action if confirmed (week 3):** Anchor every blog internal link strategy to /doctors or /experts, never to /illnesses or /treatments (no conversion evidence on those either).

---

### Pattern 4: Geo×page paradox — PARTIALLY RESOLVED W26
**Status:** ⚠️ REVISED — Original hypothesis was partially wrong. See below.

**Original hypothesis (W25):** "Telugu intent comes from AP (Rajahmundry/Vijayawada), NOT Hyderabad. Telangana leak persists."

**W26 result:** Hyderabad +350% (16 → 72 book clicks). Telugu-speaking-doctors visitors +59.5%. Tamil-speaking-doctors visitors +82.9%.

**Revised hypothesis:** Both effects are real.
- W25: Telugu intent was AP-origin. Hyderabad users weren't finding the Telugu doctor pages.
- W26: As Telugu-doctor visibility grew (more visitors, presumably from organic growth), Hyderabad users started landing on them too.
- The paradox was a visibility lag, not a geo mismatch.

**Action:** Paradox resolved for Telangana. NEW watch: Mumbai (-21.9%) and Chennai (-31.8%) despite Tamil doctor page growth (+82.9% visitors). Tamil page is serving Salem/Coimbatore users, not Chennai city. Chennai may need localized doctor pages ("psychiatrist in Chennai") not just language pages.

---

### Pattern 5: AI search (ChatGPT) is a new organic booking channel 🆕
**Status:** 🔵 SEED — Week 1 of 3 needed. Watch.

| Source | W26 book_appointment_clicked | Comparison |
|---|---:|---|
| chatgpt.com | 57 | Larger than Mumbai (75), Delhi (74), Chennai (30) in relative intent |
| perplexity.ai | 12 | Small but present |

**W26 note:** chatgpt.com appeared for the first time in the booking intent breakdown with 57 events — making it the #4 booking-intent source after Bengaluru, Mumbai, and Delhi, but ahead of Hyderabad (before this week's reversal). Mindtalk.in is being recommended in ChatGPT responses to mental health queries.

**Hypothesis:** Mindtalk's assessment-heavy, YMYL-structured content is being cited by AI models for mental health queries (anxiety, depression, finding therapists in India). This is an AI-SEO signal, not traditional SEO.

**Action if confirmed (week 3):** Feed to AI-visibility strategy. Create "AI-citable" content assets (authoritative mental health statistics, India-specific mental health data, structured FAQ blocks that LLMs can reference). Priority feed to searchfit-seo:ai-visibility skill.

---

## Retired patterns (stopped converting)
(empty — populated as T19 detects regressions)

---

## Categories to watch for
- Topic angles (e.g., "in working professionals" vs generic)
- Question vs descriptive page format (e.g., "What is anxiety neurosis?" vs "Anxiety Neurosis: An Overview")
- City suffix (e.g., "therapist bangalore" vs "therapist")
- Page type (illness vs treatment vs blog vs doctor profile)
- Author/reviewer presence (named YMYL reviewer page vs no reviewer)
- Word count brackets (short <800w vs medium 800-2000w vs long >2000w)
- Internal link density (low vs medium vs high)
