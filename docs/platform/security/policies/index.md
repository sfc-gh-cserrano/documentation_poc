---
icon: material/shield-check
title: Policies
---

# :material-shield-check: Policies

## Network Policies

Restrict access by IP address range:

```sql
CREATE NETWORK POLICY office_only
  ALLOWED_IP_LIST = ('10.0.0.0/8', '172.16.0.0/12')
  BLOCKED_IP_LIST = ('10.0.0.99');
```

## Masking Policies

Protect sensitive data at the column level:

```sql
CREATE MASKING POLICY email_mask AS (val STRING)
  RETURNS STRING ->
  CASE
    WHEN CURRENT_ROLE() IN ('ADMIN') THEN val
    ELSE REGEXP_REPLACE(val, '.+@', '***@')
  END;
```

## Row Access Policies

Filter rows based on the querying role:

```sql
CREATE ROW ACCESS POLICY region_filter AS (region STRING)
  RETURNS BOOLEAN ->
  CURRENT_ROLE() = 'ADMIN' OR region = CURRENT_REGION();
```
