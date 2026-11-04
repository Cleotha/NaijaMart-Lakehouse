# NaijaMart Lakehouse: End-to-End Data Engineering Pipeline

## Project Overview

NaijaMart Lakehouse is an end-to-end data engineering project built with **PySpark, Databricks, Spark SQL, and Delta Lake**.

The project implements a Medallion Architecture (Bronze, Silver, and Gold) to ingest, clean, validate, transform, and analyse customer, product, and order data from multiple file formats.

The pipeline includes data quality checks, duplicate handling, rejected-record management, and the creation of analytical tables to support business reporting.

## Architecture

The project follows the Medallion Architecture:

**Bronze → Silver → Gold**

- **Bronze Layer:** Ingests raw CSV and JSON datasets into Delta tables while preserving source information and ingestion timestamps.
- **Silver Layer:** Cleans and standardises data, handles duplicates, validates records, and separates rejected records from valid datasets.
- **Gold Layer:** Produces business-focused analytical tables using Spark SQL.

## Data Sources

The pipeline works with three datasets:

| Dataset | File Format |
|---|---|
| Customers | CSV |
| Orders | CSV |
| Products | JSON |

Raw files are stored in Databricks Volumes.

## Pipeline Workflow

### 1. Bronze Layer – Data Ingestion

- Read customer and order datasets from CSV files.
- Read product data from a JSON file.
- Apply explicit schemas.
- Capture source filenames using Spark metadata.
- Add ingestion timestamps.
- Store ingested datasets as Delta tables.

### 2. Silver Layer – Data Cleaning and Validation

The Silver layer prepares the raw datasets for reliable analysis.

Key operations include:

- Standardising column names and text values.
- Trimming whitespace and handling blank values.
- Standardising date and currency fields.
- Removing duplicate records.
- Applying data quality validation rules.
- Separating invalid records into rejection datasets.
- Retaining valid records in clean Silver tables.

Rejected records are stored separately with rejection reasons to support data quality investigation.

### 3. Gold Layer – Business Analytics

The Gold layer contains six analytical tables:

| Gold Table | Purpose |
|---|---|
| `gold_monthly_revenue` | Calculates monthly revenue from delivered orders and month-over-month revenue growth. |
| `gold_top_10_customers` | Identifies the ten highest-revenue customers. |
| `gold_revenue_by_category_city` | Analyses revenue and order counts by product category and customer city. |
| `gold_top_3_products_per_category` | Identifies the three highest-revenue products in each category. |
| `gold_cancelled_returned_rate` | Calculates the combined cancelled and returned order rate by product category. |
| `gold_payment_method_share` | Calculates the percentage share of orders by payment method. |

Revenue calculations are based on delivered orders, while order-status and payment-method metrics use the relevant valid order records.

## Pipeline Execution Summary

The following table summarises the latest pipeline execution:

| Table | Raw Rows | Duplicates Removed | Rejected Rows | Valid Rows |
|---|---:|---:|---:|---:|
| Customers | 331 | 28 | 12 | 291 |
| Products | 43 | 3 | 3 | 37 |
| Orders | 6,140 | 140 | 840 | 5,160 |

The pipeline also generates a summary table containing the number of raw, duplicate, rejected, and valid records for each dataset.

## Data Quality and Reliability

The project incorporates several data engineering practices:

- Explicit schema definition.
- Data validation and standardisation.
- Duplicate detection and removal.
- Rejection handling with recorded reasons.
- Separation of raw, cleaned, and analytical datasets.
- Pipeline execution logging.
- Record-count tracking across pipeline stages.

## Technology Stack

- **Python**
- **PySpark**
- **Apache Spark**
- **Databricks**
- **Spark SQL**
- **Delta Lake**
- **Databricks Unity Catalog Volumes**
- **Git and GitHub**

## Key Data Engineering Concepts Demonstrated

- ETL pipeline development.
- Medallion Architecture.
- Multi-format data ingestion.
- Distributed data processing with PySpark.
- Data quality management.
- Deduplication and record validation.
- Delta table creation and management.
- Window functions and analytical SQL.
- Logging and pipeline monitoring.
- Business-oriented data modelling.

## Project Objective

The goal of this project is to demonstrate how raw data from multiple sources can be transformed into reliable, structured, and analysis-ready datasets using modern data engineering technologies.

The resulting Gold tables provide useful business insights into revenue performance, customer purchasing behaviour, product performance, order statuses, and payment methods.
