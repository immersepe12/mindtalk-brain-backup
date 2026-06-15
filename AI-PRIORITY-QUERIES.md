# AI Citation Priority Queries

**Used by:** Task 17 Competitive + AI Monitor (Thursday 7 PM IST)
**Tested against:** Perplexity, ChatGPT, Claude, Google AI Overview
**Update via:** Manual edit OR 7-day Meta-Learner proposal

---

## 10 priority queries (current)

### Discovery / commercial intent (high revenue impact if cited)

1. `best mental health platform india`
2. `online therapy bangalore`
3. `psychiatrist near me bangalore`
4. `cbt therapy online india`
5. `anxiety treatment india`

### Branded (signals brand SERP health)

6. `mindtalk cadabams`
7. `cadabams mental health`
8. `cadabams app`

### Condition-led (high informational intent → conversion potential)

9. `depression treatment online india`
10. `ocd specialist bangalore`

---

## Why these 10

Trade-off: cover commercial + branded + condition-led without overwhelming weekly API budget.
- Commercial queries (1-5): proxy for revenue potential
- Branded (6-8): tests "do AI engines know Mindtalk exists for Cadabams?"
- Condition-led (9-10): proxy for content authority

## Expansion path

Once weekly run stabilizes (3-4 weeks of data), Meta-Learner can propose:
- Add 5 more high-volume queries from GSC top impressions
- Add 5 long-tail "low-hanging-fruit" queries Mindtalk already ranks for organically
- Total budget: ~25 queries × 4 engines = 100 citations checked weekly

## Output format

`brain/memory/ai-citations-{YYYY-MM-DD}.md` per run, with table:

| Query | Perplexity | ChatGPT | Claude | Google AI OV |
| {query} | cited / not | cited / not | cited / not | cited / not |

Weekly diff vs previous snapshot → TRAJECTORY.md "AI Overview citation share" row.
