# Brazilian E-Commerce Azure Data Engineering Project

Built an end-to-end Azure Data Engineering solution using the Brazilian Olist E-Commerce dataset to demonstrate scalable ETL pipelines, cloud data architecture, dimensional modeling, and business intelligence reporting for modern retail analytics. The project showcases industry-level practices in Azure Data Factory, Azure Data Lake Gen2, Azure Databricks, SQL, PySpark, and Power BI.

# 📌 Table of Contents
- [ Overview](#-overview)
- [ Business Problem](#-business-problem)
- [ Project Objectives](#-project-objectives)
- [ Architecture Overview](#️-architecture-overview)
- [ Dataset & Source Systems](#-dataset--source-systems)
- [ Azure Services Used](#️-azure-services-used)
- [ Data Engineering Workflow](#-data-engineering-workflow)
- [ Data Lake Architecture](#️-data-lake-architecture)
- [ Data Modeling](#-data-modeling)
- [ ETL & Data Cleaning Strategy](#-etl--data-cleaning-strategy)
- [ Key Business Metrics](#-key-business-metrics)
- [ Power BI Dashboard](#-power-bi-dashboard)
- [ Project Structure](#-project-structure)
- [ How to Run This Project](#-how-to-run-this-project)
- [ Key Engineering Highlights](#-key-engineering-highlights)
- [ Business Impact](#-business-impact)
- [ Future Enhancements](#-future-enhancements)
- [ Author & Contact](#-author--contact)
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

![image_alt](https://github.com/AjayAntonyPowerBIDataEngineer/EcomAzureDataEngineerPipeline/blob/1074bc7d41e6225824d8796206c748a6110c451b/Screenshot%20(130).png)

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

Executive sales overview
Customer analytics
Seller performance
Product category analysis
Delivery & logistics insights
Geographic sales distribution
Revenue trend analysis

# Project Structure
```plaintext
brazilian-ecommerce-azure-data-engineering/
│
├── README.md
├── architecture/
│   └── solution_architecture.png
│
├── datasets/
│   └── raw_source_files/
│
├── adf-pipelines/
│   ├── master_pipeline/
│   ├── ingestion_pipelines/
│   └── incremental_loads/
│
├── databricks/
│   ├── bronze_layer/
│   ├── silver_layer/
│   ├── gold_layer/
│   └── pyspark_transformations/
│
├── sql/
│   ├── schema_creation/
│   ├── fact_tables/
│   └── dimension_tables/
│
├── powerbi/
│   └── ecommerce_dashboard.pbix
│
├── notebooks/
│   ├── data_cleaning.ipynb
│   ├── exploratory_analysis.ipynb
│   └── business_metrics.ipynb
│
└── docs/
    └── project_documentation.pdf
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
