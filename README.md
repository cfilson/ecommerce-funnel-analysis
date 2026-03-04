# E-Commerce Conversion Funnel Optimization

Sales funnel analysis built in **Google BigQuery (SQL)** to find conversion bottlenecks, compare marketing channel performance, and put together revenue optimization recommendations for an e-commerce platform.

---

## Overview

This project looks at **9,300+ user events** across **4,400+ unique visitors** to trace the full customer journey from first page view to completed purchase. The goal was to answer three questions:

1. **Where are we losing customers in the funnel?**
2. **Which marketing channels actually drive revenue, not just traffic?**
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
Page View (4,445) > Add to Cart (1,379) > Checkout (981) > Payment (796) > Purchase (734)
```

| Stage Transition | Conversion Rate |
|-----------------|----------------|
| View to Cart | 31% |
| Cart to Checkout | 71% |
| Checkout to Payment | 81% |
| Payment to Purchase | 92% |
| **Overall (View to Purchase)** | **17%** |

The biggest drop-off is at View to Cart (31%), so ~69% of visitors leave without engaging. Once users add to cart, the checkout-to-purchase flow is strong (81-92%), which tells us the payment UX is working well.

### 2. Funnel by Traffic Source

Segmented the funnel by acquisition channel to compare volume vs. efficiency:

| Channel | Views | Carts | Purchases | Cart Rate | Purchase Rate | Cart to Purchase |
|---------|-------|-------|-----------|-----------|---------------|------------------|
| Organic | 1,815 | 592 | 309 | 33% | 17% | 52% |
| Paid Ads | 856 | 316 | 179 | 37% | 21% | 57% |
| Email | 465 | 296 | 160 | 64% | 34% | 54% |
| Social | 1,309 | 175 | 86 | 13% | 7% | 49% |

Email has the highest purchase conversion rate (34%) and a cart rate of 64%, despite being the smallest traffic source by volume. Social drives ~29% of all traffic but only converts at 7%, which points to a "window shopping" pattern. Paid ads sit at a solid 21% purchase conversion, suggesting that spend is reasonably well-targeted. The gap between social's traffic volume and its actual conversion rate has real budget implications.

### 3. Time-to-Conversion Analysis

Tracked the average time between funnel stages for users who completed a purchase:

| Metric | Value |
|--------|-------|
| Converted Users | 734 |
| Avg View to Cart | 11.23 min |
| Avg Cart to Purchase | 13.41 min |
| **Avg Total Journey** | **24.63 min** |

The purchase journey is fast (~25 min on average), which suggests that users who convert tend to have high intent from the start. This supports capturing intent early through email signups and retargeting pixels rather than running long nurture campaigns.

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

With an AOV of ~$107 and revenue per visitor of ~$18, we can benchmark customer acquisition costs against these numbers. Any channel spending more than $18 per visitor to acquire traffic is losing money.

---

## Recommendations

### 1. UX & Website Optimization
- **Leave the checkout flow alone.** Checkout to Payment to Purchase rates are 81-92%. The payment experience works, no need to risk breaking it.
- **Focus on the View to Cart gap.** 69% of visitors leave without adding anything. Test product page improvements like better imagery, social proof, and urgency elements.

### 2. Marketing Channel Strategy
- **Pull back social media ad spend for direct sales.** Social drives volume but not revenue (7% conversion). Shift budget from "Traffic" campaign objectives to "Retargeting" or "Lead Gen" to capture emails instead.
- **Invest more in email.** It converts at 34%, the highest of any channel. Build out email capture (popups, exit intent) targeting the high-volume social visitors. If we can get them onto the email list, the data shows they're much more likely to buy.

### 3. Financial & Revenue
- **Set a strict CAC limit based on AOV.** With an average order of ~$107, acquisition costs above $40-50 through low-converting channels like social are likely unprofitable after overhead.
- **Revenue per visitor ($17.71) is the number to watch** when evaluating whether a traffic source is worth what you're paying for it.

---

## Tech Stack

- **Google BigQuery** for SQL querying and data warehouse
- **SQL** using CTEs, conditional aggregation, and timestamp arithmetic
- **Dataset** of 9,300+ e-commerce user events across 4 traffic sources and 6 products

---

## Files

| File | Description |
|------|-------------|
| `Data_Analytics_Project1.sql` | All SQL queries (funnel, source segmentation, time analysis, revenue) |
| `user_events.csv` | Raw event-level dataset |
| `README.md` | Project summary, findings, and recommendations |

---

## Author

**Cole Filson**
University of California, Santa Cruz | B.S. Technology Information Management & B.A. Economics (2026)
[LinkedIn](https://linkedin.com/in/colefilson) | colenf44@gmail.com
