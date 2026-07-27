---
icon: material/file-document
title: File Formats
---

# :material-file-document: File Formats

## Supported Formats

| Format | Structured | Semi-Structured | Binary |
|--------|-----------|-----------------|--------|
| CSV | :material-check: | | |
| JSON | | :material-check: | |
| Parquet | :material-check: | | |
| Avro | | :material-check: | |
| ORC | :material-check: | | |
| XML | | :material-check: | |

## Example Definitions

```sql
CREATE FILE FORMAT csv_format
  TYPE = 'CSV'
  FIELD_DELIMITER = ','
  SKIP_HEADER = 1
  NULL_IF = ('NULL', 'null', '');

CREATE FILE FORMAT json_format
  TYPE = 'JSON'
  STRIP_OUTER_ARRAY = TRUE;
```
