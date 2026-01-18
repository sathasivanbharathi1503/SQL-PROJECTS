📌 Project Overview

Project Title: Adventure Works Sales Analysis
Database: adventure_works

This project showcases end-to-end SQL analysis on a sales fact table inspired by the Adventure Works dataset.
It focuses on KPI reporting, time-based analysis, customer & product performance, and regional sales insights using MySQL.

The project is designed to demonstrate real-world data analyst SQL skills such as aggregation, grouping, business metrics calculation, and dashboard-ready queries.

🎯 Objectives

Database Setup – Create a structured sales database and fact table

KPI Analysis – Calculate key business metrics (Sales, Cost, Profit, Volume)

Time-Based Analysis – Monthly, quarterly, and yearly sales performance

Business Insights – Identify top customers, products, and regions

Dashboard Support – Provide slicer queries for BI tools (Power BI / Tableau)

🗄️ Project Structure

Adventure-Works-SQL/
│
├── 01_database_setup.sql
├── 02_kpi_queries.sql
├── 03_time_analysis.sql
├── 04_business_insights.sql
└── README.md


1️⃣ Database Setup
Database & Table Creation

```sql
CREATE DATABASE adventure_works;
USE adventure_works;

CREATE TABLE sales_data (
    ProductKey INT,
    OrderDateKey INT,
    DueDateKey INT,
    ShipDateKey INT,
    CustomerKey INT,
    PromotionKey INT,
    CurrencyKey INT,
    SalesTerritoryKey INT,

    SalesOrderNumber VARCHAR(20),
    SalesOrderLineNumber INT,
    RevisionNumber INT,

    OrderQuantity INT,
    UnitPrice DECIMAL(10,2),
    ExtendedAmount DECIMAL(12,2),
    UnitPriceDiscountPct DECIMAL(5,2),
    DiscountAmount DECIMAL(12,2),

    ProductStandardCost DECIMAL(12,2),
    TotalProductCost DECIMAL(12,2),
    SalesAmount DECIMAL(12,2),
    TaxAmt DECIMAL(12,2),
    Freight DECIMAL(12,2),

    CarrierTrackingNumber VARCHAR(30),
    CustomerPONumber VARCHAR(30),

    OrderDate DATE,
    DueDate DATE,
    ShipDate DATE,

    Year INT,
    Month INT,
    Month_Name VARCHAR(20),
    Qtr VARCHAR(5),
    YearMonth VARCHAR(10),

    Day_of_Week INT,
    Day_Name VARCHAR(15),

    FinancialMonth INT,
    FinancialQuarter VARCHAR(5),

    CalculatedSalesAmount DECIMAL(12,2),
    CalculatedProductionCost DECIMAL(12,2),
    Profit DECIMAL(12,2),

    ProductName VARCHAR(100),
    CustomerName VARCHAR(100),
    Region VARCHAR(50),
    Country VARCHAR(50)
);
```

2️⃣ Data Overview

```sql
SELECT COUNT(*) FROM sales_data;
```

3️⃣ KPI Analysis (Dashboard Cards)
🔹 Total Sales

```sql
SELECT SUM(SalesAmount) AS Total_Sales
FROM sales_data;
```

<img width="206" height="81" alt="image" src="https://github.com/user-attachments/assets/a715ad9e-bf3f-4c5f-9a82-46ad624687e8" />


🔹 Total Production Cost

```sql

SELECT 
    SUM(ProductStandardCost * OrderQuantity) AS Total_Production_Cost
FROM sales_data;


```


<img width="247" height="81" alt="image" src="https://github.com/user-attachments/assets/2fa76068-8eff-4421-9d1e-18345fb9b668" />



🔹 Total Profit

```sql
SELECT SUM(Profit) AS Total_Profit
FROM sales_data;

```
<img width="202" height="83" alt="image" src="https://github.com/user-attachments/assets/84621f3f-bf43-4cb9-8566-e216ea5218b8" />


🔹 Total Products Sold

```sql
SELECT SUM(OrderQuantity) AS Total_Products_Sold
FROM sales_data;

```

<img width="218" height="87" alt="image" src="https://github.com/user-attachments/assets/622ff340-1d4c-4e4c-90eb-b88f661e5631" />



4️⃣ Time-Based Sales Analysis
📅 Monthly Sales Performance

