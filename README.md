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
architecture-beta
    service rds(database)
    service glue_ingest(server)
    service s3_landing(bucket)
    service lambda_trigger(server)
    service glue_qc(server)
    service s3_staging(bucket)
    service s3_discarded(bucket)
    service glue_catalog(database)
    service athena(analytics)

    rds --> glue_ingest
    glue_ingest --> s3_landing
    s3_landing --> lambda_trigger
    lambda_trigger --> glue_qc
    glue_qc --> s3_staging
    glue_qc --> s3_discarded
    s3_staging --> glue_catalog
    glue_catalog --> athena
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
