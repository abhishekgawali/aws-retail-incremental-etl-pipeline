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

```mermaid
flowchart TB
    RDS[AWS RDS (MySQL)]
    GLUE1[AWS Glue<br/>Incremental PySpark Job]
    S3L[S3 Landing Zone]
    LAMBDA[AWS Lambda<br/>S3 Event Trigger]
    GLUE2[AWS Glue<br/>Data Quality Checks]
    S3S[S3 Staging<br/>(Valid Records)]
    S3D[S3 Discarded<br/>(Invalid Records)]
    CATALOG[AWS Glue Data Catalog]
    ATHENA[Amazon Athena]

    RDS --> GLUE1
    GLUE1 --> S3L
    S3L --> LAMBDA
    LAMBDA --> GLUE2
    GLUE2 --> S3S
    GLUE2 --> S3D
    S3S --> CATALOG
    CATALOG --> ATHENA
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