```sql
SELECT 
    MONTHNAME(OrderDate) AS Month,
    SUM(SalesAmount) AS Total_Sales
FROM sales_data
GROUP BY MONTH(OrderDate), MONTHNAME(OrderDate)
ORDER BY MONTH(OrderDate);
```
<img width="223" height="310" alt="image" src="https://github.com/user-attachments/assets/942bcaab-5052-4702-96f6-9201b65d6561" />


📊 Quarterly Sales Performance

```sql
SELECT 
    QUARTER(OrderDate) AS Quarter,
    SUM(SalesAmount) AS Quarterly_Sales
FROM sales_data
GROUP BY QUARTER(OrderDate)
ORDER BY Quarter;
```
<img width="241" height="136" alt="image" src="https://github.com/user-attachments/assets/230c88bf-4eee-40c7-8c00-d93d339cbcf6" />


📈 Yearly Sales vs Production Cost

```sql
SELECT
    Year,
    SUM(SalesAmount) AS Total_Sales,
    SUM(ProductStandardCost * OrderQuantity) AS Total_Production_Cost
FROM sales_data
GROUP BY Year
ORDER BY Year;
```

<img width="375" height="165" alt="image" src="https://github.com/user-attachments/assets/78b33dae-d2c9-4766-bb06-c420cc50646f" />


5️⃣ Business Performance Insights
👥 Top 10 Customers by Sales

```sql
SELECT
    CustomerName,
    SUM(SalesAmount) AS Total_Sales
FROM sales_data
GROUP BY CustomerName
ORDER BY Total_Sales DESC
LIMIT 10;
```
<img width="282" height="276" alt="image" src="https://github.com/user-attachments/assets/ecf62f47-e5e5-4383-bd9a-df88d35a1d32" />



🛒 Top 10 Products by Sales

```sql
SELECT
    ProductName,
    SUM(SalesAmount) AS Total_Sales
FROM sales_data
GROUP BY ProductName
ORDER BY Total_Sales DESC
LIMIT 10;
```

<img width="308" height="271" alt="image" src="https://github.com/user-attachments/assets/ed82c4d1-a77c-45a1-a984-36c2c4eb70ab" />


🌍 Sales Performance by Region

```sql
SELECT
    Region,
    SUM(SalesAmount) AS Total_Sales
FROM sales_data
GROUP BY Region
ORDER BY Total_Sales DESC;
```

<img width="248" height="248" alt="image" src="https://github.com/user-attachments/assets/7f012016-987b-4036-b902-3876e10ecb26" />


6️⃣ Dashboard Slicer Queries
Year Slicer

```sql
SELECT DISTINCT Year
FROM sales_data
ORDER BY Year;
```

<img width="102" height="142" alt="image" src="https://github.com/user-attachments/assets/9a550c13-c2d5-44ea-ba33-5092b5cbf6f0" />


Region Slicer

```sql
SELECT DISTINCT Region
FROM sales_data
ORDER BY Region;
```
<img width="182" height="266" alt="image" src="https://github.com/user-attachments/assets/5e224afb-ec82-41e3-ae99-6bd2f97ce6e2" />

Quarter Slicer

```sql
SELECT DISTINCT QUARTER(OrderDate) AS Quarter
FROM sales_data
ORDER BY Quarter;
```

<img width="112" height="122" alt="image" src="https://github.com/user-attachments/assets/c0339b0a-e7cc-4d54-bc01-ad657948aff8" />


Month Slicer

```sql
SELECT DISTINCT MONTHNAME(OrderDate) AS Month_Name
FROM sales_data;
```
<img width="156" height="292" alt="image" src="https://github.com/user-attachments/assets/07232242-7613-4b6e-a6c1-7777b63b8d18" />



📊 Key Insights

Sales performance varies significantly across months and quarters

A small group of customers and products contribute a large share of revenue

Regional analysis helps identify high-performing markets

Profit tracking enables cost vs revenue comparison over time

🧠 Skills Demonstrated

MySQL database & fact table design

KPI calculation for business dashboards

Time-series analysis (monthly, quarterly, yearly)

Customer, product, and regional performance analysis

SQL queries optimized for BI tools


👤 Author

Selvabharathi S
SQL • Data Analytics • Portfolio Project
