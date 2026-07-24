# Customer Shopping Behavior Analysis

End-to-end retail analytics project analyzing 3,900 customer transactions to uncover what drives purchases, repeat business, and revenue — using Python, SQL (MySQL), and Power BI.

## Business Problem

A retail company wanted to better understand its customers' shopping behavior in order to improve sales, customer satisfaction, and long-term loyalty. Management had noticed shifting purchasing patterns across demographics, product categories, and sales channels, and needed to know which factors — discounts, reviews, seasonality, or payment preferences — actually drive consumer decisions and repeat purchases.

**Core question:** How can the company leverage consumer shopping data to identify trends, improve customer engagement, and optimize marketing and product strategies?

## Project Overview

This project follows a full analytics workflow, from raw data to stakeholder-ready insight:

1. **Data Preparation & Modeling (Python)** — Clean and transform the raw dataset for analysis.
2. **Data Analysis (SQL)** — Structure the data and run queries to extract insights on customer segments, loyalty, and purchase drivers.
3. **Visualization (Power BI)** — Build an interactive dashboard highlighting key patterns and trends.
4. **Reporting** — Summarize findings into clear, actionable business recommendations.

## Dataset

- **Rows:** 3,900 transactions
- **Columns:** 18
- **Key fields:**
  - Customer demographics — Age, Gender, Location, Subscription Status
  - Purchase details — Item Purchased, Category, Purchase Amount, Season, Size, Color
  - Shopping behavior — Discount Applied, Promo Code Used, Previous Purchases, Frequency of Purchases, Review Rating, Shipping Type
- **Data quality issue:** 37 missing values in Review Rating

## Step 1 — Data Preparation in Python

Using `pandas`, the dataset was loaded and profiled with `df.info()` and `.describe()` before any cleaning.

- **Missing data handling:** Imputed the 37 missing Review Rating values using the median rating of each product category, preserving category-level accuracy instead of using a single global average.
- **Column standardization:** Renamed all columns to `snake_case` for consistency and readability.
- **Feature engineering:**
  - `age_group` — created by binning customer ages
  - `purchase_frequency_days` — derived from purchase data
- **Redundancy check:** Verified `discount_applied` and `promo_code_used` carried duplicate signal, and dropped `promo_code_used`.
- **Database integration:** Connected the cleaned DataFrame to MySQL to hand off to the SQL analysis stage.

## Step 2 — Data Analysis in SQL (MySQL)

With the cleaned data loaded into MySQL, ten queries were written to answer specific business questions rather than perform generic exploration:

| # | Query | Key Finding |
|---|-------|-------------|
| 1 | Revenue by Gender | Male customers generated $157,890 in revenue vs. $75,191 from female customers |
| 2 | High-Spending Discount Users | 839 customers used a discount but still spent above the average purchase amount |
| 3 | Top 5 Products by Rating | Gloves, Sandals, Boots, Hat, and Skirt — all rated above 3.75 |
| 4 | Shipping Type Comparison | Express shipping customers spend slightly more on average ($60.48) than Standard ($58.46) |
| 5 | Subscribers vs. Non-Subscribers | Non-subscribers (2,847 customers) generated $170,436 in revenue vs. $62,645 from subscribers (1,053) |
| 6 | Discount-Dependent Products | Hat, Sneakers, Coat, Sweater, and Pants each have discount rates above 47% |
| 7 | Customer Segmentation | Classified customers as Loyal (3,116), Returning (701), or New (83) |
| 8 | Top 3 Products per Category | Identified best-selling items within Accessories, Clothing, Footwear, and Outerwear |
| 9 | Repeat Buyers & Subscriptions | Of customers with 5+ purchases, 2,518 are not subscribed vs. 958 who are |
| 10 | Revenue by Age Group | Young Adults drive the most revenue ($62,143), followed by Middle-Aged, Adult, and Senior groups |

## Step 3 — Dashboard in Power BI

An interactive, single-page dashboard was built so stakeholders can explore the findings without requesting ad hoc reports. It includes:

- KPI cards for number of customers (3.9K), average purchase amount ($59.76), and average review rating (3.75)
- Slicers for Subscription Status, Gender, Category, and Shipping Type
- A subscription-mix donut chart (27% subscribed vs. 73% not subscribed)
- Revenue and sales breakdowns by product category
- Revenue and sales breakdowns by age group

## Business Recommendations

- **Boost subscriptions** — Non-subscribers currently drive far more total revenue than subscribers, indicating significant headroom to convert this segment through subscriber-exclusive benefits.
- **Build customer loyalty programs** — Reward repeat buyers to grow the Loyal segment and move more customers out of the smaller Returning and New tiers.
- **Review discount policy** — Several products are discounted more than 47% of the time; balance the sales lift against margin impact.
- **Lead with top-rated products** — Highlight Gloves, Sandals, Boots, Hat, and Skirt in marketing campaigns given their strong ratings.
- **Target high-value segments** — Prioritize marketing spend toward Young Adults and Express-shipping customers, who show the strongest revenue signals.

## Repository Structure

```
├── python/              # Data cleaning, feature engineering, and MySQL load scripts
├── sql/                 # SQL queries for each business question
├── dashboard/           # Power BI (.pbix) dashboard file
├── report/              # Full project report and business recommendations
└── README.md
```

## Tech Stack

- **Python** — pandas, data cleaning, feature engineering
- **MySQL** — data modeling and SQL analysis
- **Power BI** — interactive dashboard and visualization

## How to Reproduce

1. Clone the repository
2. Run the Python scripts in `/python` to clean the raw dataset and load it into MySQL
3. Execute the queries in `/sql` against the loaded database
4. Open the `.pbix` file in `/dashboard` with Power BI Desktop to explore the interactive dashboard
