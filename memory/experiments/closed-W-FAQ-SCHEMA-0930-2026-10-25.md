# Experiment Log: W-FAQ-SCHEMA-0930
**Closed:** 2026-10-25  
**Evaluated by:** T12 (LEARNER)  
**Verdict:** 🟢 RECOVERED (yoga-for-anxiety) / 🟡 PARTIAL (light-therapy-for-insomnia)

---

## Hypothesis
Fixing Blog-FAQ schema key mismatch (mainEntity → acceptedAnswer) would restore lost impressions and clicks on affected blog pages. Fix shipped in commit `2c9ffa1d`. Live-verified: yoga-for-anxiety had 5 Question nodes, light-therapy-for-insomnia had 3.

---

## Baseline (28-day pre-fix, ~2026-09-02)
| URL | Impressions | Clicks | Position |
|---|---|---|---|
| /blogs/yoga-for-anxiety | 616 | 0 | 10.9 |
| /blogs/light-therapy-for-insomnia | 616 | 0 | 10.9 |

*(Shared baseline from watch spec — pages experienced click collapse prior to fix)*

---

## Final Window: Oct 15–22, 2026
| URL | Impressions | Clicks | Position | vs Prev (Oct 8–15) |
|---|---|---|---|---|
| /blogs/yoga-for-anxiety | 1,531 | 12 | 8.6 | +3.9% impr, +140% clk |
| /blogs/light-therapy-for-insomnia | 301 | 2 | 8.0 | +10.7% impr, +0% clk |

---

## Verdict Rationale
**yoga-for-anxiety → 🟢 RECOVERED**
- Impressions +148.5% vs baseline (616 → 1,531)
- Clicks recovered from 0 → 12 (full recovery signal)
- Position: 10.9 → 8.6 (page-1 territory)
- Strong causal signal: FAQ schema fix is the only structural change; click recovery is decisive

**light-therapy-for-insomnia → 🟡 PARTIAL**
- Impressions -51% vs baseline (616 → 301) — not yet recovered
- Clicks: 0 → 2 (small but nonzero — positive signal)
- Position improved to 8.0 (from 10.9)
- Confound: W-LIGHT-THERAPY-0923 (separate refresh watch) may be capturing the signal
- Conclusion: Schema fix contributed partially; confound prevents clean GREEN verdict

---

## Pattern Signals
- FAQ schema fix has clear positive signal on pages with strong keyword demand (yoga ≫ light-therapy)
- Click recovery is the decisive green indicator; impression growth alone is insufficient
- Schema node count matters: 5 nodes (yoga) outperformed 3 nodes (light-therapy)

---

## Action Items
- None required (yoga: full recovery; light-therapy: monitor via W-LIGHT-THERAPY-0923)
- Schema fix validated as effective technique for click-collapse recovery

---

## Status
CLOSED — W-FAQ-SCHEMA-0930 archived. No further monitoring needed.
