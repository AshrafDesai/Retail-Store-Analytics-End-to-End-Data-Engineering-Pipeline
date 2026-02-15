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

