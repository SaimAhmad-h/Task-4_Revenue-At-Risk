# Revenue at Risk: E-Commerce Order Analytics

Data visualization and analysis of a 1,200-order e-commerce dataset (Jan 2023–Jun 2025), built for a Data Analytics "Data Visualization" training project (Project 4). The project's brief framed the task as an "Optional Mastery Phase" focused on data storytelling: choose the right chart for each question, strip out chartjunk, and deliver boardroom-ready, action-titled insights rather than raw exploratory plots.

This repository applies that brief to a real dataset. Rather than producing generic charts for their own sake, the analysis was driven by one central business question: **how much revenue is the business actually losing, and where should it intervene first?** Everything below follows from that question.

All figures in this document were computed directly from `Dataset_for_Data_Analytics.xlsx` in `Project4_Data_Analysis.ipynb` and were independently re-verified line-by-line before being written here. Every value is exact unless explicitly marked as rounded.

## Table of Contents

- [Background](#background)
- [Dataset Overview](#dataset-overview)
- [Key Findings](#key-findings)
- [Detailed Analysis](#detailed-analysis)
  - [1. Revenue at Risk](#1-revenue-at-risk)
  - [2. Quarterly Revenue Trend](#2-quarterly-revenue-trend)
  - [3. Reliability by Payment Method](#3-reliability-by-payment-method)
  - [4. Reliability by Acquisition Channel](#4-reliability-by-acquisition-channel)
  - [5. Revenue and Reliability by Product](#5-revenue-and-reliability-by-product)
  - [6. Coupon Usage](#6-coupon-usage)
  - [7. Order Composition & Correlations](#7-order-composition--correlations)
  - [8. Customers](#8-customers)
- [Repository Contents](#repository-contents)
- [Dataset Schema](#dataset-schema)
- [Analysis Notebook](#analysis-notebook)
- [Presentation](#presentation)
- [Design Principles Applied](#design-principles-applied)
- [Limitations](#limitations)
- [Tools Used](#tools-used)
- [License](#license)

## Background

The source brief (Project 4: Data Visualization) set three requirements: create charts (bar, line, pie, etc.), choose the appropriate visual for each type of data, and highlight key insights rather than displaying data for its own sake. It also laid out a specific set of design rules that this project follows throughout:

- Match chart type strictly to the business question (bar for category comparison, line for trend)
- Avoid pie charts; never truncate a bar chart's y-axis — start at zero
- Maximize the data-ink ratio; eliminate chartjunk (3D effects, heavy gridlines, decorative backgrounds)
- Use direct labels on bars/lines instead of legends
- Use color only to spotlight the single most important data point, not decoratively
- Write "action titles" that state the conclusion, not just the topic
- Structure the narrative as Situation → Complication → Resolution (SCR)

## Dataset Overview

- **File:** `Dataset_for_Data_Analytics.xlsx`
- **Rows:** 1,200 orders
- **Columns:** 14
- **Date range:** 2023-01-01 to 2025-06-30 (3.5 years)
- **Missing data:** only `CouponCode` has nulls — 309 orders (25.75% of all orders) have no coupon applied; every other column is fully populated
- **Total booked revenue:** $1,264,761.96
- **Average order value:** $1,053.97

## Key Findings

| # | Finding | Exact Figure |
|---|---|---|
| 1 | **Revenue at risk** | 497 of 1,200 orders (41.4167%) are Cancelled or Returned, representing $519,673.91 (41.0887%) of total revenue |
| 2 | **Revenue trend** | Quarterly revenue fell from a peak of $145,590.79 (2024 Q2) to a trough of $103,617.61 (2025 Q1) — a 28.83% decline |
| 3 | **Payment method reliability** | Online has the lowest cancel/return rate (35.27%); Gift Card the highest (44.35%) |
| 4 | **Acquisition channel reliability** | Instagram has the lowest cancel/return rate (37.07%); Email the highest (43.20%) |
| 5 | **Revenue by product** | Ranges from $151,722.39 (Phone) to $195,620.11 (Chair) — a relatively even spread |
| 6 | **Coupon usage** | 891 of 1,200 orders (74.25%) used a coupon; orders with a coupon average $1,057.64 vs. $1,043.37 without — a marginal $14.27 difference |
| 7 | **Order value drivers** | `TotalPrice` correlates most strongly with `UnitPrice` (r = 0.717) and `Quantity` (r = 0.615); `ItemsInCart` is a weaker driver (r = 0.393) |
| 8 | **Repeat customers** | Only 11 of 1,189 unique customers (0.93%) placed more than one order in this dataset |

## Detailed Analysis

### 1. Revenue at Risk

Grouping the five order statuses into two buckets — **Realized** (Delivered, Shipped, Pending) and **At Risk** (Cancelled, Returned) — shows that nearly as much revenue is tied up in orders that never complete as in orders that do.

| Bucket | Orders | Revenue |
|---|---|---|
| Realized | 703 | $745,088.05 |
| At Risk | 497 | $519,673.91 |
| **Total** | **1,200** | **$1,264,761.96** |

Raw order-status breakdown (for reference):

| Status | Order Count | Revenue |
|---|---|---|
| Cancelled | 250 | $276,396.21 |
| Pending | 237 | $256,328.15 |
| Shipped | 235 | $246,159.58 |
| Returned | 247 | $243,277.70 |
| Delivered | 231 | $242,600.32 |

**So what:** Cancellations and returns aren't a rounding error — they represent a revenue stream almost the size of the business's realized sales. Reducing this rate even modestly recovers real revenue without any additional acquisition spend.

### 2. Quarterly Revenue Trend

| Quarter | Revenue |
|---|---|
| 2023 Q1 | $145,412.78 |
| 2023 Q2 | $141,088.74 |
| 2023 Q3 | $126,699.47 |
| 2023 Q4 | $139,442.25 |
| 2024 Q1 | $111,468.55 |
| 2024 Q2 | $145,590.79 |
| 2024 Q3 | $114,750.03 |
| 2024 Q4 | $108,426.50 |
| 2025 Q1 | $103,617.61 |
| 2025 Q2 | $128,265.24 |

Peak: **2024 Q2** ($145,590.79). Trough: **2025 Q1** ($103,617.61). Decline from peak to trough: **28.83%**.

**So what:** Revenue is not simply flat — it shows a real downward drift across the observed period, with a partial recovery in the most recent quarter (2025 Q2).

### 3. Reliability by Payment Method

| Payment Method | Order Count | Cancel/Return Rate |
|---|---|---|
| Online | 258 | 35.27% |
| Debit Card | 232 | 40.95% |
| Cash | 246 | 43.09% |
| Credit Card | 234 | 44.02% |
| Gift Card | 230 | 44.35% |

**So what:** Online payment orders are meaningfully more reliable than every other method, with roughly a 9-point gap versus Gift Card.

### 4. Reliability by Acquisition Channel

| Referral Source | Order Count | Cancel/Return Rate |
|---|---|---|
| Instagram | 259 | 37.07% |
| Google | 241 | 41.91% |
| Referral | 222 | 42.34% |
| Facebook | 228 | 42.98% |
| Email | 250 | 43.20% |

**So what:** Instagram delivers both the highest order volume of any channel and the lowest cancel/return rate — the most efficient channel in the dataset by this measure.

### 5. Revenue and Reliability by Product

| Product | Order Count | Revenue | Cancel/Return Rate |
|---|---|---|---|
| Chair | 178 | $195,620.11 | 41.01% |
| Printer | 181 | $195,612.61 | 40.33% |
| Laptop | 173 | $192,126.56 | 42.77% |
| Tablet | 179 | $186,568.95 | 43.02% |
| Monitor | 163 | $175,651.41 | 43.56% |
| Desk | 170 | $167,459.93 | 39.41% |
| Phone | 156 | $151,722.39 | 39.74% |

**So what:** Unlike payment method and channel, product category shows only a narrow 4.15-point spread in cancel/return rate (39.41%–43.56%) — it is a much weaker lever than the factors above.

### 6. Coupon Usage

| Coupon | Order Count | Avg Order Value | Total Revenue |
|---|---|---|---|
| FREESHIP | 313 | $1,070.41 | $335,036.99 |
| SAVE10 | 286 | $1,065.87 | $304,840.02 |
| WINTER15 | 292 | $1,035.90 | $302,483.54 |
| *(none)* | 309 | $1,043.37 | $322,401.41 |

74.25% of orders (891 of 1,200) used one of three coupon codes. Average order value with a coupon ($1,057.64) is only $14.27 higher than without ($1,043.37) — a negligible difference, suggesting coupon usage is not a meaningful driver of order size in this dataset.

### 7. Order Composition & Correlations

| Metric | Mean | Std Dev | Min | Median | Max |
|---|---|---|---|---|---|
| Quantity | 2.95 | 1.41 | 1 | 3 | 5 |
| Unit Price | $356.41 | $197.18 | $11.39 | $364.21 | $699.93 |
| Items in Cart | 5.49 | 2.28 | 1 | 5 | 10 |

Correlation with `TotalPrice`:

| Variable | Correlation (r) |
|---|---|
| Unit Price | 0.717 |
| Quantity | 0.615 |
| Items in Cart | 0.393 |

**So what:** Order value is driven primarily by what's purchased (unit price) and how many units (quantity), not by how many other items sit in the cart.

### 8. Customers

- **Unique customers:** 1,189
- **Total orders:** 1,200
- **Customers with more than one order:** 11 (0.93% of unique customers)

This dataset is overwhelmingly single-purchase — repeat-purchase behavior is not a meaningful pattern here and was not used to drive any recommendation.

## Repository Contents

```
├── Dataset_for_Data_Analytics.xlsx     # Source dataset (1,200 rows x 14 columns)
├── Project4_Data_Analysis.ipynb        # Full analysis: Python (pandas/matplotlib) + equivalent SQL (SQLite)
├── Project4_Data_Visualization.pptx    # Executive-facing slide deck summarizing the findings
└── README.md
```

## Dataset Schema

`Dataset_for_Data_Analytics.xlsx` contains one row per order across 14 columns:

| Column | Description |
|---|---|
| `OrderID` | Unique order identifier (1,200 unique values) |
| `Date` | Order date (2023-01-01 to 2025-06-30) |
| `CustomerID` | Customer identifier (1,189 unique values across 1,200 orders) |
| `Product` | One of 7 categories: Chair, Desk, Laptop, Monitor, Phone, Printer, Tablet |
| `Quantity` | Units ordered (integer, 1–5) |
| `UnitPrice` | Price per unit in USD ($11.39–$699.93) |
| `ShippingAddress` | Delivery address (655 unique values) |
| `PaymentMethod` | One of 5 methods: Cash, Credit Card, Debit Card, Gift Card, Online |
| `OrderStatus` | One of 5 statuses: Cancelled, Delivered, Pending, Returned, Shipped |
| `TrackingNumber` | Unique shipment tracking code (1,200 unique values) |
| `ItemsInCart` | Total items in the cart at checkout (integer, 1–10) |
| `CouponCode` | One of 3 codes (FREESHIP, SAVE10, WINTER15) or blank (309 orders / 25.75%) |
| `ReferralSource` | One of 5 channels: Email, Facebook, Google, Instagram, Referral |
| `TotalPrice` | Final order value in USD (the target metric for all revenue analysis) |

## Analysis Notebook

`Project4_Data_Analysis.ipynb` covers, in order:

1. Data loading and inspection (shape, dtypes, missing values)
2. Core KPIs (total revenue, order count, average order value, date range)
3. Revenue-at-risk breakdown (Realized vs. Cancelled/Returned)
4. Quarterly revenue trend
5. Cancel/return rate by payment method
6. Cancel/return rate by acquisition channel
7. Revenue by product
8. The same aggregations re-expressed as SQL queries against an in-memory SQLite database
9. Summary table and recommendations






## Tools Used

- **Python:** pandas (data loading, grouping, aggregation), matplotlib (all charts)

- **Jupyter:** notebook execution and inline chart rendering
