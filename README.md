Retail Store Analytics – End-to-End Data Engineering Pipeline
=============================================================

An **end-to-end Data Engineering project** implementing the **Medallion Architecture (Bronze → Silver → Gold)** on **Databricks (Delta Lake)** and building a **Star Schema semantic model** for **Power BI dashboards**.

This project demonstrates **data ingestion, transformation, dimensional modeling, surrogate key strategy, data quality handling, and business KPI reporting**.

📌 Project Architecture
=======================

🔷 Medallion Architecture
-------------------------

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Raw CSV → Bronze (Raw Delta)            → Silver (Cleaned & Standardized)            → Gold (Star Schema: Fact + Dimensions)            → Power BI Semantic Model → Dashboard   `

🛠 Tech Stack
=============

LayerToolStorageDelta Lake (Databricks)ProcessingDatabricks SQLCatalogUnity CatalogModelingStar Schema (Kimball)VisualizationPower BILanguageSQL, DAX

📂 Dataset
==========

Retail store transactional dataset containing:

*   Customer ID
    
*   Product Category & Item
    
*   Price & Quantity
    
*   Total Spend
    
*   Payment Method
    
*   Location
    
*   Transaction Date
    
*   Discount Flag
    

🥉 Bronze Layer – Raw Ingestion
===============================

### 📥 Source

CSV file stored in **Unity Catalog Volume**

### ⚙️ Load Strategy

*   Schema inferred
    
*   No transformations
    
*   Stored as Delta for audit & reprocessing
    

Table:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   bronze.retail_sales_raw   `

🥈 Silver Layer – Data Cleaning & Standardization
=================================================

### 🔄 Transformations

*   Renamed columns (removed spaces & special characters)
    
*   Casted data types
    
*   Standardized categorical fields (UPPER)
    
*   Parsed transaction\_date
    
*   Normalized boolean discount flag
    
*   Filtered null transaction records
    

Table:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   silver.retail_sales_clean   `

🥇 Gold Layer – Dimensional Model (Star Schema)
===============================================

⭐ Fact Table
------------

### gold.fact\_sales

ColumnDescriptioncustomer\_keyFK to dim\_customerproduct\_keyFK to dim\_productlocation\_keyFK to dim\_locationpayment\_keyFK to dim\_payment\_methoddate\_keyFK to dim\_datequantityUnits soldprice\_per\_unitUnit pricetotal\_spentRevenuediscount\_appliedDiscount flag

📐 Dimension Tables
-------------------

### dim\_customer

*   customer\_key (Surrogate)
    
*   customer\_id (Business key)
    

### dim\_product

*   product\_key
    
*   item
    
*   category
    

### dim\_location

*   location\_key
    
*   location
    

### dim\_payment\_method

*   payment\_key
    
*   payment\_method
    

### dim\_date

Generated using min/max transaction dates:

*   date\_key
    
*   transaction\_date
    
*   year
    
*   quarter
    
*   month
    
*   month\_name
    
*   week\_of\_year
    
*   day
    

🔑 Surrogate Key Strategy
=========================

*   Generated using DENSE\_RANK()
    
*   Implemented **Unknown member (0)** to avoid NULL foreign keys
    
*   Ensured referential integrity for BI tools
    

🧪 Data Quality Handling
========================

IssueSolutionInvalid column namesRenamed in SilverNULL dimension joinsDefault key = 0Many-to-many in BIFixed dimension grainMissing datesGenerated full calendarSchema mismatchUsed fully qualified catalog.schema.table

🔗 Star Schema Model
====================

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML            `dim_customer                   |              dim_date                   |  dim_product — fact_sales — dim_location                   |           dim_payment_method`

✔ One-to-many relationships✔ Single direction filtering✔ Optimized for Power BI performance

📊 Power BI Semantic Model
==========================

Relationships
-------------

FromToTypedim\_customerfact\_sales1:\*dim\_productfact\_sales1:\*dim\_locationfact\_sales1:\*dim\_payment\_methodfact\_sales1:\*dim\_datefact\_sales1:\*

📐 DAX Measures
===============

Core KPIs
---------

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Total Revenue = SUM(fact_sales[total_spent])  Total Transactions = COUNTROWS(fact_sales)  Avg Basket Size =  DIVIDE([Total Revenue], [Total Transactions], 0)   `

Repeat Purchase Logic
---------------------

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Customer Transactions =  CALCULATE(      [Total Transactions],      ALLEXCEPT(dim_customer, dim_customer[customer_key])  )   `

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Repeat Purchase Rate =  DIVIDE(      CALCULATE(DISTINCTCOUNT(dim_customer[customer_key]),          FILTER(dim_customer, [Customer Transactions] > 1)      ),      DISTINCTCOUNT(dim_customer[customer_key]),      0  )   `

📈 KPI Dashboard
================

🔝 KPI Cards
------------

*   Total Revenue
    
*   Total Transactions
    
*   Avg Basket Size
    
*   Repeat Purchase %
    

📊 Visuals
----------

### Time Series

Line Chart:

*   Revenue by Month
    
*   Transactions by Month
    
*   Basket Size Trend
    

### Product Insights

Bar Chart:

*   Revenue by Category
    
*   Basket Size by Category
    

### Customer Behavior

Donut Chart:

*   Repeat vs One-Time Customers
    

### Channel Analysis

Stacked Column:

*   Revenue by Location
    
*   Payment Method split
    

🎯 Business Insights
====================

*   Identified top-performing product categories
    
*   Measured customer retention (Repeat Purchase %)
    
*   Tracked basket size trends over time
    
*   Compared payment method performance
    
*   Evaluated online vs offline contribution
    

⚡ Performance Optimization
==========================

*   Delta Lake for fast reads & ACID transactions
    
*   Star schema for BI query efficiency
    
*   Surrogate keys for compact joins
    
*   Cleaned Silver layer for reusable datasets
    

🚧 Challenges & Resolutions
===========================

ChallengeResolutionDelta invalid column namesCleaned in SilverMissing tables across schemasUsed Unity Catalog fully qualified namesNULL product keys in factAdded Unknown member (0)Many-to-many in Power BIRebuilt dim\_product grainDate intelligence errorsMarked dim\_date as Date table

🔮 Future Enhancements
======================

*   Incremental loads with Auto Loader
    
*   SCD Type 2 for customer dimension
    
*   RFM segmentation
    
*   Cohort retention analysis
    
*   Databricks Workflows orchestration
    
*   Unity Catalog data governance
    

🧠 Key Learnings
================

*   Built Medallion architecture end-to-end
    
*   Implemented Kimball dimensional modeling
    
*   Handled data quality and surrogate key design
    
*   Created BI-optimized semantic model
    
*   Delivered retail analytics KPIs
    

📷 Dashboard Preview
====================

> Add screenshots of:

*   KPI page
    
*   Trend analysis
    
*   Customer segmentation
    

🚀 How to Run
=============

1️⃣ Databricks
--------------

*   Create catalog & schemas
    
*   Upload CSV to Unity Catalog Volume
    
*   Run Bronze → Silver → Gold SQL scripts
    

2️⃣ Power BI
------------

*   Connect to Databricks SQL Warehouse
    
*   Load Gold tables
    
*   Create relationships
    
*   Add DAX measures
    
*   Build dashboard
    

Author

** Asharafraza Desai **
** Data Engineer | Databricks | Power BI**
