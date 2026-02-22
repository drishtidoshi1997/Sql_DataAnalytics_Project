# 🏢 SQL Data Warehouse Analytics Project

**Sales & Customer Analytics | Star Schema | T-SQL | Business Intelligence**

---

## 📋 Project Overview

A comprehensive data warehouse analytics solution built in SQL Server to transform raw transactional data into actionable business insights. The project implements a star schema with fact and dimension tables, delivering analytical queries that answer key business questions about sales performance, customer behavior, and product profitability.

---

## 📁 Repository Structure

```
Sql_DataAnalytics_Project/
├── Datasets/
│   ├── dim_customers.csv        # Customer dimension data
│   ├── dim_products.csv         # Product dimension data
│   └── fact_sales.csv           # Sales fact transactions
├── Scripts/
│   ├── EDA.sql                   # Exploratory analysis + KPIs + segmentation
│   └── Report.sql                 # Customer & product report views
└── README.md
```

---

## 🎯 Business Questions Answered

- What are our total sales, average price, and units sold?
- Which countries have the highest number of customers?
- Which product categories generate the most revenue?
- Who are our top 10 customers by revenue?
- Which are our top 5 best-selling and bottom 5 underperforming products?
- How do sales trend month by month?
- How do we segment customers based on spending? (VIP, Regular, New)
- How are products distributed across price tiers?
- What is the complete profile of each customer with key KPIs?
- What is the complete profile of each product with performance metrics?

---

## 🔧 Key Features

- **Star Schema Design** – fact_sales + dim_customers + dim_products
- **Window Functions** – ROW_NUMBER, LAG for rankings & YoY comparisons
- **Customer Segmentation** – VIP (≥12 months, >$5K), Regular, New
- **Product Tiers** – High-Performer (>$50K), Mid-Range (≥$10K), Low-Performer
- **Analytical Views** – gold.report_customers & gold.report_products with 15+ KPIs each

---

## 📊 Sample Query

```sql
-- Customer segmentation by spending behavior
WITH customer_segments AS (
    SELECT 
        c.customer_key,
        SUM(f.sales_amount) AS total_spending,
        DATEDIFF(MONTH, MIN(order_date), MAX(order_date)) AS lifespan
    FROM gold.fact_sales f
    LEFT JOIN gold.dim_customers c ON f.customer_key = c.customer_key
    GROUP BY c.customer_key
)
SELECT 
    CASE 
        WHEN lifespan >= 12 AND total_spending > 5000 THEN 'VIP'
        WHEN lifespan >= 12 AND total_spending <= 5000 THEN 'Regular'
        ELSE 'New'
    END AS customer_segment,
    COUNT(customer_key) AS total_customers
FROM customer_segments
GROUP BY customer_segment
ORDER BY total_customers DESC;
```

---

## 🚀 Getting Started

1. **Clone the repository**
2. **Import CSV files** from `/Datasets` into SQL Server
3. **Run scripts** in order:
   - `EDA.sql` – Exploratory analysis, KPIs, rankings, trends, segmentation
   - `Report.sql` – Create `gold.report_customers` and `gold.report_products` views

---

## 💡 Key Insights

- **VIP customers** (≥12 months, >$5K spend) generate highest revenue
- **High-Performer products** (>$50K sales) drive majority of revenue
- Products with negative YoY growth identified for review
- Customer age groups show distinct spending patterns

---

## 🛠️ Skills Demonstrated

- **SQL Server & T-SQL** – Window functions, CTEs, views, date functions
- **Data Modeling** – Star schema design
- **Business Analytics** – Customer segmentation, product performance tiers, KPI development

---

**#SQL #DataWarehouse #BusinessIntelligence #DataAnalytics #TSQL #CustomerAnalytics**
