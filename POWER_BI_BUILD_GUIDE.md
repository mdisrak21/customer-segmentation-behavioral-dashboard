# Progree Task 3 — Customer Segmentation & Behavioral Trend Dashboard

## Objective
Prepare customer-level analytics for an interactive Power BI dashboard covering RFM segmentation, cohort trends, and geographic analysis.

## Dataset
Online Retail II workbook with two sheets (2009–2010 and 2010–2011).

## Cleaning and preparation
- Combined both workbook sheets.
- Removed exact duplicate rows.
- Excluded cancellation invoices (`InvoiceNo` starts with `C`).
- Kept positive `Quantity` and positive `UnitPrice`.
- Required valid `InvoiceDate`.
- Required `CustomerID` for customer-level RFM analysis.
- Created `Revenue = Quantity × UnitPrice`.

## RFM
Snapshot date: **2011-12-10**.
- **Recency:** days since the customer's latest purchase.
- **Frequency:** distinct invoice count.
- **Monetary:** total revenue.
- R, F and M scores use quintile scoring.
- Customer segments are generated from the three RFM scores.

## Cohort
- `CohortMonth` = customer's first valid purchase month.
- `CohortIndex` = number of months from the cohort month, starting at 1.
- `RetentionRate` = active customers / original cohort customers.

## Files
- `customer_transactions.csv` — Power BI-ready transaction table.
- `customer_rfm.csv` — one row per customer with RFM metrics and segment.
- `cohort_analysis.csv` — cohort retention table.
- `country_summary.csv` — country-level customer/order/revenue summary.
- `task3_summary.csv` — preparation summary.
- `POWER_BI_BUILD_GUIDE.md` — dashboard layout and DAX.

## Power BI Dashboard

### Page 1 — Customer Overview
**Cards**
- Total Customers
- Total Revenue
- Total Orders
- Average Customer Revenue

**Charts**
- Customer Count by Segment
- Revenue by Segment
- Monthly Revenue Trend

**Slicers**
- Country
- Segment
- InvoiceMonth

### Page 2 — RFM Segmentation
- Segment distribution
- Revenue by segment
- Recency vs Monetary scatter
- Frequency distribution
- Customer detail table

### Page 3 — Cohort Analysis
- Cohort retention matrix
- Retention trend by cohort period
- Cohort size chart

### Page 4 — Geographic Analysis
- Country revenue map
- Revenue by country
- Customers by country
- Country slicer

Set `Country` Data Category to **Country/Region** in Power BI for map geocoding.

## Useful DAX Measures

```DAX
Total Revenue = SUM(customer_transactions[Revenue])

Total Customers = DISTINCTCOUNT(customer_transactions[CustomerID])

Total Orders = DISTINCTCOUNT(customer_transactions[InvoiceNo])

Average Customer Revenue =
DIVIDE([Total Revenue], [Total Customers])

Average Order Value =
DIVIDE([Total Revenue], [Total Orders])

Customer Count =
DISTINCTCOUNT(customer_rfm[CustomerID])
```

## Preparation summary
- Raw records: **1,067,371**
- After duplicate removal: **1,033,036**
- Customer-eligible cleaned sales records: **779,425**
- Customers: **5,878**
- Orders: **36,969**
- Revenue: **17,374,804.27**
- Snapshot date: **2011-12-10**

The Power BI `.pbix` file itself must be created/saved in Power BI Desktop. These datasets are prepared for direct import.
