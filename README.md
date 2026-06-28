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

## Phase 3 — Advanced Sentiment Analysis using Python

Connects to the SQL Server database, pulls the cleaned customer reviews, and runs sentiment analysis using NLTK's VADER model.

### What the Script Does

**customer_reviews_enrichment.py**
Fetches customer reviews from `dbo.customer_reviews`, cleans double spaces in the review text, and enriches each record with three new columns:

| Column | Description |
|--------|-------------|
| SentimentScore | A score between -1 (most negative) and 1 (most positive) |
| SentimentCategory | Positive, Negative, Neutral, Mixed Positive, or Mixed Negative |
| SentimentBucket | Score grouped into ranges: -1.0 to -0.5, -0.49 to 0.0, 0.0 to 0.49, 0.5 to 1.0 |

The final output is saved as `fact_customer_reviews_with_sentiment.csv` for use in Power BI.

### Tools Used

- Python 3
- pandas
- NLTK (VADER Sentiment Analyzer)
- SQLAlchemy
- SQL Server

### How to Run

1. Install dependencies:
```bash
   pip install pandas nltk sqlalchemy pyodbc
```
2. Run the script:
```bash
   python customer_reviews_enrichment.py
```
3. Output file `fact_customer_reviews_with_sentiment.csv` will be saved in the same folder.

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

## Phase 4 — Interactive Power BI Dashboard

Built an interactive Power BI dashboard to visualize the cleaned and enriched data, enabling the marketing team to explore performance across customers, products, and campaigns.

### What the Dashboard Covers

- Customer conversion rates by region, product, and journey stage
- Sentiment breakdown of customer reviews by product and rating
- Marketing campaign engagement metrics — views, clicks, and likes by content type
- Revenue trends segmented by product price category

### Tools Used

- Power BI Desktop
- DAX for calculated measures
- `fact_customer_reviews_with_sentiment.csv` as the sentiment data source
- SQL Server as the primary data source

---

## Phase 5 — Presenting Data to Stakeholders

Findings were compiled and presented to stakeholders using a structured presentation covering the business problem, methodology, key insights, and recommended actions.

### Key Insights Delivered

- Identified the customer segments with the highest drop-off rates in the journey funnel
- Highlighted products with high ratings but negative sentiment — indicating a gap between score and review text
- Pinpointed underperforming campaign content types and recommended reallocation of marketing spend

The business case presentation is available in the `/docs` folder.

---

## Tools and Skills

| Area | Tools |
|------|-------|
| Data Cleaning | SQL Server, T-SQL, SSMS |
| Python Analysis | pandas, NLTK, SQLAlchemy |
| Visualization | Power BI, DAX |
| Version Control | Git, GitHub |

---

## Roadmap

- [x] Phase 1 — Business Case and Project Planning
- [x] Phase 2 — Data Cleaning with SQL
- [x] Phase 3 — Advanced Sentiment Analysis using Python
- [x] Phase 4 — Interactive Power BI Dashboard
- [x] Phase 5 — Presenting Data to Stakeholders
