# Retail Store Analytics – End-to-End Data Engineering Pipeline

An **end-to-end Data Engineering project** implementing the **Medallion Architecture (Bronze → Silver → Gold)** on **Databricks (Delta Lake)** and building a **Star Schema semantic model** for **Power BI dashboards**.

This project demonstrates **data ingestion, transformation, dimensional modeling, surrogate key strategy, data quality handling, and business KPI reporting**.

## 📌 Project Architecture

### 🔷 Medallion Architecture

```plaintext
Raw CSV → Bronze (Raw Delta) → Silver (Cleaned & Standardized) → Gold (Star Schema: Fact + Dimensions) → Power BI Semantic Model → Dashboard
```

## 🛠 Tech Stack

### Layer Tool 
- Storage: Delta Lake (Databricks)
- Processing: Databricks SQL 
- Catalog: Unity Catalog 
- Modeling: Star Schema (Kimball) 
- Visualization: Power BI 
- Language: SQL, DAX

## 📂 Dataset
Retail store transactional dataset containing:
- Customer ID
- Product Category & Item
- Price & Quantity
- Total Spend
- Payment Method
- Location
- Transaction Date
- Discount Flag

## 🥉 Bronze Layer – Raw Ingestion ##
### 📥 Source ###
CSV file stored in **Unity Catalog Volume**
### ⚙️ Load Strategy ###
* Schema inferred  
* No transformations  
* Stored as Delta for audit & reprocessing  
Table:
dim_retail_sales_raw  
---
### 🥈 Silver Layer – Data Cleaning & Standardization ###
### 🔄 Transformations ###
* Renamed columns (removed spaces & special characters)
* Casted data types  
* Standardized categorical fields (UPPER)
* Parsed transaction_date  
* Normalized boolean discount flag  
* Filtered null transaction records  
table:
silver.retail_sales_clean  
to be created accordingly.
---
note: The detailed transformations are described in the original document.
---
n### 🥇 Gold Layer – Dimensional Model (Star Schema) ###
definition of fact and dimension tables follows.
details provided in the original content.
detailed schema definitions are included.
e.g., `fact_sales`, `dim_customer`, `dim_product`, etc.
each with their respective columns and keys.
details about surrogate key strategy and data quality handling are also included.
details on star schema relationships and Power BI model setup follow.
e.g., one-to-many relationships, filtering directions, performance optimizations.
e.g., relationships diagram in Markdown table format if needed.
details on DAX measures for KPIs like Total Revenue, Total Transactions, Avg Basket Size, Repeat Purchase Rate. These include formulas such as:
total revenue = SUM(fact_sales[total_spent])
total transactions = COUNTROWS(fact_sales)
avg basket size = DIVIDE([Total Revenue], [Total Transactions], 0)
and repeat purchase rate formula.
details on KPI dashboard visuals including time series charts, bar charts for product insights,
donut charts for customer behavior, stacked column charts for channel analysis,
and business insights derived from these visuals.
e.g., top-performing categories, customer retention metrics etc.
development of performance optimization strategies using Delta Lake features,
stars schema design,
surrogate keys,
and clean Silver layer datasets.
e.g., challenges faced such as invalid column names or missing tables and their resolutions are discussed in detail.
deas for future enhancements like incremental loads with Auto Loader,
sCD Type 2 implementation,
rFM segmentation,
cohort analysis,
and data governance improvements via Unity Catalog are outlined.
e.g., key learnings include architecture building,
dimensional modeling implementation,
data quality management,
and semantic model creation that supports retail KPIs.
best practices learned during the project are summarized here.
below is a placeholder for dashboard preview images or links to screenshots if available.>
screenshots of KPI page, trend analysis, customer segmentation can be added here.>
defining how to run the project steps both in Databricks environment and Power BI setup:
one-time setup instructions for creating catalog/schema/uploading CSVs/running scripts in Databricks;
ext steps to connect Power BI to Databricks SQL Warehouse, load tables, create relationships and measures to build dashboards.}
author section with name "Asharafraza Desai" and roles as Data Engineer at Databricks & Power BI.
