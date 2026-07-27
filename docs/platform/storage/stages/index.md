---
icon: material/folder-upload
title: Stages
---

# :material-folder-upload: Stages

## Overview

Stages are locations where data files are stored for loading and unloading operations.

## Types

| Type | Description | Example |
|------|-------------|---------|
| Internal | Managed by Snowflake | `@~`, `@%table`, `@stage_name` |
| External (S3) | AWS S3 bucket | `@s3_stage` |
| External (GCS) | Google Cloud Storage | `@gcs_stage` |
| External (Azure) | Azure Blob Storage | `@azure_stage` |

## Creating an External Stage

```sql
CREATE STAGE raw_data_stage
  URL = 's3://acme-data-lake/raw/'
  STORAGE_INTEGRATION = aws_integration
  FILE_FORMAT = (TYPE = 'PARQUET');
```

## Listing Files

```sql
LIST @raw_data_stage/2024/;
```
