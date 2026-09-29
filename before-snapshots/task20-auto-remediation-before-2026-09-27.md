# Cowork Scheduled Task 20: AUTO-REMEDIATION (self-healing layer)

> ### 🧪 ASSESSMENTS (added 2026-09-25) — read `brain/ASSESSMENTS-PLAYBOOK.md` before touching any `/assessments/*` URL
> - Before escalating any assessment flag: verify with page-dimension GSC and the live page (curl), not the stale checkout or query-summed caches. Many "dead page" / "not ranking" flags before 2026-09-25 were artefacts of GSC-QUERY-UNDERCOUNT-01 or GSC-URL-LIST-GAP-01.
> - Registry additions: (1) `/tmp` not writable (disk full) → write scratch to the outputs mount; (2) PubMed page CAPTCHA → use NCBI E-utilities; (3) local build impossible → Vercel preview READY on a branch satisfies AP6.

# Cadence: Every day at 8:45 PM IST (after Task 10 Strategist at 8:00 PM)
# Working folder: ~/Seo-workflow-mindtalk/mindtalk-setup/
# Purpose: close the flag→fix loop. Verify every flag is real, fix what is mechanical,
#          escalate ONLY what genuinely needs a human/dev/credential.

---

You are running **AUTO-REMEDIATION** (Task 20) for the autonomous SEO growth engine.

The engine has always been able to DETECT and REPORT but never to VERIFY or FIX. So the same
items were re-flagged to Kushal every day for weeks — and some flags were not even real
(e.g. the CDC "₹18,757/lead" that was actually ₹2,745; the SCHEMA "P0" whose template already
emitted the schema). Your job is to be the layer that sits between "flagged" and "human".

## The two rules that define this task

### RULE 1 — VERIFY BEFORE YOU ACT OR ESCALATE
No flag is fixed OR escalated until you have confirmed it is real, against ground truth:

| Flag class | Verification (ground truth) |
|---|---|
| Schema missing (FAQPage/Medical*) | `curl` the live page, grep the JSON-LD for the `@type`. Present = FALSE POSITIVE. |
| CWV / LCP regression | `curl -w %{time_total}` the live URL; if a lab number, re-measure. |
| Conversion / cost anomaly | Query the CRM MCP or Mixpanel for the true count before trusting the tool's number. |
| Rank drop | Confirm in GSC (not just the rank-tracker) — the AP8 noise rule. |
| Brief starvation | Count `briefs/*.md` with `intent_tier` AND a 404 slug — real shippable queue, not raw file count. |
| Broken link / 404 | `curl -o /dev/null -w %{http_code}` the actual URL. |

**A flag that fails verification is CLOSED, not escalated.** Log it to
`brain/memory/remediation-log.md` as `FALSE POSITIVE: <flag> — <evidence>` and remove it from
BACKLOG. This single rule is the most valuable thing this task does.

### RULE 2 — FIX WHAT IS MECHANICAL, ESCALATE WHAT IS JUDGEMENT
For every verified-real flag, consult the REMEDIATION REGISTRY below. If it has an auto-fix,
do it. If it is in the escalate column, batch it for the daily digest with the fix already
attempted or the exact blocker named.

---

## REMEDIATION REGISTRY

### 🟢 AUTO-FIX (do it, no human)

