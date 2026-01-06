# AWS Retail Incremental ETL Pipeline

## Overview
This project implements an end-to-end, production-style data engineering
pipeline on AWS to incrementally ingest retail order data from a MySQL
database (AWS RDS) into an Amazon S3 data lake for analytics and reporting.

The pipeline is event-driven, scalable, and includes automated data quality
validation, making it suitable for large-scale retail datasets.

---

## Architecture

```mermaid
architecture-beta
    service rds(database) [AWS RDS (MySQL)]
    service glue1(server) [AWS Glue - Incremental Job]
    service s3(bucket) [Amazon S3 - Landing]
    service lambda(server) [AWS Lambda Trigger]
    service glue2(server) [AWS Glue - Data Quality]
    service s3good(bucket) [S3 Staging]
    service s3bad(bucket) [S3 Discarded]
    service catalog(database) [Glue Data Catalog]
    service athena(analytics) [Amazon Athena]

    rds --> glue1
    glue1 --> s3
    s3 --> lambda
    lambda --> glue2
    glue2 --> s3good
    glue2 --> s3bad
    s3good --> catalog
    catalog --> athena
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
