# Proposal: T11 — Add post-ship schema type verification for YMYL illness/treatment refreshes
**Proposed:** 2026-08-16T20:30:00+05:30
**Source:** task13-meta-learner-2026-08-16
**Apply on:** 2026-08-23T20:00:00+05:30
**Status:** preview

## Issue detected

T12 Learner (ran 2026-08-16 at 6 PM IST, 2h before this Meta-Learner run) flagged SCHEMA-MEDICAL-TYPES-01: "illness templates don't emit FAQPage/MedicalWebPage JSON-LD schema." This was diagnosed as the root cause of W36 🔴 STALLED + W37 ⚫ WORSE — both the `depression` and `anxiety` YMYL refreshes shipped 2026-07-31 (W28-YMYL-BATCH-SHIP-01) have stalled at Day-14 check. T12 flag: "3/4 watches 🔴/⚫."

The issue is in `src/` (template code) — PROTECTED from auto-apply. However, the T11 Executor spec (`cowork-tasks/task11-executor.md`) Step 4a `ship_REFRESH_brief` has no post-ship check to DETECT the absence of these schema types before closing the BACKLOG action and opening the watch window. Currently T11 ships the content, marks tracking-db as PUBLISHED, opens a watch window — and the schema gap is only discovered 14 days later via T12 Learner when the watch stalls.

The fix: add a Step 8.5 to T11's `ship_REFRESH_brief` that, after Vercel confirms deployment, curls the live URL and checks for `FAQPage` and `MedicalWebPage` in the rendered HTML. If absent → write a `human-review-only` BACKLOG entry for the dev team before opening the watch window.

## Proposed change
**File to edit:** `cowork-tasks/task11-executor.md`
**Edit type:** sed-replace

### Before
```
9. Update `tracking-db.json`: status → `PUBLISHED`, `last_refresh_date` → today
```

### After
```
8.5. **Schema type verification — YMYL paths only (added 2026-08-23 — SCHEMA-MEDICAL-TYPES-01 fix)**

    For briefs targeting `/illnesses/*` or `/treatments/*` paths only:

    After Vercel confirms deployment (step 8), curl the live URL and check for required JSON-LD schema types:

    ```python
    import subprocess, json, re, datetime, pathlib

    live_url = f"https://mindtalk.in{slug}"  # e.g. /illnesses/depression
    result = subprocess.run(['curl', '-s', '-L', live_url], capture_output=True, text=True, timeout=15)
    html = result.stdout

    has_faq_page = 'FAQPage' in html
    has_medical = 'MedicalWebPage' in html

    missing = []
    if not has_faq_page:
        missing.append('FAQPage')
    if not has_medical:
        missing.append('MedicalWebPage')

    if missing:
        backlog_path = pathlib.Path('brain/BACKLOG.md')
        entry_id = f"SCHEMA-MISSING-{slug.split('/')[-1].upper()[:20]}-{datetime.date.today()}"
        if entry_id not in backlog_path.read_text():
            entry = (
                f"| {entry_id} | human-review-only | {datetime.date.today()} | "
                f"YMYL page {live_url} missing JSON-LD schema types: {', '.join(missing)}. "
                f"Root: illness/treatment MDX template does not emit these types (SCHEMA-MEDICAL-TYPES-01). "
                f"Fix required in src/ — dev task. Affects rank signals within 14 days. | "
                f"T11 ship_REFRESH_brief schema check |\n"
            )
            with open(backlog_path, 'a') as fh:
                fh.write(entry)
            # Post Slack flag
            print(f"SCHEMA-MISSING: {live_url} missing {missing} — BACKLOG {entry_id} written (human-review-only)")
    else:
        print(f"SCHEMA-OK: {live_url} has FAQPage + MedicalWebPage ✓")
    ```

    Log result to `logs/executor-{TODAY}.txt` as `SCHEMA-CHECK: OK` or `SCHEMA-CHECK: MISSING {types}`.

9. Update `tracking-db.json`: status → `PUBLISHED`, `last_refresh_date` → today
```

## Rationale

Without this check, the schema gap is only discoverable at Day-14 when a watch stalls — costing 14 days of indexing signal on the highest-value YMYL pages. The check catches the gap at ship time and creates a `human-review-only` BACKLOG entry immediately, so the dev team can patch the template before the next refresh batch. The fix is in the spec file (allowed), not in `src/` (protected). The BACKLOG entry is marked `human-review-only` to prevent Strategist from auto-applying a src/ fix.

## Risk assessment

Low. The curl is read-only against the live site. The BACKLOG entry is deduped (slug-specific ID). The only failure mode is if curl times out or the page is temporarily unavailable after deploy — mitigated by the 15s timeout; a single timeout is acceptable (the next T11 run can re-check). This does NOT block the ship — it only appends a BACKLOG flag and logs; step 9 tracking-db update always runs.

## Rollback

Before snapshot: `brain/proposed-changes/t11-ymyl-schema-verification-20260816T2030.md` (this file, Before section).
To revert: remove the Step 8.5 block, restoring "9. Update `tracking-db.json`..." as the line immediately following step 8.
