# Proposal: Add GSC OAuth token health check to Task 5 before discovery run

**Proposed:** 2026-10-25T20:30 IST
**Source:** T13 Meta-Learner run 2026-10-25
**Apply on:** 2026-11-01T20:00 IST
**Status:** preview

## Issue detected

Task 5 (new-content-discovery) has a fallback chain for GSC API failures, but **no pre-run token health check**. On 2026-10-19, the GSC OAuth token expired in the cloud sandbox, causing the discovery script to time out silently, trigger the stale-cache fallback, and produce a run log with no upfront warning about token expiry.

**Evidence from `logs/new-content-2026-10-19.txt`:**
```
new-content-discovery.py: FAILED (timed out — GSC OAuth token likely expired in cloud sandbox; retried once with alternate PYTHONPATH, same result)
[Fallback] Using cached new-content-opportunities.json (7-day-old data)
```

The fallback ran silently: the log says "DISCOVERY STALE — ran on cache" (per spec), but the **root cause** (expired OAuth token) was only surfaced as a parenthetical note inside the timeout error, not as a distinct pre-run gate. This means:
1. T5 spends ~60–90 seconds on a doomed API call before falling back
2. Token expiry is a fixable pre-run condition (re-auth or pickle refresh), but the current flow treats it as a runtime error rather than an upfront gate
3. A stale-cache brief queue means T5 may miss newly trending queries from the past 7 days — compounding the "T5 FLOOR MISS 2026-10-12" event already in BRAIN.md

## Proposed change

**File to edit:** `/Users/agent/Seo-workflow-mindtalk/mindtalk-setup/cowork-tasks/task5-new-content-discovery.md`
**Edit type:** line-edit (insert after the ALWAYS block and before the "This runs both approaches" line)

### Before

```
**⚠ ALWAYS set `PYTHONPATH=.pip-packages` (fix 2026-07-10).** The google-api libraries live in the repo's `.pip-packages/` folder; without PYTHONPATH the script fails with `google.oauth2 unavailable` — this silently froze fresh discovery from ~06-15 to 07-10 while runs fell back to cached data. The GSC token (`gsc-token.pickle`) self-refreshes; no separate credentials file is needed.

**Self-healing fallbacks, in order:**
```

### After

```
**⚠ ALWAYS set `PYTHONPATH=.pip-packages` (fix 2026-07-10).** The google-api libraries live in the repo's `.pip-packages/` folder; without PYTHONPATH the script fails with `google.oauth2 unavailable` — this silently froze fresh discovery from ~06-15 to 07-10 while runs fell back to cached data. The GSC token (`gsc-token.pickle`) self-refreshes; no separate credentials file is needed.

**Pre-run GSC token health check (T13 fix 2026-10-25):**
Before invoking the discovery script, validate the OAuth token is alive:

```bash
cd ~/Seo-workflow-mindtalk/mindtalk-setup
PYTHONPATH=.pip-packages python3 -c "
import pickle, time, sys
try:
    creds = pickle.load(open('gsc-token.pickle','rb'))
    if hasattr(creds, 'expiry') and creds.expiry and creds.expiry.timestamp() < time.time() + 300:
        if hasattr(creds, 'refresh_token') and creds.refresh_token:
            print('TOKEN_REFRESH_NEEDED — token expires soon, attempting refresh')
        else:
            print('TOKEN_EXPIRED_NO_REFRESH — manual re-auth required')
            sys.exit(2)
    else:
        print('TOKEN_OK')
except Exception as e:
    print(f'TOKEN_CHECK_FAILED: {e}')
    sys.exit(1)
" 2>&1
```

- If `TOKEN_OK` → proceed to discovery.
- If `TOKEN_REFRESH_NEEDED` → the script's own self-refresh will handle it; proceed, but log `GSC_TOKEN_REFRESH_IN_PROGRESS` at the top of the run log.
- If `TOKEN_EXPIRED_NO_REFRESH` or `TOKEN_CHECK_FAILED` → **do NOT start discovery**. Log `DISCOVERY_BLOCKED_GSC_OAUTH` at the top of the run log. Post to Slack `#seo-workflow-mindtalk`:
  ```
  🚨 T5 DISCOVERY BLOCKED — GSC OAuth token invalid
  Error: [paste exit message]
  Action: manual re-auth needed (run gsc-auth.py or equivalent on local machine with browser access)
  This week's discovery run is SKIPPED. Using last cache if < 21 days old.
  ```
  Then fall through to the stale-cache fallback as usual, but with this explicit pre-gate log entry.

**Self-healing fallbacks, in order:**
```

## Rationale

The pre-run token check turns a 90-second timeout into a 3-second diagnosis. It also produces a distinct `DISCOVERY_BLOCKED_GSC_OAUTH` status code that can be grepped in logs — making T12's anomaly detection (or a future T13 run) able to distinguish "token expired" from "API down" from "script crash". The check uses only stdlib (`pickle`, `time`) and the existing token file; no new dependencies.

**Why 2026-10-19 stale-cache was a real loss:** The run used 7-day-old data. That week's Tier A candidates included queries that spiked after the cache was written — those new opportunities were invisible to T5 and are now in a BRIEF_CREATED backlog gap.

## Risk assessment

Low. Read-only pickle inspection. Exit codes 1 and 2 are handled by the spec's existing fallback chain. No change to the actual discovery script (`scripts/new-content-discovery.py` is not touched — forbidden path). The health check block adds < 10 lines to the task spec and < 5 seconds to each run.

## Rollback

`cp brain/before-snapshots/task5-new-content-discovery-{TIMESTAMP}.bak cowork-tasks/task5-new-content-discovery.md`
Alternatively, delete the "Pre-run GSC token health check" block manually — it is clearly delimited between the ALWAYS note and the "Self-healing fallbacks" header.

## Veto instructions

To veto: rename this file to `t5-gsc-oauth-token-health-check-20261025T2030.vetoed.md` and add a `## Veto reason` section.
To approve early: rename to `t5-gsc-oauth-token-health-check-20261025T2030.approved.md`.
