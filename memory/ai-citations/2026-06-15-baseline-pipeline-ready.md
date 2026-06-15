# AI Citations Baseline — Pipeline Ready

**Date:** 2026-06-15
**Status:** BASELINE_RUN — first real data Thursday 2026-06-18 19:00 IST

---

## Pipeline validation

- Claude-in-Chrome MCP: 2 browsers connected (work laptop + Personal workspace for claude). Either can drive citation queries.
- Priority queries seeded: 10 queries in `brain/AI-PRIORITY-QUERIES.md`
- Engines to test: Perplexity, ChatGPT, Claude, Google AI Overview
- Snapshot folder: `brain/memory/ai-citations/` ✓
- Output format defined: weekly markdown table per `task17-competitive-ai-monitor.md` Step 7

## What Thursday's run will do

For each of the 10 priority queries:
1. Open Perplexity → run query → record whether mindtalk.in cited
2. Open ChatGPT → same (requires Kushal logged in)
3. Open Claude → same (requires Kushal logged in)
4. Open Google → check AI Overview presence + cited sources

40 data points. First snapshot = baseline. Each subsequent week = diff.

## What no inaugural can show

There's nothing to diff against until Thursday completes — the value is week-over-week.

## Flags raised for Thursday

- Auth check: confirm Kushal stays logged in to ChatGPT + Claude on the chosen browser, else those 2 engines skipped
- Rate-limiting risk: 40 queries in rapid succession might hit Perplexity rate caps — script should sleep 5s between
- Google AI Overview presence varies by query — record AI OV absent vs Mindtalk-not-cited separately

## TRAJECTORY KPI row to populate Thursday

```
| AI Overview citation share | TBD | TBD | TBD | TBD | (10 queries × 4 engines) |
```
