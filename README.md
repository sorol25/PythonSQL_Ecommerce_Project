<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0a0a1a,50:1a1a3e,100:0d1b2a&height=200&section=header&text=E-Commerce%20Data%20Analysis&fontSize=38&fontColor=ffffff&fontAlignY=38&desc=Python%20%C3%97%20MySQL%20%7C%20End-to-End%20Analytics%20Project&descAlignY=56&descSize=16&animation=fadeIn" width="100%"/>

<a href="https://git.io/typing-svg">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=20&pause=1000&color=38BDF8&center=true&vCenter=true&width=700&lines=Brazilian+E-Commerce+Dataset+%F0%9F%9B%92;CSV+%E2%86%92+MySQL+Automated+Pipeline+%F0%9F%97%84%EF%B8%8F;15+Business+SQL+Queries+Solved+%F0%9F%94%8D;Revenue+%7C+Retention+%7C+Rankings+%F0%9F%93%8A" alt="Typing SVG" />
</a>

<br/>

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white"/>
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white"/>
  <img src="https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white"/>
  <img src="https://img.shields.io/badge/Seaborn-4C72B0?style=for-the-badge&logo=python&logoColor=white"/>
</p>

<p>
  <img src="https://img.shields.io/github/stars/sorol25/PythonSQL_Ecommerce_Project?style=for-the-badge&color=38BDF8"/>
  <img src="https://img.shields.io/github/forks/sorol25/PythonSQL_Ecommerce_Project?style=for-the-badge&color=0ea5e9"/>
  <img src="https://img.shields.io/badge/License-MIT-22c55e?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/SQL_Queries-15-f59e0b?style=for-the-badge"/>
</p>

</div>

---

## 📌 Project Overview

> **Real-world Brazilian e-commerce data, analyzed end-to-end** — from loading 7 raw CSV files into a relational MySQL database, all the way through 15 progressively complex business intelligence queries.

This project demonstrates a production-style **Python → SQL analytics pipeline**: automated schema inference, bulk data ingestion, and layered business questions answered with clean SQL — from basic aggregations to advanced window functions.

---

## 🗄️ Database Schema

Seven interconnected tables power all queries:

```
┌─────────────┐     ┌──────────────┐     ┌──────────────┐
│  customers  │────▶│    orders    │────▶│  order_items │
│─────────────│     │──────────────│     │──────────────│
│ customer_id │     │ order_id     │     │ order_id     │
│ customer_   │     │ customer_id  │     │ product_id   │
│   city      │     │ order_       │     │ seller_id    │
│ customer_   │     │  purchase_   │     │ price        │
│   state     │     │  timestamp   │     └──────────────┘
└─────────────┘     └──────────────┘            │
                           │                    ▼
                    ┌──────────────┐     ┌──────────────┐
                    │   payments   │     │   products   │
                    │──────────────│     │──────────────│
                    │ order_id     │     │ product_id   │
                    │ payment_     │     │ product_     │
                    │   value      │     │  category    │
                    │ payment_     │     └──────────────┘
                    │ installments │
                    └──────────────┘
     ┌──────────────┐        ┌──────────────────┐
     │   sellers    │        │   geolocation    │
     │──────────────│        │──────────────────│
     │ seller_id    │        │ zip_code_prefix  │
     │ seller_city  │        │ lat / lng        │
     └──────────────┘        └──────────────────┘
```

---

## 📁 Repository Structure

```
PythonSQL_Ecommerce_Project/
│
├── 📓 PythonSql_ecommerce.ipynb     # Main analysis notebook (EDA + all 15 SQL queries)
├── 🐍 csv_to_sql.py                 # Automated CSV → MySQL ingestion script
├── customers.csv
├── orders.csv
├── order_items.csv
├── payments.csv
├── products.csv
├── sellers.csv
├── geolocation.csv
│
└── 📖 README.md
```

---

## 🚀 Getting Started

### Prerequisites

```
Python 3.8+  |  MySQL Server  |  Jupyter Notebook
```

Install required Python libraries:

```bash
pip install pandas mysql-connector-python matplotlib seaborn numpy
```

---

### Step 1 — Clone the Repository

```bash
git clone https://github.com/sorol25/PythonSQL_Ecommerce_Project.git
cd PythonSQL_Ecommerce_Project
```

---

### Step 2 — Set Up MySQL Database

```sql
CREATE DATABASE ecommerce;
```

---

### Step 3 — Load CSV Data into MySQL

`csv_to_sql.py` handles everything automatically:

- Infers SQL column types from pandas dtypes (`INT`, `FLOAT`, `DATETIME`, `TEXT`)
- Creates all 7 tables dynamically with `CREATE TABLE IF NOT EXISTS`
- Handles `NaN → NULL` conversion cleanly before insert
- Commits each table as an independent transaction

Update the data folder path, then run:

```python
# In csv_to_sql.py — update this line to your local path:
folder_path = 'your/path/to/data/folder'
```

```bash
python csv_to_sql.py
```

---

### Step 4 — Open the Analysis Notebook

```bash
jupyter notebook PythonSql_ecommerce.ipynb
```

Update the DB connection at the top:

