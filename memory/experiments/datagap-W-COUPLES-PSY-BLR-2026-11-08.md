# Data Gap Log: W-COUPLES-1023 + W-PSY-BLR-1023 (Day-14 Gate)
**Date:** 2026-11-08 (T12 LEARNER run — Day-14 gate was Nov 6)
**Issue:** Both Day-14 watches have pre-action GSC data only (stale files from before PR #23 landed ~Oct 23).

## W-COUPLES-1023
**URL:** /treatments/couples-therapy
**Action:** PR #23 — full content rewrite (couples therapy)
**Launch:** ~Oct 23, 2026
**Day-14 gate:** Nov 6, 2026
**Baseline (28d):** pos 32.7, 1,551 impr, 6 clicks
**GSC file available:** gsc-data/treatments_couples-therapy.json — dated Oct 4 (Sep 24-Oct 1 window)
**Day-14 data:** PRE-ACTION (file is from before PR #23 landed)

**Status: OPEN — DATA_GAP, keep watch active**
Cannot evaluate Day-14. Need fresh GSC pull post-Oct-23 to assess position movement.

## W-PSY-BLR-1023
**URL:** /doctors/psychologists-in-bangalore
**Action:** PR #23 — FAQs, quickAnswer schema, reviewer, meta optimization
**Launch:** ~Oct 23, 2026
**Day-14 gate:** Nov 6, 2026
**Baseline (28d):** pos ~6.2, high impression volume
**GSC file available:** gsc-data/doctors_psychologists-in-bangalore.json — dated Sep 24 (Sep 14-21 window)
**Day-14 data:** PRE-ACTION (file is from Sep 14-21, well before action)

**Status: OPEN — DATA_GAP, keep watch active**
Cannot evaluate Day-14. Need fresh GSC pull post-Oct-23 to assess position movement.

## Root cause
gsc-pull.py requires google.oauth2 Python module — not installed in device_bash environment. Fresh pull blocked.

## Next gate
Both watches: Day-42 → approximately Nov 27-Dec 4, 2026
Recommend: resolve GSC pull infrastructure before next T12 run to avoid repeated DATA_GAP.

## Watch window status: OPEN — awaiting fresh GSC data
