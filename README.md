Project Overview
This project focuses on building a modern Data Warehouse using SQL Server. The goal was to take raw "messy" data from two different systems—CRM (Customer Relationship Management) and ERP (Enterprise Resource Planning)—and unify them into a single "Source of Truth" for business analysis.

The architecture follows the Medallion Framework, ensuring that data is progressively cleaned and modeled as it moves through the pipeline.

🏗️ Architecture & Data Flow
The project is divided into three distinct layers:

1. Bronze Layer (The Raw Zone)
Purpose: Lands the raw data from CSV files exactly as-is.

Implementation: Developed Stored Procedures with BULK INSERT logic to automate the loading of CRM and ERP datasets.

Key Feature: Includes a robust load_bronze procedure with TRY...CATCH error handling and batch execution logging.

2. Silver Layer (The Clean Zone)
Purpose: Standardizes and cleanses the raw data.

Transformations: * Data Cleansing: Handled null values and used TRIM to remove unwanted whitespace.

Normalization: Converted inconsistent codes (e.g., 'M', 'S', 'F') into readable formats like 'Married', 'Single', and 'Female'.

Deduplication: Utilized Window Functions (ROW_NUMBER) to identify and remove duplicate records based on the most recent timestamps.

Derived Columns: Calculated fields and standardized date formats.

3. Gold Layer (The Analytics Zone)
Purpose: Delivers business-ready data through a Star Schema.

Data Modeling: Created optimized Views for:

dim_customers: Unified customer profiles from both CRM and ERP sources.

dim_products: Current product catalog with category and maintenance details.

fact_sales: Centralized sales transactions linked to dimensions via surrogate keys.

🛠️ Tech Stack & Skills
Database: Microsoft SQL Server.

SQL Mastery: Advanced Joins, CTEs, Window Functions, Stored Procedures, and View creation.

Data Modeling: Star Schema design, Fact & Dimension tables, and Surrogate Key implementation.

ETL Methodology: Medallion Architecture, Data Integration (CRM + ERP), and Automated Ingestion.

📊 Data Integration Strategy
The project integrates disparate tables to provide a holistic view of the business. For example:

Customer Integration: Combines basic info from crm_cust_info with birthdates from erp_cust_az12 and location data from erp_loc_a101.

Product Integration: Merges product details from crm_prd_info with categorical and maintenance data from erp_px_cat_g1v2.

🚀 How to Run
Ensure you have SQL Server Management Studio (SSMS) installed.

Clone this repository.

Update the file paths in the load_bronze stored procedure to match your local dataset location.

Execute the script to build the schemas, tables, and views.

This project was developed by an AI graduate from Sindh Madressatul Islam University with a focus on building production-ready data environments.
