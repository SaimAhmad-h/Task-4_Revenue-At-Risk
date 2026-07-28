# Revenue at Risk: E-Commerce Order Analytics

Data visualization and analysis of a 1,200-order e-commerce dataset (Jan 2023–Jun 2025), built for a Data Analytics "Data Visualization" training project. The analysis quantifies how much revenue is lost to cancellations and returns, tracks the quarterly revenue trend, and identifies which payment methods and acquisition channels are most reliable.

## Key Findings

| Finding | Detail |
|---|---|
| **Revenue at risk** | 497 of 1,200 orders (41.4%) are Cancelled or Returned, representing $519,674 (41.1%) of the $1,264,762 in total booked revenue |
| **Revenue trend** | Quarterly revenue declined from a peak of $145,591 (2024 Q2) to a trough of $103,618 (2025 Q1) — a ~29% drop |
| **Payment method reliability** | Online payment has the lowest cancel/return rate (35.3%); Gift Card has the highest (44.3%) |
| **Acquisition channel reliability** | Instagram-sourced orders have the lowest cancel/return rate (37.1%); Email-sourced orders have the highest (43.2%) |
| **Revenue by product** | Fairly evenly distributed across the 7 product categories, ranging from $151,722 (Phone) to $195,620 (Chair) |

All figures above are computed directly in `Project4_Data_Analysis.ipynb` and are reproducible by re-running the notebook.

```

## Dataset

`Dataset_for_Data_Analytics.xlsx` contains one row per order with the following columns:

`OrderID, Date, CustomerID, Product, Quantity, UnitPrice, ShippingAddress, PaymentMethod, OrderStatus, TrackingNumber, ItemsInCart, CouponCode, ReferralSource, TotalPrice`

- **Rows:** 1,200
- **Date range:** 2023-01-01 to 2025-06-30
- **Products (7):** Chair, Desk, Laptop, Monitor, Phone, Printer, Tablet
- **Payment methods (5):** Cash, Credit Card, Debit Card, Gift Card, Online
- **Order statuses (5):** Cancelled, Delivered, Pending, Returned, Shipped
- **Acquisition channels (5):** Email, Facebook, Google, Instagram, Referral
- **Missing data:** `CouponCode` is blank for 309 orders (no coupon applied); all other columns are fully populated

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

### Running it locally

```bash
pip install pandas matplotlib openpyxl jupyter
jupyter nbconvert --to notebook --execute --inplace Project4_Data_Analysis.ipynb
```

Update the file path in the first code cell to point to your local copy of the dataset before running.



## Tools Used

- **Python:** pandas, matplotlib
- 
## License

Add a license of your choice (e.g., MIT) if you intend to make this repository public.
