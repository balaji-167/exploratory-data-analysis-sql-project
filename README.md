# Exploratory Data Analysis with SQL

A pure-SQL exploratory analysis of a retail sales data warehouse, no BI tool, just queries to uncover trends, rankings, segments, and the anomalies hiding underneath the headline numbers.

## About the Data

A star-schema retail dataset (bike shop) across three tables:

| Table | Rows | Contents |
|---|---|---|
| `fact_sales` | 60,398 | Order-level transactions — dates, quantity, price, sales amount |
| `dim_customers` | 18,484 | Demographics — country, gender, marital status, birthdate |
| `dim_products` | 295 | Category, subcategory, product line, cost |

**Scope:** $29.35M in sales · 27,657 orders · 18,484 customers · Dec 2010 – Jan 2014

## Business Questions

The analysis was built to answer questions a retail owner would actually ask:

**Revenue & Product**
1. How much are we selling, and which categories and products actually drive that revenue?
2. Which products are worth keeping, and which are dead weight?
3. How dependent are we on any single category?

**Growth & Trends**
4. Is the business growing — and is that growth coming from more customers, more orders, or bigger orders?
5. How does each year compare to the last, and to our own average?
6. Is demand seasonal, and when should we plan inventory around it?

**Customers**
7. Who are our most valuable customers, and how much of the business rests on them?
8. Do customers come back, or do they buy once and disappear?
9. Which countries and demographics generate the most value, not just the most volume?

## What I Did

Twelve SQL scripts, each covering one analysis technique:

- **Database & dimension exploration** - schema, distinct dimensions, date boundaries
- **Measures exploration** - core KPIs in a single consolidated report
- **Magnitude & ranking analysis** - revenue by category, country, and demographic; top/bottom performers via `RANK()`
- **Change-over-time & cumulative analysis** - yearly/monthly trends and running totals with `SUM() OVER()`
- **Performance analysis** - year-over-year and vs-average comparisons using `LAG()` and window functions
- **Part-to-whole analysis** - each category's share of total revenue
- **Data segmentation** - customers bucketed into VIP / Regular / New; products into cost bands via `CASE`
- **Customer & product reports** - two final consolidated views with derived KPIs (recency, average order value, monthly spend)

## Key Insights

**1. Revenue is dangerously concentrated in one category.**
Bikes drive **96.5% of all revenue** ($28.3M), while Accessories (2.4%) and Clothing (1.2%) contribute almost nothing — despite Accessories generating *more orders* than Bikes in 2013. The business is effectively a single-product company.

**2. 2013 was a breakout year — but not the way it looks.**
Revenue jumped **+180%** (from $5.8M to $16.3M) as Accessories and Clothing scaled from 76 orders in 2012 to **24,499 orders in 2013**. Volume, not price, drove the growth.

**3. Average order value collapsed as the mix shifted.**
AOV fell from **$3,193 (2011) → $310 (2013)** - a 90% drop. The company traded a small number of high-ticket bike sales for a flood of cheap add-ons. Healthy for reach, risky for margin.

**4. Australia is the most valuable market per customer, not the US.**
The US leads on total revenue ($9.16M), but Australia earns **$2,523 per customer vs the US's $1,225** — more than double, from less than half the customer base. The US looks big because it's wide, not because it's deep.

**5. Retention is the weakest link.**
**62.9% of customers ordered only once.** Meanwhile the **VIP segment — just 9% of customers — drives 36.7% of revenue**. A small loyal core carries the business while the majority never return.

**6. Demand is strongly seasonal.**
Within 2013, monthly revenue climbed steadily from $857K (Jan) to **$1.87M (Dec)** — a clear year-end peak worth planning inventory around.

## Tools Used

`SQL Server` · `T-SQL` - window functions (`SUM() OVER`, `LAG()`, `RANK()`), CTEs, `CASE` segmentation, date functions

---
*Part of my data analytics portfolio — [balaji-167](https://github.com/balaji-167)*
