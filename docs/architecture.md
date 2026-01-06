# Architecture Overview

This project implements an event-driven, incremental data pipeline on AWS
to ingest retail sales data from a relational database into an S3-based
data lake for analytics.

The design follows a layered data lake architecture with automated
triggering and validation.

---

## High-Level Architecture

```text
AWS RDS (MySQL)
   |
   |  Incremental Extract (AWS Glue - PySpark)
   v
Amazon S3 (Landing Zone)
   |
   |  S3 Event Notification
   v
AWS Lambda
   |
   |  Triggers Glue Data Quality Job
   v
AWS Glue (Data Quality Checks)
   |        |
   |        ├── Valid Records → S3 Staging
   |        └── Invalid Records → S3 Discarded
   v
AWS Glue Data Catalog
   |
   v
Amazon Athena
