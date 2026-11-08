# Data Gap Log: W-ASSESS Stale Batch (Day-42 Gate)
**Date:** 2026-11-08 (T12 LEARNER run)
**Issue:** 10 W-ASSESS Phase 1+2 watches have stale GSC data (last refresh: Oct 16 = Day-21 midpoint only). No Day-42 window data available.
**Root cause:** gsc-pull.py scripts require google.oauth2 Python module — not installed in device_bash environment. Fresh GSC pull blocked.

## Watches in DATA_GAP state

| Watch ID | URL | Day-21 Data (Oct 16) | Day-21 Verdict | Day-42 Status |
|---|---|---|---|---|
| W-ASSESS-YBOCS-0925 | /assessments/y-bocs | pos 3.6, CTR 2.36% | 🟢 midpoint | DATA_GAP |
| W-ASSESS-BPD-0925 | /assessments/am-i-borderline-test | pos 6.1, CTR 6.04% | 🟢 midpoint | DATA_GAP |
| W-ASSESS-ACE-0925 | /assessments/ace-test | pos 9.2, CTR 0.84% | mid | DATA_GAP |
| W-ASSESS-DASS-0925 | /assessments/dass-21 | pos 6.9, CTR 2.73% | 🟢 midpoint | DATA_GAP |
| W-ASSESS-CSSRS-0925 | /assessments/c-ssrs | pos 8.9, CTR 0.25% | 🔴 midpoint | DATA_GAP |
| W-ASSESS-EAT26-0925 | /assessments/eat-26 | pos 25.2, CTR 0.70% | 🔴 midpoint | DATA_GAP |
| W-ASSESS-CUBE-0925 | /assessments/cube-test | pos 6.3, CTR 2.32% | page-1 candidate | DATA_GAP |
| W-ASSESS-INDEX-0925 | /assessments/compatibility-test | pos 6.6, CTR 4.08% | mid | DATA_GAP |
| W-ASSESS-NEW8-0925 | /assessments/mental-health-test | 0 clicks, 0 impr | zero-data guard | DATA_GAP |
| W-ASSESS-308-0925 | /assessments/[308 URL] | stale | stale | DATA_GAP |

## Action Required
- Strategist or automated runner should refresh GSC data for these URLs
- Once refreshed, re-run evaluation against Day-42 baselines
- CUBE and YBOCS are strong P12 candidates if position held
- C-SSRS and EAT-26 were struggling at Day-21; need fresh data to confirm or close

## Zero-data guard reminder
Per task spec: if any watch has 0 impressions in GSC file, cross-check before writing 🔴/⚫. NEW8 had 0/0 at last check — do NOT classify until confirmed.

## Watch window status: OPEN — awaiting fresh GSC data
These watches remain OPEN in WATCH.md. No formal close issued this run.
