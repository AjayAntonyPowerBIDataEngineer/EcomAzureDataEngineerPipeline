# Brazilian E-Commerce Azure Data Engineering Project

Built an end-to-end Azure Data Engineering solution using the Brazilian Olist E-Commerce dataset to demonstrate scalable ETL pipelines, cloud data architecture, dimensional modeling, and business intelligence reporting for modern retail analytics. The project showcases industry-level practices in Azure Data Factory, Azure Data Lake Gen2, Azure Databricks, SQL, PySpark, and Power BI.

# 📌 Table of Contents
- [Overview](#overview)
- [Business Problem](#business-problem)
- [Project Objectives](#project-objectives)
- [Architecture Overview](#architecture-overview)
- [Dataset & Source Systems](#dataset--source-systems)
- [Azure Services Used](#azure-services-used)
- [Data Engineering Workflow](#data-engineering-workflow)
- [Fact and Dimensional Data Processing](#fact-and-dimensional-data-processing)
- [Data Pipeline](#data-pipeline)
- [Data Modeling](#data-modeling)
- [ETL & Data Cleaning Strategy](#etl--data-cleaning-strategy)
- [Key Business Metrics](#key-business-metrics)
- [Power BI Dashboard](#power-bi-dashboard)
- [Project Structure](#project-structure)
- [How to Run This Project](#how-to-run-this-project)
- [Key Engineering Highlights](#key-engineering-highlights)
- [Business Impact](#business-impact)
- [Future Enhancements](#future-enhancements)
- [Author & Contact](#author--contact)
***
# Overview

This project demonstrates an end-to-end Azure Data Engineering solution built using the Brazilian Olist E-Commerce dataset. The platform was designed to simulate a real-world enterprise analytics environment where data is ingested from multiple heterogeneous sources, transformed using scalable cloud-based ETL pipelines, and modeled into business-ready analytical datasets.

The project leverages Azure Data Factory for orchestration, Azure Data Lake Gen2 for storage, Azure Databricks and PySpark for distributed data processing, SQL for data modeling, and Power BI for interactive business intelligence reporting.

The solution showcases modern Data Engineering practices including Medallion Architecture, incremental loading, dimensional modeling, data quality validation, and scalable cloud analytics workflows.

---

# Business Problem

Modern e-commerce organizations generate massive amounts of transactional and operational data from multiple disconnected systems such as orders, payments, customers, products, sellers, and logistics platforms.

Without a centralized cloud-based analytics platform, organizations face challenges in:

- Integrating data from multiple heterogeneous sources
- Maintaining data quality and consistency
- Building scalable ETL pipelines
- Monitoring operational and business KPIs
- Tracking customer and seller performance
- Optimizing delivery and fulfillment operations
- Generating actionable business insights for decision-making

This project addresses these challenges by building a scalable Azure-based Data Engineering platform capable of processing, transforming, and analyzing Brazilian e-commerce data efficiently.

---

# Architecture Overview

![image_alt](https://github.com/AjayAntonyPowerBIDataEngineer/EcomAzureDataEngineerPipeline/blob/c8805a7169079ef53e90d8999ce278cc09690476/Pipeline.png)

# Dataset

Dataset Used:

Brazilian E-Commerce Public Dataset by Olist

The dataset contains multi-domain e-commerce data including:

- Orders
- Customers
- Products
- Sellers
- Payments
- Reviews
- Geolocation
- Order Items

Data was ingested from multiple simulated enterprise source systems including:

- SQL Server
- REST APIs
- Snowflake
- CSV files
- Excel files
- JSON files
- SFTP sources

---

# Tools & Technologies

| Technology | Purpose |
|---|---|
| Azure Data Factory | ETL orchestration and data movement |
| Azure Data Lake Gen2 | Raw, staging, and curated storage |
| Azure Databricks | Distributed data transformation |
| PySpark | Data cleaning and processing |
| SQL | Data modeling and querying |
| Power BI | Interactive dashboards and reporting |
| GitHub | Version control and project documentation |
Architecture inspired by your ETL project presentation

# Data Engineering Workflow

- Data Ingestion

  Azure Data Factory pipelines ingest data from:
  
  SQL databases
  REST APIs
  Snowflake tables
  CSV/Excel/JSON files
  SFTP servers

- Raw Layer (Bronze)

    Data is landed into Azure Data Lake Gen2 without modification.
    
    Features:
    
    Historical retention
    Partitioned storage
    Incremental ingestion
    Metadata-driven loading
  
- Data Transformation (Silver)

  Azure Databricks + PySpark used for:
  
  Schema validation
  Null handling
  Type casting
  Deduplication
  Data standardization
  Business rule validation
  
- Curated Layer (Gold)

Business-ready dimensional tables created for analytics and reporting.

# Fact and Dimensional Data Processing

![image_alt](https://github.com/AjayAntonyPowerBIDataEngineer/EcomAzureDataEngineerPipeline/blob/7abe0e953321438efa023abe25bbc5dd1edb8a98/Screenshot%20(194).png)

The pipeline follows a Medallion-style data processing architecture where raw Parquet files are first ingested into the Bronze layer using date-based partitioning for scalable storage and historical tracking.

During the transformation phase, data cleansing and standardization processes are applied before loading the data into the Silver layer.

### Dimension Table Processing

Small Dimension Tables are processed using a Truncate and Load strategy, where existing records are replaced with the latest dataset during every execution.
Large Dimension Tables are processed using Slowly Changing Dimension (SCD Type 1 / Type 2) logic based on business and reporting requirements:

- SCD Type 1 updates existing records without maintaining history.
- SCD Type 2 preserves historical changes by creating versioned records.

### Fact Table Processing

Fact Tables are processed using an Append-only strategy to efficiently handle high-volume transactional data and maintain historical records.

Finally, curated Gold layer views are generated for downstream reporting and analytics consumption in Power BI dashboards.

# Data Pipeline

![image_alt](https://github.com/AjayAntonyPowerBIDataEngineer/EcomAzureDataEngineerPipeline/blob/43fd258c914d2423a0a646e0fc8f243cb0787ff6/Data%20Pipeline%20For%20loading%20tables.png)

- What This Pipeline Demonstrates
  
Metadata-Driven Orchestration using Lookup, Set Variable, and dynamic mapping enables reusable and configurable pipeline execution instead of hardcoded logic.
Enterprise Logging & Auditing through SP_START_LOG_ENTRY, SP_SUCCESS, and SP_FAILURE supports execution tracking, monitoring, and operational visibility.
Proper Error Handling with dedicated success and failure paths improves pipeline reliability and maintainability.
Layered Data Processing following the Raw → Silver → Gold flow aligns with modern Medallion/Lakehouse architecture practices.
Clear Separation of Responsibilities where ADF manages orchestration and ingestion, while Databricks handles transformations and business logic processing.

# ETL & Data Cleaning Strategy

### Implemented industry-standard PySpark transformations:

- Data Quality Checks
- Null validation
- Duplicate detection
- Schema enforcement
- Invalid date handling
- Referential integrity validation
- Cleaning Operations
- Removed corrupted records
- Standardized timestamps
- Converted currencies & numeric formats
- Trimmed inconsistent text values
- Filtered negative payment values
- Standardized category mappings
- Performance Optimizations
- Incremental loading
- Partition pruning
- Delta-based processing
- Optimized joins
- Surrogate key generation
  
# Data Modeling

### Implemented a Galaxy Schema Data Model.
![image_alt](https://github.com/AjayAntonyPowerBIDataEngineer/EcomAzureDataEngineerPipeline/blob/9716d4b8d16ab56730e0ba802f478e3b07cfaed3/Screenshot%20(132).png)


The project follows a Galaxy Schema (Fact Constellation Schema) design pattern for scalable e-commerce analytics. Transactional fact tables including Fact_Orders, Fact_Order_Items, Fact_Payments, and Fact_Reviews are connected with shared dimension tables such as Dim_Customers, Dim_Products, Dim_Sellers, and Dim_Geolocation.

The model primarily uses one-to-many relationships between dimensions and facts, while fact-to-fact analytical relationships are conceptually many-to-many through shared business keys like order_id and customer_id.

## Slowly Changing Dimension Strategy

- SCD Type 2:
  - Dim_Customers
  - Dim_Sellers

- SCD Type 1:
  - Dim_Products
    
- Overwrite:
   - Dim_Geolocation

### Loading Strategy

- Append-Only Fact Tables:
  - Fact_Orders
  - Fact_Order_Items
  - Fact_Payments
  - Fact_Reviews

- Overwrite Strategy:
  - Staging and temporary transformation tables in Silver layer

The solution also implements incremental MERGE operations, surrogate key modeling, and Medallion Architecture (Bronze, Silver, Gold) for scalable cloud-based analytics engineering.

# Key Business Metrics

### The dashboard tracks critical e-commerce KPIs:

KPI	Description
- Total Revenue	Overall sales generated
- Order Volume	Number of customer orders
- Average Order Value	Revenue per order
- Delivery Performance	Shipping delay analysis
- Customer Satisfaction	Review score trends
- Top Performing Sellers	Revenue contribution
- Product Category Trends	Best-selling categories
- Payment Analysis	Payment method insights
- Customer Retention	Repeat purchase behavior
  
### BI Dashboard

Interactive dashboards built using Power BI provide:

![image_alt](https://github.com/AjayAntonyPowerBIDataEngineer/EcomAzureDataEngineerPipeline/blob/084fa4dc491914d973c3846fd035422b8a497b9d/4_3.png)



# Project Structure
```plaintext
ecom-azure-data-engineering-pipeline/
│
├── README.md
│
├── architecture/
│   ├── Data Pipeline For loading tables.png
│   ├── Factanddimprocessing.png
│   └── Pipeline.png
│
├── datasets/
│   ├── source_datasets/
│   │   ├── DS_SRC_CSV_PAYMENTS.json
│   │   ├── DS_SRC_FACT_ORDER_ITEMS.json
│   │   ├── DS_SRC_ONPREM_SQL_SERVER.json
│   │   ├── DS_SRC_SFTP.json
│   │   ├── DS_SRC_SNOWFLAKE_ORDERITEMS.json
│   │   └── DS_SQLSERVER_PQ.json
│   │
│   ├── sink_datasets/
│   │   ├── DS_OUT_EXCEL_PARQUET.json
│   │   ├── DS_SINK_DIM_SQL_PQ.json
│   │   ├── DS_SINK_FACT_SQL_PQ.json
│   │   └── DS_SQL_FACT.json
│   │
│   └── file_datasets/
│       ├── DS_AZURE_SQL_PARQUET.json
│       ├── DS_CSV_PARQUET.json
│       ├── DS_EXCEL_PQ.json
│       ├── DS_OUT_out001tgt.json
│       ├── DS_SFTP_OUT_CSV.json
│       └── DS_SRC_raw01t.json
│
├── databricks/
│   ├── bronze_to_silver/
│   │   ├── Customers Bronze -> Silver.ipynb
│   │   ├── Geolocation Bronze -> Silver.ipynb
│   │   ├── Seller Bronze -> Silver.ipynb
│   │   ├── OrderItems Bronze to Silver Full Load.ipynb
│   │   ├── OrderReviews Bronze to Silver Full Load.ipynb
│   │   ├── Orders Bronze to Silver Full Load.ipynb
│   │   └── Payments Bronze to Silver Full Load.ipynb
│   │
│   ├── silver_to_gold/
│   │   ├── Customers Silver -> Gold.ipynb
│   │   ├── Geolocation Silver -> Gold.ipynb
│   │   ├── Products Silver -> Gold.ipynb
│   │   ├── Seller Silver -> Gold.ipynb
│   │   ├── OrderItemsFact Silver to Gold.ipynb
│   │   ├── Payments Silver to Gold.ipynb
│   │   └── Reviews Silver to Gold.ipynb
│   │
│   ├── dimension_processing/
│   │   └── SCD 1 Products Bronze -> Silver.ipynb
│   │
│   └── setup/
│       └── setup.ipynb
│
├── orchestration/
│   ├── master_pipeline/
│   │   └── PL1_MASTER.json
│   │
│   ├── raw_ingestion_pipelines/
│   │   ├── PL2_RAW_DATA.json
│   │   ├── PL3_CLOUDSG_CSV_EXCEL.json
│   │   ├── PL_SWITCH_CSV_EXCEL.json
│   │   └── PL_SQL_SERVER.json
│   │
│   ├── dimension_pipelines/
│   │   ├── PL_DIM_TABLE_GEOLOCATION.json
│   │   ├── PL_REST_API_DIM_PRODUCTCATEGORY.json
│   │   ├── PL_SFTP_CUSTOMERS_DIM.json
│   │   ├── PL_SQL_DIM_TABLE_PRODUCTS.json
│   │   └── PL_SQL_DIM_TABLE_SELLERS.json
│   │
│   └── fact_pipelines/
│       ├── PL_CSV_Payments.json
│       ├── PL_EXCEL_FACT_REVIEWS.json
│       ├── PL_SNOWFLAKE_ORDERITEMS.json
│       └── PL_SQL_FACT_TABLE_ORDERS.json
│
├── linked_services/
│   ├── AzureBlobStorage1.json
│   ├── AzureSqlDatabase1.json
│   ├── LS_CSV_PARQUET.json
│   ├── LS_EXCEL_PARQUET.json
│   ├── LS_OUT.json
│   ├── LS_REST_API.json
│   ├── LS_SQLSERVER_ONPREM.json
│   ├── LS_SRC_SFTP.json
│   └── Snowflake1.json
│
├── integration_runtime/
│   └── integrationRuntime1.json
│
├── factory/
│   └── ADF-VB8B-ETL-DEV.json
│
├── workflows/
│   ├── raw_to_bronze_workflow/
│   ├── bronze_to_silver_workflow/
│   ├── silver_to_gold_workflow/
│   └── scd_processing_workflow/
│
├── docs/
│   ├── implementation_notes/
│   ├── pipeline_execution_flow/
│   ├── medallion_architecture/
│   └── scd_processing_logic/
│
└── publish_config/
    └── publish_config.json
```

Connect Power BI to Gold layer

# Key Engineering Highlights

✔ Enterprise ETL orchestration using ADF
✔ Multi-source cloud ingestion
✔ Distributed PySpark transformations
✔ Incremental loading strategy
✔ Medallion architecture implementation
✔ Dimensional modeling for analytics
✔ Production-style data validation
✔ Cloud-native scalable architecture
✔ Business KPI reporting using Power BI

# Business Impact

This project enables organizations to:

Improve decision-making through centralized analytics
Monitor seller and product performance
Identify delivery inefficiencies
Optimize customer experience
Track revenue and operational KPIs
Build scalable analytics infrastructure

# Future Enhancements

Real-time streaming using Azure Event Hub
CI/CD using Azure DevOps
Delta Lake implementation
Data quality monitoring framework
Machine Learning forecasting models
Automated metadata-driven pipelines

# Author & Contact

Ajay Suresh
Azure Data Engineer | Power BI Developer

💼 Focus Areas: Azure Data Engineering, ETL Pipelines, PySpark, Data Warehousing, Power BI
🔗 LinkedIn Portfolio
🔗 GitHub Projects
