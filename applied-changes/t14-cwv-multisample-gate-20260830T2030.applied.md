# Proposal: T14 Technical Health — require 2-sample median before raising CWV CRITICAL
**Proposed:** 2026-08-30T20:30:00+05:30
**Source:** task13-meta-learner-2026-08-30
**Apply on:** 2026-09-06T20:00:00+05:30
**Status:** preview

## Issue detected

T20 Auto-Remediation (2026-08-23) opened T14-PSI-SINGLE-SAMPLE-01 after observing that the same URL (`/assessments`) returned LCP **10.6s** and **2.3s** ten minutes apart in the same T14 run. T14's spec (Step 3) takes a single PageSpeed Insights API call per URL and immediately flags any result exceeding threshold as CRITICAL. T20's conclusion: "Require ≥3 samples (median) before raising a CWV flag."

T20 also noted it "nearly escalated a false CWV alarm to dev three days before the Core Update" based on a single-sample LCP reading. The BACKLOG entry T14-PSI-SINGLE-SAMPLE-01 was written, but the task14 spec itself was not updated — so T14's next run will repeat the same single-sample behaviour.

Practical cost of single-sample error: T14 has now posted 5 CWV CRITICAL flags to BACKLOG over 8 weeks. At least 2 of those (T20 2026-08-23 confirms the CWV reopen and assessments closure) had single-sample artefacts. Each false CRITICAL creates a dev escalation, a Kushal flag, and potential sprint misallocation.

T20 recommends ≥3 samples; proposing 2 samples (median) as a pragmatic compromise — 3 API calls per URL × 10 URLs = 30 PSI calls at ~3s each is ~90 seconds of wall time, potentially hitting the task runtime limit. 2 calls per URL = 20 calls + 2 min gap = ~2 minutes added to T14 runtime, which is acceptable.

## Proposed change
**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task14-technical-health-monitor.md`
**Edit type:** line-edit

### Before
```
Flag any URL where any metric crossed a threshold. Compare to previous week's report — flag regressions ≥ 10%.
```

### After
```
**Multi-sample rule:** for each URL, run the PSI call **twice** with a 2-minute gap between runs; record both LCP values and use the **lower value (best-of-2)** as the operative reading. Flag CRITICAL only if the best-of-2 LCP exceeds the threshold — this eliminates single-sample spikes from lab variance, CDN cold starts, or temporary server load. If both samples exceed threshold, the flag is genuine. If only one exceeds it, record as `⚠ ELEVATED (single sample)` in the report but do NOT add to BACKLOG as CRITICAL. Promote to CRITICAL only if the elevated reading persists in the following week's T14 run.

Flag any URL where the best-of-2 metric crossed a threshold. Compare to previous week's report — flag regressions ≥ 10%.
```

## Rationale
T14-PSI-SINGLE-SAMPLE-01 is a confirmed recurring issue (T20 2026-08-23). Lab-mode PageSpeed Insights is known to have high variance — a single CDN cold start or transient server load can produce a 4-5× LCP spike. Requiring the best-of-2 reading before flagging CRITICAL eliminates this noise class while keeping the check sensitive to genuine degradation (a truly slow page will show high LCP on both samples). The 2-minute gap between samples avoids cache hitting the same cold-start window.

## Risk assessment
Low-medium. The change delays detection of genuine CWV degradation by one sample (adds ~2 minutes to T14 runtime and defers single-sample issues to the next week). For the Core Update period, this is acceptable — T14 has been generating more noise than signal from single samples. The "promote to CRITICAL if persists next week" clause ensures genuine regressions are still escalated.

## Rollback
Snapshot target file before apply: `brain/before-snapshots/task14-technical-health-20260906T200000.bak`
Revert the two modified lines to the original `Flag any URL where any metric crossed a threshold.` text.
