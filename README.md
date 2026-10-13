# RetailPulse — Retail Sales Intelligence Pipeline

## Overview

RetailPulse is an end-to-end retail analytics project designed to demonstrate how business data can be collected, validated, transformed, stored, and visualized to support data-driven decision-making.

The project simulates a retail organization's data workflow, from CRM/ERP-style exports to a centralized SQL database and interactive Power BI dashboards.

## Business Problem

Retail organizations generate data across sales, customers, products, geography, and suppliers. When this information is stored in separate files or systems, analyzing performance consistently becomes difficult.

RetailPulse addresses this challenge by building a repeatable data pipeline that combines historical sales data with simulated monthly data deliveries.

## Architecture

```text
CRM / ERP Data Exports
          |
          v
   Incoming CSV Folder
          |
          v
 Python Data Ingestion
          |
          v
 Validation and Quality Checks
          |
          v
    Python ETL Pipeline
          |
          v
       SQL Server
          |
          v
     Power BI Dashboard
```

## Technology Stack

- **Python:** Data ingestion, validation, transformation, and automation
- **Pandas:** Data manipulation and processing
- **SQL Server:** Data storage, relational modeling, and analytical queries
- **Power BI:** Business intelligence dashboards and reporting
- **Git and GitHub:** Version control, collaboration, and documentation

## Data Sources

### Historical Dataset

The initial historical dataset is based on a public Superstore sales dataset. It contains sales transactions and associated customer, product, shipping, and geographical attributes.

The project includes prepared fact and dimension tables to support analytical modeling.

### Simulated Monthly Data

Future data deliveries will be represented by synthetic CSV batches that simulate monthly exports from a CRM or ERP system.

These batches will be used to demonstrate incremental ingestion, validation, duplicate detection, and database updates.

Supplier attributes and product-supplier assignments included in the prepared dataset pack are synthetic and intended for demonstration.

## Planned Pipeline

1. **Data collection:** Detect incoming CSV files and record ingestion metadata.
2. **Data validation:** Check required columns, data types, missing values, and invalid records.
3. **Data transformation:** Clean, standardize, and prepare records for analytical use.
4. **Data loading:** Load data into SQL Server staging and analytical tables.
5. **Data quality monitoring:** Track ingestion outcomes, rejected records, and duplicate files.
6. **Business intelligence:** Develop Power BI dashboards for sales, profitability, product performance, and regional trends.

## Planned Repository Structure

```text
retailpulse-sales-intelligence/
├── data/
│   ├── incoming/
│   ├── raw/
│   ├── processed/
│   └── synthetic/
├── src/
│   ├── collect_data.py
│   ├── validate_data.py
│   ├── transform_data.py
│   └── load_sql.py
├── sql/
│   ├── schema.sql
│   └── analytics_queries.sql
├── tests/
├── docs/
│   ├── architecture.md
│   └── data_dictionary.md
├── powerbi/
├── requirements.txt
├── .gitignore
└── README.md
```

## Expected Outcomes

- A repeatable, file-based data ingestion workflow
- Reliable validation and transformation of sales data
- A structured SQL Server analytical data model
- Incremental processing of simulated monthly data deliveries
- Interactive business intelligence dashboards
- Documented, testable, and version-controlled data engineering code

## Project Status

**Current stage:** Initial setup and data ingestion design.

Subsequent milestones will implement the ingestion pipeline, data quality checks, ETL transformations, SQL Server integration, and Power BI reporting.

## Data Disclaimer

This is a portfolio project using a public historical sample dataset and clearly identified synthetic data for demonstration. It is not connected to a live retail company's CRM or ERP system.
