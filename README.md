# Overview
This project designs and implements a small, end-to-end ETL analytics pipeline using an AdventureWorks-style dataset and is **co-developed by Arvanitis Anastasis, Lianeris Michail and Tsolaki Eleni**. The objective of the project is to design a unified sales analytics Lakehouse in Databricks, utilizing the medallion architecture, that will serve various analytics demands in an efficient and scalable way. After the implementation of the Lakehouse, the final data schema is ingested into Microsoft Fabric and utilized for data analysis in PowerBI

# Technical Stack
In this project the following tools are used:

- Databricks (community edition)
- Microsoft Fabric
- Microsoft PowerBI (via Microsoft Fabric)

# Business Problem
The dataset consists of 10 csv files repesenting transactional sales data and supporting operational data of mid-size distribution company. The manual consolidation of data in spreadsheets makes reporting slow, error-prone and incosistent while depriving data-driven decisions. In addition, the files show several data quality issues such as incosistent currency formatting, null values, duplicate records. The objective of this project is to organize a modern scalable analytics foundation that preserves raw data for auditability, improves data quality and consistency, supports analytical modeling for business users and enable interactive reporting.

# Solution Architecture
This project design and implements an analytics-ready ETL-pipeline in Databricks, utilizing the medallion architecture. The main pillars of the solution are the following:

- Data Ingestion (Bronze Layer): Raw CSV files are ingested from legacy systems into the Data Lake and organized into Delta tables to ensure a permanent, auditable record of the source data in its original state

- Data Transformation (Silver Layer): Bronze level data transformation suitable for analytics and downstream modeling. Key transformations include, but are not limited to, null values handling, appropriate data types, and basic standardization of text fields

- Data Modeling (Gold Layer): Implementation of a star schema in Delta format to enable analytics-ready data layer that can be tailored to multiple reporting needs

- Gold Layer Data Ingestion: Ingestion of gold layer data into Microsoft Fabric workspace

- BI Semantic Model: Design of a MS PowerBI semantic model (star schema) that supports efficient reporting and analysis

- Data Visualization: Creation of a MS PowerBI report with key measures, such as sales & margin trend, and global sales & profitability

# How to Run
Running the project assumes an active Databricks free tier account, and a Microsoft Fabric account (free trial is available). 

1. Connect the GitHub repo to the Databricks workspace

2. Run [00_create_schemas.ipynb](./notebooks/00_create_schemas.ipynb) located in the *'notebooks'* folder to create a new catalog, medallion schemas, and a volume to save raw data

3. In Databricks, upload the files, located in the [data](./data) folder, into the volume *'project.bronze.raw_data'*

4. Follow the instructions of [Instructions.md](jobs/Instructions.md) to create a job in Databricks in order to run all layers transformations

5. Run the job to create the medallion architecture tables (bronze, silver, and gold layers)

6. Run [parquet_export.ipynb](notebooks/parquet_export.ipynb) to extract gold layer delta tables in parquet format

7. Create a Lakehouse in Microsoft Fabric to store the parquet files

8. Import the parquet files in Fabric Lakehouse

9. Load parquet files as tables (*'Load to Tables'*) in Fabric Lakehouse

10. Create a new report in Microsoft PowerBI (via Microsoft Fabric)

11. Get data from Fabric Lakehouse

12. Create the semantic model of the report
