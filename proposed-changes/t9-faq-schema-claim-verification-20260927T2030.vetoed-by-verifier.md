# Proposal: t9-faq-schema-claim-verification

**Proposal-ID:** t9-faq-schema-claim-verification-20260927T2030
**Raised-by:** T13-Meta-Learner
**Issue-category:** Silent failure / unverified claim
**Raised-on:** 2026-09-27
**Apply-on:** 2026-10-04T20:00:00+05:30
**Affects-task:** T9 (auto-ship-new-blogs)
**Priority:** HIGH
**Rollback:** Remove Step 5.5b block from task9-auto-ship-new-blogs.md; revert tracking-db schema to not include `faq_schema_verified` field.

---

## Issue

T20 tagged `BLOG-FAQ-SCHEMA-CLAIM-UNVERIFIED-01` on 2026-09-25. T9 commits and ships blog posts with `faqs:` frontmatter entries and logs commit messages like "added FAQPage schema" — but Step 5.5 only checks HTTP 200 status. There is no assertion that `"@type":"Question"` JSON-LD nodes are actually present in the live HTML after deploy. A template change, a frontmatter key-shape mismatch, or a build error can silently drop FAQPage structured data while T9 declares success. This is a silent unverified claim that inflates structured-data coverage in logs.

**Evidence from BRAIN.md:** `2026-09-25 T20: BLOG-FAQ-SCHEMA-CLAIM-UNVERIFIED-01 — brief asserts FAQPage but no post-deploy assertion exists in T9 Step 5.5. Tagged for T13.`

---

## Proposed Change

**File:** `cowork-tasks/task9-auto-ship-new-blogs.md`

**Action:** Insert Step 5.5b immediately after the existing Step 5.5 conclusion paragraph.

### Before (insertion point — end of Step 5.5):

```
Only URLs in `DEPLOYED_OK` proceed to Step 6 (tracking-db update with status=PUBLISHED). URLs in `DEPLOYED_FAIL` get tracking-db entries with status=AUTHORED_PENDING_VERIFY + a flag for next-run human triage.
```

### After (same text + new Step 5.5b appended):

```
Only URLs in `DEPLOYED_OK` proceed to Step 6 (tracking-db update with status=PUBLISHED). URLs in `DEPLOYED_FAIL` get tracking-db entries with status=AUTHORED_PENDING_VERIFY + a flag for next-run human triage.

**Step 5.5b — FAQPage schema assertion (for briefs with `faqs:` frontmatter):**
For each URL in `DEPLOYED_OK` where the source brief contains `faqs:` with ≥1 entry:
\```bash
for url in "${FAQ_URLS[@]}"; do
  faq_count=$(curl -sL "$url" | grep -c '"@type":"Question"' 2>/dev/null || echo 0)
  if [ "$faq_count" -eq 0 ]; then
    echo "🚨 SCHEMA-CLAIM-UNVERIFIED: $url — brief asserts FAQPage but live page has 0 Question nodes"
  else
    echo "✅ FAQPage: $url — $faq_count Question nodes confirmed live"
  fi
done
\```
If `faq_count = 0` after deploy: post to Slack `🚨 BLOG-FAQ-SCHEMA-CLAIM-UNVERIFIED: {url} — 0 JSON-LD Question nodes on live page. Template may not support the frontmatter key shape used in this brief.` and add `"faq_schema_verified": false` to the tracking-db record. A commit message claiming "FAQPage schema" without this step passing is an unverified claim.
```

---

## Filters

- **Forbidden-path check:** PASS — `cowork-tasks/task9-auto-ship-new-blogs.md` is an allowed path
- **Anti-pattern check:** PASS — no AP conflicts; AP10 ("never trust local repo state as proof of production state") is the motivating principle here, not violated
- **Duplicate check:** PASS — no proposal in applied-changes/ or proposed-changes/ within 30 days targets this insertion point
- **INTENT-PRIORITY.md protection:** PASS — not related to intent classification or Tier gates

## Rollback Path

Delete the Step 5.5b block from `cowork-tasks/task9-auto-ship-new-blogs.md`. Remove `faq_schema_verified` field from any tracking-db records that were written after apply. No other files affected.