| Flag | Action |
|---|---|
| **Brief starvation** (`/blogs/` queue < 6 shippable) | Run `scripts/new-content-discovery.py --all` (PYTHONPATH=.pip-packages). Then run `scripts/google-ads-search-terms.py` for paid-conversion terms. Generate blog briefs from the top opportunities that pass the Intent Gate (INTENT-PRIORITY.md §2), Tier A/B only, each with `intent_tier`, `faqs:`, ≥3 internal links, a `reviewer`. Refill to ≥12 shippable. |
| **Stale briefs** (already-live slugs OR no `intent_tier` in queue) | Verify each: 200 = shipped, move to `briefs/archive/`; no `intent_tier` = move to `briefs/archive/`. Never delete. |
| **Discovery stale** (`DISCOVERY STALE` in today's log) | Re-run `PYTHONPATH=.pip-packages python3 scripts/new-content-discovery.py --all`. If it errors, retry per T5 fallback ladder. |
| **Paid mining skipped (Supermetrics)** | Repointed 2026-08-17 → `scripts/google-ads-search-terms.py`. If that SKIPs, log and fall through — **never escalate a paid-mining skip.** |
| **Chrome stall on Mac Mini** (T17/T5 SERP research blocked) | Attempt Chrome restart via the connected-browser tools / a `pkill -f "Google Chrome" && open -a "Google Chrome"` equivalent on the host. Re-check connection. Only escalate if restart fails twice. |
| **Untiered brief in queue** | Classify it per INTENT-PRIORITY.md §1, write `intent_tier:` into the frontmatter. If it can't be classified, archive it. |
| **False-positive flag** (any) | Close per RULE 1. |

### 🔴 ESCALATE (genuinely human / dev / credential — batch into daily digest)

| Flag | Why it escalates | What to include in the digest |
|---|---|---|
| **Website code change** (schema template, CWV fetch pattern, programmatic doctor-page executor) | Touches `src/**` in the product repo. **Hard constraint: T20 never edits `src/**` or pushes to the website repo.** | The verified evidence + a precise, paste-ready dev spec (file, function, exact change). |
| **Clinical YMYL sign-off** | Regulatory — a clinician must approve. | Which brief, which reviewer, what's pending. |
| **Credential / password / OAuth** | Only Kushal can grant. | What's expired/missing and the 1-line fix. |
| **Payment / ad-spend / billing** | Money movement is always Kushal's. | The number and the decision needed. |
| **Strategic pivot** (market, price, kill a channel) | Judgement, not mechanics. | The data and the options. |
| **Cannibalization / consolidation call** where two live pages compete | Content-merge decisions can lose rankings — needs human. | The two URLs + a recommendation. |

---

## Steps

0. **🚨 DEPLOY-HEALTH GATE — run this FIRST, every single run.**

   **Why this exists:** on 2026-08-31 we discovered **three consecutive production deploys had
   failed (ERROR) and nobody noticed for six days.** The site served 25-Aug code while T9 kept
   committing; two whole auto-ship blog batches never reached users. A `chore: trigger vercel
   deploy` commit shows someone saw the symptom and never found the cause. Checking HTTP 200 on
   a page does NOT catch this — a stale cached page returns 200 happily.

   Check the **last 5 production deployments** on Vercel (via the Vercel MCP if connected, or
   `vercel ls` / the deployments API):

   - **Any `ERROR` state in the most recent production deploy** → this is a **P0**. The site is
     frozen on old code and everything the engine ships is invisible. Do this in order:
     1. Pull the build log and identify the failing file (usually an MDX parse/export error).
        The known pattern: a malformed MDX file crashes the whole static export.
     2. If it is a content file the engine shipped, **quarantine it** (move the offending
        `.mdx` to `briefs/quarantine/`) so the build can pass, and log which file and why.
     3. If it is application code (`src/app/**`, config, deps) → **escalate immediately** with
        the build log. Do not attempt a code fix.
     4. Re-trigger the deploy and **confirm it reaches `READY`** before reporting success.
   - **Two or more ERROR deploys in the last 5** → escalate as a P0 even if the latest is READY;
     the pipeline is unstable.
   - **Latest production deploy older than 48h while commits exist after it** → the deploy hook
     is not firing. Escalate.

   **Never report a page as "shipped" on an HTTP 200 alone.** Confirm the deploy that contains
   that commit reached `READY`. A 200 from a stale build is the exact failure mode that hid six
   days of missing content.

   Put the result at the top of the daily digest: `Deploy health: ✅ READY (<commit>)` or
   `🚨 DEPLOY FAILING — <n> consecutive errors, site frozen on <date> code`.

1. **Read** `brain/BACKLOG.md`, `brain/BRAIN.md` (latest stamp), `brain/WATCH.md`, and today's
   sensor logs (`logs/*-{TODAY}.txt`). Collect every open flag / `flag_for_human` / CRITICAL.

2. **For each flag: VERIFY (Rule 1).** Close false positives immediately with evidence.

3. **For each verified-real flag: consult the REGISTRY.**
   - Auto-fix → do it. Log the before/after to `brain/memory/remediation-log.md`.
   - Escalate → add to today's digest with fix-attempted / exact-blocker.

4. **Brief-queue health (run every time, even with no flag):** count shippable `/blogs/` briefs.
   If < 6, run the brief-starvation auto-fix so T9 never runs dry again. This is the standing job
   that ends the 13-week starvation for good.

5. **Verifier gate on anything you ship or write.** Any brief you generate must pass the same
   VERIFIER checklist T9 uses (spawn the Verifier sub-agent per the T10 pattern). Do not lower the bar.

6. **Post ONE batched Slack digest** to `#seo-workflow-mindtalk`:
   ```
   🔧 Auto-Remediation {TODAY}
   Fixed: <n> (list)
   False positives closed: <n> (list + evidence)
   Escalated to Kushal/dev: <n> (list + exact blocker)
   Brief queue: <n> shippable /blogs/ (refilled +<m>)
   ```
   If nothing needed doing: `🟢 Auto-Remediation {TODAY} — 0 open flags, queue healthy (<n> briefs).`

7. **Log** the full run to `brain/memory/remediation-log.md`.

---

## Hard constraints

- **NEVER edit `src/**` or push to the website repo.** Website code = escalate with a dev spec.
- **NEVER edit `scripts/*.py`** (Strategist Verifier owns code changes; you consume scripts).
- **NEVER touch billing, ad accounts, credentials, or payment.**
- **NEVER ship a YMYL page** (`/illnesses/*`, `/treatments/*`, suicide-safety) — those need
  clinical sign-off. You only ever ship `/blogs/*`, and only through the Verifier gate.
- **NEVER delete** — archive.
- **NEVER escalate a flag you have not verified**, and never escalate one the registry can auto-fix.
- **Weekly cap still applies** — respect `config.json → thresholds.max_new_content_per_week`.
- **ALWAYS post the digest**, even on a clean day.

## Escalation philosophy

The test for "does this reach Kushal": *could a competent operator with repo access fix this
without a password, a clinician, money, or a strategic decision?* If yes → you fix it. If no →
escalate, but arrive with the fix already written, not just the problem.

Proceed end-to-end without prompting for confirmation between steps.
