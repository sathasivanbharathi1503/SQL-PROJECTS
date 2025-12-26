📌 Project Overview

Project Title: Retail Sales Analysis
Database: sql_project_p2

This project demonstrates core SQL skills used by data analysts to clean, explore, and analyze retail sales data.
It focuses on real-world business questions, data quality checks, and KPI-driven analysis using MySQL.

🎯 Objectives

Database Setup – Create a retail sales database and table

Data Cleaning – Identify and remove invalid or NULL records

Exploratory Data Analysis (EDA) – Understand sales, customers, and categories

Business Analysis – Answer real business questions using SQL

🗄️ Project Structure
Retail-Sales-SQL/
│
├── 01_database_setup.sql
├── 02_data_cleaning.sql
├── 03_analysis_queries.sql
└── README.md

1️⃣ Database Setup
Database & Table Creation 
```sql
CREATE DATABASE IF NOT EXISTS sql_project_p2;
USE sql_project_p2;

DROP TABLE IF EXISTS retail_sales;

CREATE TABLE retail_sales (
    transaction_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(15),
    age INT,
    category VARCHAR(15),
    quantity INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);
```

2️⃣ Data Exploration & Cleaning
Basic Exploration
```sql
SELECT COUNT(*) AS total_records FROM retail_sales;
SELECT COUNT(DISTINCT customer_id) AS unique_customers FROM retail_sales;
SELECT DISTINCT category FROM retail_sales;

Identify NULL Records
SELECT *
FROM retail_sales
WHERE 
    transaction_id IS NULL
    OR sale_date IS NULL
    OR sale_time IS NULL
    OR gender IS NULL
    OR category IS NULL
    OR quantity IS NULL
    OR cogs IS NULL
    OR total_sale IS NULL;

Remove Invalid Records (Safe Update Handled)
SET SQL_SAFE_UPDATES = 0;

DELETE FROM retail_sales
WHERE 
    transaction_id IS NULL
    OR sale_date IS NULL
    OR sale_time IS NULL
    OR gender IS NULL
    OR category IS NULL
    OR quantity IS NULL
    OR cogs IS NULL
    OR total_sale IS NULL;

SET SQL_SAFE_UPDATES = 1;
```

3️⃣ Data Analysis & Business Questions

Q1. Sales on a specific date (2022-11-05)

```sql
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';
```

<img width="918" height="312" alt="image" src="https://github.com/user-attachments/assets/b8a1960f-a341-453a-b2af-807f73597116" />




Q2. Clothing sales (quantity ≥ 4) in Nov-2022

```sql
SELECT *
FROM retail_sales
WHERE 
    category = 'Clothing'
    AND DATE_FORMAT(sale_date, '%Y-%m') = '2022-11'
    AND quantity >= 4;
```

<img width="926" height="433" alt="image" src="https://github.com/user-attachments/assets/857fc47e-8ff8-4fec-b6fa-3b662d6f6444" />


Q3. Total sales by category

```sql
SELECT 
    category,
    SUM(total_sale) AS net_sale,
    COUNT(*) AS total_orders
FROM retail_sales
GROUP BY category;
```

<img width="302" height="113" alt="image" src="https://github.com/user-attachments/assets/e2d9eb69-bf8f-4369-9f48-09b0c39a9f98" />



Q4. Average age of customers in Beauty category

```sql
SELECT 
    ROUND(AVG(age), 2) AS avg_age
FROM retail_sales
WHERE category = 'Beauty';
```

<img width="141" height="62" alt="image" src="https://github.com/user-attachments/assets/73890bc6-09aa-4c46-abe0-6f7508bdd7f3" />



Q5. High-value transactions (total_sale > 1000)

```sql
SELECT *
FROM retail_sales
WHERE total_sale > 1000;

```

<img width="912" height="508" alt="image" src="https://github.com/user-attachments/assets/8fc35bb3-db6e-4e7f-881d-eac07ede645c" />


Q6. Transactions by gender and category

```sql
SELECT 
    category,
    gender,
    COUNT(transaction_id) AS total_transactions
FROM retail_sales
GROUP BY category, gender
ORDER BY category;
```

<img width="323" height="163" alt="image" src="https://github.com/user-attachments/assets/ca9b6506-5d64-4585-b9d1-5f991ed07564" />


Q7. Best selling month (average sale) for each year

```sql
SELECT 
    year,
    month,
    avg_sale
FROM (
    SELECT 
        YEAR(sale_date) AS year,
        MONTH(sale_date) AS month,
        AVG(total_sale) AS avg_sale,
        RANK() OVER (
            PARTITION BY YEAR(sale_date)
            ORDER BY AVG(total_sale) DESC
        ) AS rnk
    FROM retail_sales
    GROUP BY YEAR(sale_date), MONTH(sale_date)
) t
WHERE rnk = 1;

```

<img width="292" height="76" alt="image" src="https://github.com/user-attachments/assets/d161fab8-0dfb-4a2e-a4f7-76452c4354a3" />


Q8. Top 5 customers by total sales

```sql
SELECT 
    customer_id,
    SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;

```

<img width="217" height="151" alt="image" src="https://github.com/user-attachments/assets/d9f8903b-0fa6-44cf-a7fd-865c39314f01" />


Q9. Unique customers per category

```sql
SELECT 
    category,
    COUNT(DISTINCT customer_id) AS unique_customers
FROM retail_sales
GROUP BY category;
```

<img width="266" height="106" alt="image" src="https://github.com/user-attachments/assets/848ee14e-5e3f-4478-8d8e-4bc80333194a" />


Q10. Orders by shift (Morning / Afternoon / Evening)

```sql
WITH hourly_sale AS (
    SELECT *,
        CASE
            WHEN HOUR(sale_time) < 12 THEN 'Morning'
            WHEN HOUR(sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
            ELSE 'Evening'
        END AS shift
    FROM retail_sales
)
SELECT 
    shift,
    COUNT(*) AS total_orders
FROM hourly_sale
GROUP BY shift;

```

<img width="220" height="115" alt="image" src="https://github.com/user-attachments/assets/f33defd1-d939-4019-8a5c-9722cf85e8a6" />


📊 Key Findings

Sales are distributed across multiple product categories such as Clothing and Beauty

High-value transactions highlight premium customer segments

Monthly trends help identify peak sales periods

Customer behavior analysis reveals repeat and high-spending customers

🧠 Skills Demonstrated

MySQL database design

Data cleaning with safe update handling

Exploratory data analysis (EDA)

Window functions & CTEs

KPI and business insight generation

🧾 Resume One-Liner

Built a retail sales SQL project using MySQL involving database design, data cleaning, and KPI-driven sales analysis.

▶️ How to Use

Clone the repository

Run 01_database_setup.sql

Import dataset (CSV → MySQL Workbench)

Execute cleaning and analysis scripts

Modify queries to explore further insights

👤 Author

Selvabharathi S
SQL & Data Analytics Portfolio Project

