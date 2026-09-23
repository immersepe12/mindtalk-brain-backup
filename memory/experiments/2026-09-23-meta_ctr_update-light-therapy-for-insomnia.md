# meta_ctr_update on /blogs/light-therapy-for-insomnia — 2026-09-23

## What we did
- Changed metaTitle to "Light Therapy for Insomnia: Benefits, Dose & Timing | Mindtalk" (62ch, quoted to handle YAML colon)
- Updated metaDescription to action-keywords approach: "Does light therapy for insomnia work? Learn the recommended dose, best timing, and who benefits most. Guide by Mindtalk's sleep specialists." (140ch)
- Added 3 FAQ entries in frontmatter `faqs:` block
- Commits: 159f81a7 (broken — unquoted YAML colon) → 2ea8fdcd (fix) | Vercel: dpl_3BbWk7NE4WVSBYTJP9kevQLjLTQT (READY)

## Build issue encountered
First push (159f81a7) caused Vercel build ERROR: YAML parse failed at metaTitle because the value contained a colon (":") without quotes. Next.js YAML frontmatter parser treats unquoted colons as mapping delimiters. Fix: wrap value in double quotes. Fixed and re-pushed as 2ea8fdcd.

## ANTI-PATTERN learned
**AP-NEW: Always quote YAML values that contain colons.** When writing metaTitle/title with a colon (e.g. "Topic: Subtitle"), must wrap in double-quotes in frontmatter to avoid YAML parse errors. The T11 Verifier pre-flight should add a char-level YAML colon check.

## Schema note
`faqs:` frontmatter is stored but `/blogs/` template does not emit FAQPage JSON-LD (known SCHEMA-MEDICAL-TYPES-01 gap — dev fix required). FAQs are NOT visible in rendered HTML or structured data for blog pages. Step 8.5 schema check not required for non-YMYL pages but noting for T13 proposal.

## Expected outcome
+10-25 clicks/wk from CTR improvement at pos 10.9 / 616 impr

## Watch
W-LIGHT-THERAPY-0923 → check 2026-10-07
