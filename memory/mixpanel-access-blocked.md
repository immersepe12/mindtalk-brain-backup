# Mixpanel Access Blocked — Mindtalk website (project 4011856)

**Detected:** 2026-06-15 (Task 15 inaugural run)
**Status:** BLOCKED — no conversion data reachable. Two independent blockers, both admin-side.

## Diagnosis

### Blocker 1 — Direct API is plan-gated
- Endpoint: `https://mixpanel.com/api/2.0/*`
- Auth: project-scoped API Secret (`secrets/mixpanel-mindtalk.txt`) — **VALID** (no 401; request was recognised).
- Result: **HTTP 402**, body: `{"error": "Your plan does not allow API calls. Upgrade at mixpanel.com/pricing"}`
- Reproduced on `events/names` AND `segmentation`; on both US and EU clusters → not endpoint- or region-specific.
- **Meaning:** the project's Mixpanel plan tier does not include the data/query API. This is NOT an auth/secret problem — do not regenerate the secret.

### Blocker 2 — Mixpanel MCP per-project access toggle is OFF
- Account: connected via Kushal's login (owner of org "cadabams group", id 3076134).
- `Get-Projects` → project 4011856 "Mindtalk website" IS visible (workspace 4507622). Account-level access is fine.
- `Get-Events` / `Get-Business-Context` on 4011856 → `"MCP access is not enabled for this project"`.
- Same error on a 2nd project (3986277 "Cadabams consult") → org/project-level setting, not Mindtalk-specific.

## Fixes — either one unblocks Task 15 (both are admin actions, not autonomous)

**Option A — enable MCP access (recommended: likely free; account already connected)**
1. Mixpanel admin → Settings → Integrations → enable MCP / AI access for project 4011856.
2. T15 then pulls data through the MCP. No plan change required.

**Option B — upgrade plan for API access**
1. Upgrade "Mindtalk website" (4011856) to a Mixpanel plan that includes API calls — mixpanel.com/pricing.
2. Unblocks the direct-API secret path used by the current T15 script.

## Until fixed
- Recurring T15 (Wed 10 AM IST) retries weekly; the full pipeline auto-runs the moment either toggle flips.
- TRAJECTORY.md "Conversion KPIs" rows stay TBD (no data). TRAJECTORY left untouched this run — it is Learner-owned (single-writer).
- Autonomous SEO loop continues on SEO-only data, exactly as the task's first-run fallback specifies.
