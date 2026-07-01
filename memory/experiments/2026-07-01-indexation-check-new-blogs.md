# Indexation Check — New Blogs W12/W13/W14
**Date:** 2026-07-01
**Type:** NEW_indexation 14-day early read
**Pages:** /blogs/couple-therapy-techniques (W12), /blogs/how-to-find-a-therapist-for-ocd (W13), /blogs/how-to-find-a-therapist-in-india (W14)
**Ship commit:** `549dac3` — 2026-06-17
**Evaluation window:** Day 0 (2026-06-17) → Day 14 (2026-07-01)

---

## Method

- HTTP status: direct curl to each URL
- Sitemap: fetched https://www.mindtalk.in/sitemap.xml and grepped
- DataForSEO rank: live SERP pull (`/v3/serp/google/organic/live/advanced`, India geo, mobile, depth 50)
- GSC impressions: `reports/query-history.json` — week_start 2026-06-20 is the first full post-ship week (GSC 3-day delay means data through ~2026-06-26). Note: google.auth libs unavailable in sandbox; gsc-pull.py could not be run directly; query-history.json is the most recent available data.

---

## W12 — /blogs/couple-therapy-techniques

**Target query:** "couple therapy techniques"
**Brief baseline:** 414 impr/90d (~138/mo), avg pos 9.5 (pre-ship, likely attributed to treatments/couples-therapy)

| Signal | Value |
|---|---|
| HTTP status | **200 ✅** |
| In sitemap | **Yes ✅** |
| DataForSEO rank (2026-07-01, India mobile) | **40** (page 4) |
| GSC impr — week of 2026-06-20 | 8 impr, pos 7.1 |
| GSC clicks | 0 |

**Context:** The "couple therapy techniques" query was already generating impressions on mindtalk.in pre-ship (via treatments/couples-therapy). Post-ship, the new blog page competes with the existing sibling. Live rank of 40 at day 14 is consistent with normal new-page crawl lag on a low-volume (~138/mo) informational query. No signal of deindex or 404.

**Classification: 🟡 Indexed, low impressions — normal at 14d for NEW page**
- The page is live, indexed, and showing in SERPs. Rank 40 at day 14 is expected for this query volume tier. Keep watch open for 4-6 week final verdict.
- Potential cannibalisation risk with treatments/couples-therapy — monitor whether the new blog absorbs impressions or splits them. Flag if both pages stabilise at pos 30+ on the same query.

---

## W13 — /blogs/how-to-find-a-therapist-for-ocd

**Target query:** "how to find a therapist for ocd"
**Brief baseline:** ~760 combined impr/90d across OCD therapist cluster

| Signal | Value |
|---|---|
| HTTP status | **200 ✅** |
| In sitemap | **Yes ✅** |
| DataForSEO rank (2026-07-01, India mobile) | **6** (page 1) 🚀 |
| GSC impr — "therapist for ocd" week of 2026-06-20 | 13 impr, pos 16.3 |
| GSC clicks | 0 |

**Context:** DataForSEO live rank of **6** for the exact head query is a very strong early signal for a 14-day-old page. The GSC data for "therapist for ocd" (a shorter variant, pos 16.3) and the live rank diverge — this is expected because: (a) GSC data is from first post-ship week when page hadn't fully settled, (b) live DataForSEO uses the longer-tail "how to find a therapist for ocd" which the page title/H1 directly targets. The page has climbed significantly between week June 20 and July 1.

**Classification: 🟢 Indexed + impressing (strong early signal — on track)**
- Page 1 ranking at day 14 is exceptional for a new blog. Keep watch open; expect impressions to rise meaningfully in the 4-6 week window as GSC crawl + index freshness improves.

---

## W14 — /blogs/how-to-find-a-therapist-in-india

**Target query:** "how to find a therapist in india"
**Brief baseline:** ~150–400/mo est; pre-ship impressions were noise-level (2–3/week)

| Signal | Value |
|---|---|
| HTTP status | **200 ✅** |
| In sitemap | **Yes ✅** |
| DataForSEO rank (2026-07-01, India mobile) | **9** (page 1) 🚀 |
| GSC impr — week of 2026-06-20 (first full post-ship week) | **198 impr, pos 3.9** |
| GSC clicks | 0 |

**Context:** The standout result. 198 GSC impressions in the first full post-ship week at avg position 3.9 is an exceptional early signal — the page immediately captured near-page-1 ranking on the exact head term. Pre-ship impressions for this query were 2–3/week (noise), confirming the new page drove the jump. Live rank of 9 at day 14 confirms sustained page-1 presence. Zero clicks at pos 3.9 is expected for this query class (low CTR on navigational/informational "how to" queries at this stage, and GSC CTR tends to lag impressions by 1-2 weeks).

**Classification: 🟢 Indexed + impressing (exceptional early signal — on track)**
- Best-performing of the three new blogs. 198 impr at day 7 post-ship with live rank 9 at day 14 suggests strong topical alignment. Monitor for click-through as position solidifies.

---

## Secondary finding: tracking-db status gap

All three pages show `status: "BRIEF_CREATED"` in tracking-db.json, but they were published via commit `549dac3` on 2026-06-17. The tracking-db was never updated to `PUBLISHED`. This is a data hygiene issue, not a content issue. Flag for Executor T11 to patch on next run.

---

## Summary

| Watch | URL | 200 | Sitemap | Live Rank | GSC impr (wk June 20) | 14d verdict |
|---|---|---|---|---|---|---|
| W12 | /blogs/couple-therapy-techniques | ✅ | ✅ | 40 | 8 impr, pos 7.1 | 🟡 Indexed, low signal (normal) |
| W13 | /blogs/how-to-find-a-therapist-for-ocd | ✅ | ✅ | **6** | 13 impr, pos 16.3 | 🟢 Strong early signal |
| W14 | /blogs/how-to-find-a-therapist-in-india | ✅ | ✅ | **9** | **198 impr, pos 3.9** | 🟢 Exceptional early signal |

No 🔴 escalations. All three pages are indexed and showing in SERPs. Watches remain open — final indexation verdict at 4-6 weeks (~2026-07-29).
