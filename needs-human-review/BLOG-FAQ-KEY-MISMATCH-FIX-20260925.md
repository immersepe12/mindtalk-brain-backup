# NEEDS HUMAN REVIEW — BLOG-FAQ-KEY-MISMATCH-FIX
**Filed by**: T11 Executor  
**Date**: 2026-09-25  
**Priority**: HIGH — 2 pages in open watch windows (W39, W-LIGHT-THERAPY-0923)

## Root Cause (Confirmed)

**Template vs frontmatter key mismatch.**

`src/app/blogs/[slug]/page.tsx` line 239 filters FAQs using:
```js
const validFaqs = blogFaqs.filter(
  (f) => typeof f?.q === "string" && f.q.trim() && typeof f?.a === "string" && f.a.trim()
);
```
Template reads `f.q` / `f.a` — but 4 blog MDX files supply `question:` / `answer:` keys.

Result: `validFaqs` is always empty → 0 FAQ JSON-LD nodes emitted despite frontmatter being populated.

## Affected Pages (4)

| File | Status | FAQs in frontmatter | Watch window |
|------|--------|---------------------|--------------|
| `blogs/yoga-for-anxiety.mdx` | Can fix | 5 FAQs | W39 (open) |
| `blogs/light-therapy-for-insomnia.mdx` | AP4-blocked (shipped 09-23) | 3 FAQs | W-LIGHT-THERAPY-0923 (open) |
| `blogs/what-is-positive-psychology.mdx` | Can fix | Unknown count | None |
| `blogs/abandonment-issues-and-coping-strategies.mdx` | Can fix | Unknown count | None |

92 other blogs correctly use `q:`/`a:` and emit FAQ JSON-LD correctly.

## Fix Options

**Option A (Preferred — template patch, 1-line change):**
In `src/app/blogs/[slug]/page.tsx` line 239, update to accept both key patterns:
```js
const validFaqs = blogFaqs.filter(
  (f) => {
    const q = f?.q ?? f?.question;
    const a = f?.a ?? f?.answer;
    return typeof q === "string" && q.trim() && typeof a === "string" && a.trim();
  }
);
```
Also update lines 280–281 to use `f.q ?? f.question` and `f.a ?? f.answer`.
Pros: Zero MDX edits. Future-proof. Immediate fix for all 4 pages including AP4-blocked.
Cons: Permissive (supports two schemas going forward).

**Option B (Content fix — strict schema enforcement):**
Rename `question:` → `q:` and `answer:` → `a:` in 4 MDX files.
Pros: Enforces single schema.
Cons: Can't touch light-therapy-for-insomnia until AP4 clears (after 2026-10-07). Requires 4 separate commits.

## Impact if Unresolved

- W39 (yoga-for-anxiety) and W-LIGHT-THERAPY-0923 (light-therapy-for-insomnia) watch verdicts cannot be trusted — FAQ JSON-LD has been broken since these pages were published or since the key names diverged.
- AIO defense for these pages is impaired: FAQPage schema is the primary AI direct-answer citation anchor.
- yoga-for-anxiety: high-volume mental health blog, FAQPage absence is a significant ranking/AIO risk.

## Verifier Result

APPROVE — Verifier confirmed this is a correct diagnosis. Escalating to human for fix decision.

## Recommended Action

Kushal or developer: apply Option A (template patch) as the fastest path. This requires a PR to `src/app/blogs/[slug]/page.tsx` — not a T11 content change. After fix, **reset W39 and W-LIGHT-THERAPY-0923 clocks** so observation starts from when FAQ JSON-LD is actually emitting.