```python
db = mysql.connector.connect(
    host="localhost",
    username="root",
    password="your_password",
    database="ecommerce"
)
```

---

## 🔍 Business Questions Solved

### 🟢 Basic — Foundations

| # | Question | Highlight |
|---|---|---|
| 1 | Unique cities where customers are located | 4,119 distinct cities |
| 2 | Total orders placed in 2017 | **45,101 orders** |
| 3 | Total sales per product category | 74 categories — top: *Bed Table Bath* at $1.71M |
| 4 | % of orders paid in installments | **~99.99%** of all transactions |
| 5 | Customer count by state | SP dominates — visualized as bar chart |

---

### 🟡 Intermediate — Business Aggregations

| # | Question | SQL Technique |
|---|---|---|
| 1 | Orders per month in 2018 | `MONTHNAME()` · `GROUP BY` · `sns.barplot` |
| 2 | Avg products per order, grouped by city | CTE + `AVG()` + multi-table `JOIN` |
| 3 | Revenue % share per product category | Inline subquery ratio calculation |
| 4 | Price vs. purchase frequency correlation | `np.corrcoef` → **r = –0.106** *(weak negative)* |
| 5 | Revenue per seller, ranked | `DENSE_RANK() OVER(ORDER BY revenue DESC)` |

---

### 🔴 Advanced — Window Functions & Analytics

| # | Question | SQL Technique |
|---|---|---|
| 1 | Moving average of order values per customer | `AVG() OVER(ROWS BETWEEN 2 PRECEDING AND CURRENT ROW)` |
| 2 | Cumulative monthly sales per year | `SUM() OVER(ORDER BY years, months)` |
| 3 | Year-over-year revenue growth rate | `LAG()` → 2017: **+12,112%** · 2018: **+20%** |
| 4 | 6-month customer retention rate | Dual CTE + `DATE_ADD()` + `LEFT JOIN` |
| 5 | Top 3 spenders per year | `DENSE_RANK() OVER(PARTITION BY year ...)` |

---

## 📊 Key Findings at a Glance

```
💰  Total Platform Revenue (all time)   ~$16,008,872
📦  Orders in 2017                       45,101
📈  YoY Growth 2017 → vs 2016           +12,112%  (platform launch ramp)
📈  YoY Growth 2018 → vs 2017           +20%
🛍️   Top Revenue Category               Bed Table Bath — 10.70% of total
🔁  Orders Paid via Installments        ~99.99%
📉  Price vs. Purchase Correlation      –0.106  (weak negative — cheaper items sell more)
```

---

## 💡 Featured Queries

**Year-over-Year Revenue Growth**

```sql
WITH a AS (
  SELECT YEAR(orders.order_purchase_timestamp) AS years,
         ROUND(SUM(payments.payment_value), 2)  AS payment
  FROM orders JOIN payments ON orders.order_id = payments.order_id
  GROUP BY years ORDER BY years
)
SELECT years,
       ROUND(
         ((payment - LAG(payment,1) OVER(ORDER BY years)) /
           LAG(payment,1) OVER(ORDER BY years)) * 100
       , 2) AS yoy_growth_pct
FROM a;
```

**Moving Average of Customer Order Values**

```sql
SELECT customer_id, order_purchase_timestamp, payment,
  AVG(payment) OVER(
    PARTITION BY customer_id
    ORDER BY order_purchase_timestamp
    ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
  ) AS moving_avg
FROM (
  SELECT orders.customer_id, orders.order_purchase_timestamp,
         payments.payment_value AS payment
  FROM payments JOIN orders ON payments.order_id = orders.order_id
) AS a;
```

**Top 3 Customers by Spend Per Year**

```sql
SELECT years, customer_id, payment, d_rank FROM (
  SELECT YEAR(orders.order_purchase_timestamp) years,
         orders.customer_id,
         SUM(payments.payment_value) payment,
         DENSE_RANK() OVER(
           PARTITION BY YEAR(orders.order_purchase_timestamp)
           ORDER BY SUM(payments.payment_value) DESC
         ) d_rank
  FROM orders JOIN payments ON payments.order_id = orders.order_id
  GROUP BY YEAR(orders.order_purchase_timestamp), orders.customer_id
) AS a
WHERE d_rank <= 3;
```

---

## 📜 License

```
MIT License — Copyright (c) 2026 Yeamine Alam Sorol
Free to fork, star, and build upon.
```

---

## 👨‍💻 About the Author

<div align="center">

**Yeamine Alam Sorol**
*Data Analyst*

<br/>

<a href="https://www.linkedin.com/in/yeamine-alam-sorol-746831347">
  <img src="https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white"/>
</a>
&nbsp;
<a href="https://github.com/sorol25/PythonSQL_Ecommerce_Project">
  <img src="https://img.shields.io/badge/⭐_Star_This_Repo-181717?style=for-the-badge&logo=github&logoColor=white"/>
</a>

</div>

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0d1b2a,50:1a1a3e,100:0a0a1a&height=120&section=footer" width="100%"/>

<sub>If this project helped you, consider starring ⭐ the repo or sharing it with someone learning Data Analytics.</sub>

</div>
