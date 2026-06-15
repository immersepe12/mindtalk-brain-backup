# Mixpanel Event Schema — Mindtalk website (project 4011856)

> Status as of 2026-06-15: **NOT YET DISCOVERED — data access blocked.**
> Task 15 will populate this file once Mixpanel access is enabled.

## Why this is empty
Event discovery requires reading project data. As of the inaugural run, both access paths are blocked:

1. **Direct API** (project-scoped API secret) → HTTP 402, `"Your plan does not allow API calls"`.
   The Mindtalk website project's Mixpanel plan tier does not include API / data-export access.
2. **Mixpanel MCP** (account-authed) → `"MCP access is not enabled for this project"`.
   Per-project/org MCP toggle is off (confirmed on 2 projects, so not Mindtalk-specific).

Full diagnosis + fix steps: `memory/mixpanel-access-blocked.md`

## Events we EXPECT to find (per task15 spec — UNVERIFIED until access works)
- `$pageview` (or custom equivalent) — pageview event
- `cta_clicked` — TrackedLink component, per Mindtalk repo
- App download click: `get_app_clicked` / `app_store_click` / `play_store_click`
- Consult booking click: `book_session_clicked` / `booking_started`
- Lead form submit: `lead_created` / `form_submit`
- Exit intent: `exit_intent_shown`
- Scroll depth: `scroll_50` / `scroll_75`

Once access is enabled, run `Get-Events(project_id=4011856, include_details=true)` (MCP) or
`/api/2.0/events/names` (direct API) and replace the section above with the real, verified list.
