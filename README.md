# Marketing Analytics — Data Cleaning with SQL

Cleaning and preparing raw marketing data using SQL Server so it is ready for analysis and reporting.

---

## The Problem

A marketing team needed to understand why customer engagement and conversion rates were falling. Before any analysis could happen, the raw data had to be cleaned, standardized, and enriched.

---

## Project Structure

```
marketing-analytics-sql/
│
├── data/
│   └── PortfolioProject_MarketingAnalytics.bak
│
├── sql/
│   ├── dim_customers.sql
│   ├── dim_products.sql
│   ├── fact_customer_journey.sql
│   ├── fact_customer_reviews.sql
│   └── fact_engagement_data.sql
│
├── docs/
│   └── Marketing_Analytics_Business_Case.pptx
│
└── README.md
```

---

## What Each Script Does

**dim_customers.sql**
Joins the customers table with the geography table to add Country and City to each customer record.

**dim_products.sql**
Labels each product as Low, Medium, or High price using a CASE WHEN statement.

| Price | Category |
|-------|----------|
| Under $50 | Low |
| $50 – $200 | Medium |
| Over $200 | High |

**fact_customer_journey.sql**
Removes duplicate journey records using ROW_NUMBER() and fills missing durations with the daily average using COALESCE().

**fact_customer_reviews.sql**
Fixes double-space issues in the ReviewText column using REPLACE().

**fact_engagement_data.sql**
Corrects inconsistent content type labels, splits the Views and Clicks combined column into two separate columns, and standardizes the date format to dd.MM.yyyy.

---

## Tools Used

- SQL Server (T-SQL)
- SQL Server Management Studio (SSMS)
- CTEs and Window Functions
- String and Date Functions

---

## How to Run

1. Open SSMS and restore the `.bak` file from the `/data` folder.
2. Run the SQL scripts from the `/sql` folder in the order listed above.

---

## Roadmap

- [x] Phase 1 — Business Case and Project Planning
- [x] Phase 2 — Data Cleaning with SQL
- [ ] Phase 3 — Advanced Sentiment Analysis using Python
- [ ] Phase 4 — Interactive Power BI Dashboard
- [ ] Phase 5 — Presenting Data to Stakeholders
