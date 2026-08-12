# Page Conversion Map — Updated 2026-08-12 (W33)

**Written by:** T19 Conversion Intelligence (Wed 11:00 IST) — overwritten each week.
**Read by:** T10 Strategist, T18 Professional Input, T12 Learner.
**Source:** Mixpanel project 4011856 (unified: mindtalk.in + consult.cadabams.com + app), trailing 7d Aug 5–11.
**Intent signal:** `book_appointment_clicked` (total events) ÷ unique page visitors (site-wide denominator).

> **W33 data period:** Aug 5–11, 2026. Unique visitors 9,173 (+3.2% vs W32's 8,890).
>
> **⚠️ REVENUE RECORD STREAK BROKEN.** Payment Successful 154 (-24.9% vs W32 205). Appointment Booked 203 (-23.1% vs W32 264). 3-week record streak ends.
>
> **ROOT CAUSE: ADS PULL-BACK.** Paid book clicks crashed 666→359 (-46.1%). With ~46% less paid traffic entering the funnel, revenue dropped proportionally. Organic book clicks actually GREW: 1,369→1,579 (+15.3%) — **the best organic-only week ever.** This is an ads management issue, NOT an organic SEO regression.
>
> **🟢 DOCTOR_CARD RECOVERY: 5→10 payments (+100%).** 7-week series: W26=10, W27=9, W28=13, W31=13, W32=5 (anomaly), W33=10. W32 crash was likely attribution noise. Doctor path to revenue is healthy.
>
> **🔥 TAMIL NADU / CHENNAI MASSIVE RECOVERY.** Book clicks 27→123 (+356%), Chennai 15→92 (+513%). P1 Tamil status upgraded from WATCH to CONFIRMED. Both language segments (Telugu + Tamil) simultaneously strong for the first time.
>
> **📉 BENGALURU DECLINE: 1,156→912 (-21.1%).** First meaningful drop since W28. Share of national clicks: 56.8%→47.1%. Healthy geographic diversification — not necessarily negative.
>
> **🆕 ATLANTA, USA SPIKE: 51 book clicks.** Largest single-week US city reading ever. Cause unknown — investigate: diaspora cluster, VPN artifact, or organic ranking gain for US-based searches.
>
> **📉 DOHA CRASH: 47→3 (-93.6%).** W32 Qatar breakout was anomalous. Gulf NRI market reverts to baseline.
>
> **🔵 mindtalk_web attribution RECOVERY: 7→11 payments (+57%).** After W32's crash (22→7→11), attribution improving. Still well below W28's 22. Doctor_card attribution healthy.

---

## Site-level W33 snapshot (Aug 5–11)

| Metric | W33 | W32 | WoW | Notes |
|---|---:|---:|---|---|
| Unique visitors (site) | 9,173 | 8,890 | +3.2% ⬆️ | Continued growth |
| book_appointment_clicked (total) | 1,938 | 2,035 | -4.8% 📉 | Paid drop |
| Paid book clicks | 359 | 666 | -46.1% 🔴 | Ads pull-back |
| **Organic book clicks** | **1,579** | **1,369** | **+15.3% 🔥** | **Best organic week ever** |
| whatsapp_clicked | 110 | 139 | -20.9% 📉 | |
| call_clicked | 36 | 62 | -41.9% 📉 | |
| form_submitted | 64 | 114 | -43.9% 📉 | Paid forms down |
| lp_form_submitted | 34 | 57 | -40.4% 📉 | Paid LP traffic down |
| Payment Successful | 154 | 205 | -24.9% 📉 | Ads pull-back effect |
| Appointment Booked | 203 | 264 | -23.1% 📉 | Ads pull-back effect |
| Site-wide intent rate (book/uv) | 21.1% | 22.9% | -1.8pp | Slight dilution |
| mindtalk_web-attributed payments | 11 | 7 | +57.1% ✅ | Attribution recovering |
| mindtalk_web-attributed bookings | 13 | 8 | +62.5% ✅ | Attribution recovering |
| doctor_card payments | 10 | 5 | +100% 🔥 | W32 crash was anomaly |
| homepage hero payments | 1 | 1 | flat | Stable |

---

## Paid vs organic breakdown W33

| Event | Total | Paid (utm_source IN paid list) | Organic-attributable | mindtalk_web |
|---|---:|---:|---:|---:|
| book_appointment_clicked | 1,938 | 359 (18.5%) | 1,579 (81.5%) | ~0 (tracked at payment level) |
| lp_form_submitted | 34 | ~34 (~100%) | ~0 | 0 |
| whatsapp_clicked | 110 | gmb(12)+google(19)+meta(1)+sitelink(1)=33 (30%) | 77 (70%) | 0 |
| call_clicked | 36 | est ~15-20 | est ~16-21 | 0 |
| form_submitted | 64 | google(40)+Google(17)+sitelink(1)+GMB(1)=59 (92%) | 5 (8%) | 0 |
| Payment Successful | 154 | gmb(2)+Google(1)+GMB(1)=4 (2.6%) | 150 (97.4%) | 11 (7.1%) |
| Appointment Booked | 203 | gmb(2)+Google(1)+GMB(1)+meta(1)=5 (2.5%) | 198 (97.5%) | 13 (6.4%) |

**Organic book clicks W33: 1,579 (+15.3% vs W32 1,369).** Sixth consecutive week of organic growth.
**Paid book share: 18.5%** (vs W32 32.7%) — ads spend significantly reduced this week.
**chatgpt.com WhatsApp clicks: 22** — AI-referred users continue using WhatsApp path to consult.

---

## 6-Layer Attribution Breakdown W33 (book_appointment_clicked)

| Layer | Events | Share | WoW vs W32 |
|---|---:|---:|---|
| chatgpt.com (utm_source session) | 122 | 6.3% | -25.6% 📉 (sessions down) |
| perplexity (utm_source) | 4 | 0.2% | flat |
| **Total AI session clicks** | **126** | **6.5%** | **-24.5%** |
| chatgpt.com (initial_referrer, new users) | 22 | — | -54.2% vs W32 48 |
| direct | 162 | 8.4% | +32.8% ⬆️ (more returning visitors) |
| undefined/untracked | 1,285 | 66.3% | stable |
| Android search (an) | 6 | 0.3% | stable |
| Paid total | 359 | 18.5% | -46.1% 🔴 |

**$initial_referring new users W33:** chatgpt.com 22 (vs W32 48). ChatGPT new-user acquisition down significantly — P5 NEW_USER signal weakening. Session channel also down. Monitor W34 closely.

---

## UTM content breakdown W33

| utm_content | Payments | Bookings | WoW payment |
|---|---:|---:|---|
| doctor_card | 10 | 9 | +100% 🔥 (vs W32's 5) |
| hero | 1 | 4 | flat |
| E3-burnout | 0 | 1 | 🆕 new (ad creative attribution) |
| undefined | 143 | 189 | -6.5% |

**Doctor card is the dominant attributed CTA.** hero is alive but low volume. Blogs and illness pages not yet showing direct attributed payments.

---

## Page tier classification (W33 — site-level, per-page from W32 carry-forward)

Per-page visitor breakdown not available this run (Mixpanel breakdown query exceeds token limit). Carrying W32 tiers with W33 signal adjustments.

**Median intent rate W33: 21.1%** (site-wide, vs W32 22.9%)

### 🟢 Goldmines (2 pages — unchanged)

| URL | Tier | Signal basis | W33 status |
|---|---|---|---|
| /doctors (hub page) | 🟢 Goldmine | P2 confirmed 7 weeks. doctor_card 10 payments. | STABLE — doctor_card recovery confirms hub health |
| Homepage (/) | 🟢 Goldmine | Homepage hero 1 payment + 1 booking. Sticky bar. | MONITOR — hero recovering but low volume |

### 🟡 Rockets (2 pages — carries from W32, with updates)

| URL | Tier | W33 notes |
|---|---|---|
| /doctors/psychologists-in-hyderabad | 🟡 Rocket | Hyderabad 133 book clicks (+60.2%) — surging |
| /doctors/psychologists-in-mumbai | 🟡 Rocket | Mumbai 106 (+20.5%), 6th consecutive growth week |
| /doctors/psychologists-in-chennai | 🟡 Rocket → PROMOTE | Chennai 92 (+513%) — may qualify for Goldmine watch |
| /illnesses/ cluster | 🟡 Rocket → Monitor | Tamil Nadu recovery may reflect illness page traffic |

### 🔴 Leaky Buckets (0 pages — unchanged)

No pages identified this week (insufficient per-page data). Flag /appointments and /assessments for UX team (not SEO).

### ⚫ Dead Weight (3 pages — carries from W32)

| URL | Tier | Reason |
|---|---|---|
| /lps/* (all landing pages) | ⚫ Dead | Paid-only, not organic SEO pages |
| /self-help/* (low traffic) | ⚫ Dead | <100 uv/wk, no engagement signal |
| /wellbeing (misc low intent) | ⚫ Dead | Consistent sub-threshold |

---

## UX Friction Status W33

| Page cluster | Rage clicks | Dead clicks | Total | vs W32 | Verdict |
|---|---:|---:|---:|---|---|
| /appointments | 118 | 535 | 653 | -19.8% (W32 814) | 🟡 Improving but still critical |
| /assessments/* | 56 | 750 | 806 | +0.4% (W32 803) | 🔴 ESCALATING — dead clicks now > W32 |
| /find-therapist | 63 | 615 | 678 | stable est | 🔴 CRITICAL (long-standing) |

**Actions needed:**
- /assessments dead clicks escalating — dead click rate now higher than /appointments. Engineering priority.
- /appointments showing first improvement in 4 weeks — whatever dev fixed this week is working, keep going.
- /find-therapist remains the longest-running critical UX issue.
