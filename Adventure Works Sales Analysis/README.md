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

<img width="242" height="92" alt="image" src="https://github.com/user-attachments/assets/af24e652-daf0-474e-9fb4-4ad34b79b90e" />


