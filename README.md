# E-Commerce Conversion Funnel Optimization

An end-to-end sales funnel analysis built in **Google BigQuery (SQL)** to identify conversion bottlenecks, evaluate marketing channel efficiency, and deliver actionable revenue optimization recommendations for an e-commerce platform.

---

## Overview

This project analyzes **9,300+ user events** across **4,400+ unique visitors** to map the full customer journey from first page view to completed purchase. The goal was to answer three core business questions:

1. **Where are we losing customers in the funnel?**
2. **Which marketing channels actually drive revenue (not just traffic)?**
3. **What should we change to improve conversion and ROI?**

---

## Dataset

| Field | Description |
|-------|-------------|
| `event_id` | Unique event identifier |
| `user_id` | Unique user identifier |
| `event_type` | Funnel stage: `page_view`, `add_to_cart`, `checkout_start`, `payment_info`, `purchase` |
| `event_date` | Timestamp of the event |
| `product_id` | Product identifier (6 products) |
| `amount` | Purchase amount (populated on purchase events) |
| `traffic_source` | Acquisition channel: `organic`, `social`, `paid_ads`, `email` |

- **Total Events:** 9,381
- **Unique Users:** 4,445
- **Date Range:** 60-day window
- **Products Tracked:** 6

---

## Analysis & Methods

### 1. Full Funnel Breakdown

Defined a 5-stage conversion funnel and calculated stage-by-stage drop-off rates:

```
Page View (4,445) → Add to Cart (1,379) → Checkout (981) → Payment (796) → Purchase (734)
```

| Stage Transition | Conversion Rate |
|-----------------|----------------|
| View → Cart | 31% |
| Cart → Checkout | 71% |
| Checkout → Payment | 81% |
| Payment → Purchase | 92% |
| **Overall (View → Purchase)** | **17%** |

**Key Insight:** The biggest drop-off occurs at View → Cart (31%), meaning ~69% of visitors leave without engaging. Once users add to cart, the checkout-to-purchase flow is strong (81–92%), indicating the payment UX is working well.

### 2. Funnel by Traffic Source

Segmented the funnel by acquisition channel to compare volume vs. efficiency:

| Channel | Views | Carts | Purchases | Cart Rate | Purchase Rate | Cart → Purchase |
|---------|-------|-------|-----------|-----------|---------------|-----------------|
| Organic | 1,815 | 592 | 309 | 33% | 17% | 52% |
| Paid Ads | 856 | 316 | 179 | 37% | 21% | 57% |
| Email | 465 | 296 | 160 | 64% | 34% | 54% |
| Social | 1,309 | 175 | 86 | 13% | 7% | 49% |

**Key Insight:** Email has the highest purchase conversion rate (34%) and a remarkably high cart rate (64%), despite being the smallest traffic source. Social media drives ~29% of all traffic but converts at only 7% — these are likely "window shoppers." Paid ads perform solidly at 21% purchase conversion, suggesting that spend is reasonably well-targeted. The mismatch between social's volume and conversion efficiency has direct budget implications.

### 3. Time-to-Conversion Analysis

Tracked the average time between funnel stages for users who completed a purchase:

| Metric | Value |
|--------|-------|
| Converted Users | 734 |
| Avg View → Cart | 11.23 min |
| Avg Cart → Purchase | 13.41 min |
| **Avg Total Journey** | **24.63 min** |

**Key Insight:** The purchase journey is relatively fast (~24 min), suggesting users who convert tend to have high intent. This supports a strategy of capturing intent early (email signups, retargeting pixels) rather than relying on extended nurture campaigns.

### 4. Revenue Funnel Analysis

Connected funnel metrics to financial outcomes:

| Metric | Value |
|--------|-------|
| Total Visitors | 4,445 |
| Total Buyers | 734 |
| Total Orders | 734 |
| Total Revenue | $78,699.60 |
| **Avg Order Value** | **$107.22** |
| Revenue per Buyer | $107.22 |
| Revenue per Visitor | $17.71 |

**Key Insight:** With an AOV of ~$107 and revenue per visitor of ~$18, we can benchmark customer acquisition costs. Any channel spending more than $18 per visitor to acquire traffic is operating at a loss.

---

## Recommendations

### 1. UX & Website Optimization
- **Don't touch the checkout flow.** Checkout → Payment → Purchase rates are 81–92%. The technical payment experience is working — don't risk breaking it.
- **Focus on the View → Cart gap.** 69% of visitors leave without adding anything. Test product page improvements: better imagery, social proof, urgency elements.

### 2. Marketing Channel Strategy
- **Reduce social media ad spend for direct sales.** Social drives volume but not revenue (7% conversion). Shift budget from "Traffic" campaign objectives to "Retargeting" or "Lead Gen" to capture emails instead.
- **Double down on email.** It converts at 36% — the highest of any channel. Implement aggressive email capture (popups, exit intent) for the high-volume social visitors. If we can move them onto the email list, the data shows they're far more likely to buy.

### 3. Financial & Revenue
- **Set a strict CAC limit based on AOV.** With an average order of ~$107, customer acquisition costs above $40–50 via low-converting channels (social) are likely unprofitable given the additional overhead.
- **Revenue per visitor ($17.71) is the key benchmark** for evaluating whether any traffic source is worth its cost.

---

## Tech Stack

- **Google BigQuery** — SQL querying and data warehouse
- **SQL** — CTEs, window functions, conditional aggregation, timestamp arithmetic
- **Dataset** — 9,300+ e-commerce user events across 4 traffic sources and 6 products

---

## Files

| File | Description |
|------|-------------|
| `Data_Analytics_Project1.sql` | All SQL queries (funnel, source segmentation, time analysis, revenue) |
| `user_events.csv` | Raw event-level dataset |
| `README.md` | This file — project summary, findings, and recommendations |

---

## Author

**Cole Filson**
University of California, Santa Cruz — B.S. Technology Information Management & B.A. Economics (2026)
[LinkedIn](https://linkedin.com/in/colefilson) • colenf44@gmail.com
