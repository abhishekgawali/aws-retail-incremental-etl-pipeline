# AWS Retail Incremental ETL Pipeline

## Overview
This project implements an end-to-end, production-style data engineering
pipeline on AWS to incrementally ingest retail order data from a MySQL
database (AWS RDS) into an Amazon S3 data lake for analytics and reporting.

The pipeline is event-driven, scalable, and includes automated data quality
validation, making it suitable for large-scale retail datasets.

---

## Architecture

## Architecture


```text
AWS RDS (MySQL)
   → AWS Glue (Incremental PySpark Job)
   → Amazon S3 (Landing Zone)
   → AWS Lambda (S3 Event Trigger)
   → AWS Glue (Data Quality Checks)
      ├── S3 Staging (Valid Records)
      └── S3 Discarded (Invalid Records)
   → AWS Glue Data Catalog
   → Amazon Athena
```




## Project Structure
```text
aws-retail-incremental-etl-pipeline/
├── glue_jobs/
│   ├── rds_to_s3_incremental.py
│   └── data_quality_checks.py
├── lambda/
│   └── trigger_glue_job.py
├── sql/
│   ├── create_metadata_table.sql
│   └── create_orders_table.sql
├── docs/
│   ├── architecture.md
│   └── incremental_loading.md
└── README.md
```
