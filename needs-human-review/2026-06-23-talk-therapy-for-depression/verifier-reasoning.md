# NEEDS_HUMAN: talk-therapy-for-depression

**Date:** 2026-06-23
**Task:** T9 Auto-Ship NEW Blogs (first run)
**Brief:** briefs/NEW-talk-therapy-for-depression-brief.md
**Proposed target:** src/content/blogs/talk-therapy-for-depression.mdx
**Brief suggested target:** src/content/treatments/talk-therapy-for-depression.mdx

---

## Verifier Verdict: NEEDS_HUMAN

### The question Kushal must answer

> Does content of type TREATMENT_BLOG (clinical treatment guidance for a named mental health condition, with therapy modality recommendations and medication comparison) fall within Task 9's auto-ship scope when routed to /blogs/ instead of /treatments/ — or does it require the same human gate as /treatments/ pages per the spirit of AP3?

**If YES it is in scope → APPROVE** (all quality bars met, dr-arun-kumar assigned, build not yet run but schema is clean)
**If NO → route to manual /treatments/ pipeline** (same as exposure-response-therapy-ert NEEDS_HUMAN from 2026-06-16)

---

## Verifier Checklist Results

| # | Check | Result | Notes |
|---|-------|--------|-------|
| 1 | Path safety | ✅ PASS | `/blogs/` path matches T9 allowed pattern |
| 2 | AP3 spirit | ⚠️ FLAG | Content is substantively TREATMENT_BLOG — medication comparison, NICE/APA/Cochrane therapy recommendations, severity thresholds. Spirit of AP3 may apply regardless of /blogs/ path. |
| 3 | Goal alignment | ✅ PASS | Drains brief backlog, week 0/20 cap |
| 4 | Risk cap | ✅ PASS | 0/20 this week |
| 5 | Quality bars | ✅ ALL PASS | reviewer, metaTitle ≤65, metaDesc ≤160, quickAnswer, keyTakeaways, 5 FAQs, 5 internal links, Indian English, no placeholders |
| 6 | Build precheck | ⚠️ UNVERIFIED | Schema looks clean, not yet built |
| 7 | Impact | ✅ PASS | 3-7 clicks/wk plausible from 68 imp/90d pos 11.7 |
| 8 | Recency | ✅ PASS | No prior touch, no prior failure on this URL |
| 9 | Blast radius | ✅ PASS | Single page, depression cluster clear |
| 10 | PII | ✅ PASS | None present |

---

## Context: All 4 NEW briefs are TREATMENT_BLOG type

All 4 unshipped NEW-* briefs generated on 2026-06-22 are TREATMENT_BLOG content with `/treatments/` as the brief-suggested path:
- NEW-emdr-for-ptsd-brief.md → 115 imp/90d — VETOED by Verifier (AP3 spirit, clear violation)
- NEW-biofeedback-therapy-for-anxiety-brief.md → 74 imp/90d — VETOED by Verifier (AP3 spirit, clear violation)
- NEW-talk-therapy-for-depression-brief.md → 68 imp/90d — THIS FILE (NEEDS_HUMAN, quality bars pass)
- NEW-emdr-for-anxiety-brief.md → 55 imp/90d — deferred (over first-run cap of 3)

**Root cause:** The brief generation system is producing TREATMENT_BLOG spokes that belong in `/treatments/`, but T9 only ships to `/blogs/`. This is a structural gap.

---

## Staged content

See `staged.mdx` in this directory — full MDX ready to ship if approved.

**Reviewer assigned:** dr-arun-kumar (Depression/Mood/Geriatric specialty)
**metaTitle:** "Talk Therapy for Depression | Mindtalk" (38 chars ✅)
**metaDescription:** 124 chars ✅
**FAQs:** 5 ✅
**Internal links:** /illnesses/depression, /treatments/cognitive-behavioural-therapy-cbt, /treatments/talk-therapy, /contact, /centers ✅
**Crisis resource:** iCall (9152987821) included ✅
**Indian English:** throughout ✅

---

## Options for Kushal

**Option A — Ship to /blogs/ (approve T9 scope expansion)**
If you consider this blog-style educational content (not a treatment hub), approve it for /blogs/. Run `npm run build` in mindtalk repo and then:
```bash
cp brain/needs-human-review/2026-06-23-talk-therapy-for-depression/staged.mdx src/content/blogs/talk-therapy-for-depression.mdx
git add src/content/blogs/talk-therapy-for-depression.mdx
git commit -m "feat(blog): add talk-therapy-for-depression [auto-ship manual-approve]"
git push
```
Then clarify T9 rules to allow TREATMENT_BLOG content in /blogs/ going forward.

**Option B — Ship to /treatments/ (keep YMYL gate)**
If this page belongs in /treatments/talk-therapy-for-depression, route it through the manual clinical sign-off flow outside T9. The content is ready; it just needs the /treatments/ path and a human merge.

**Option C — Rewrite the brief generation rules**
Instruct the brief generator to only produce blogs that are clearly editorial (not treatment pages). TREATMENT_BLOG briefs should go into a separate human-reviewed queue.
