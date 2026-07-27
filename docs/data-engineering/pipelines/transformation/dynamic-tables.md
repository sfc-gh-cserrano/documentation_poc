---
icon: material/table-pivot
title: Dynamic Tables
---

# :material-table-pivot: Dynamic Tables

Declarative, managed transformations with automatic refresh.

See also: [Transformation Overview](index.md) | [Task DAGs](task-dags.md)

## When to Use Dynamic Tables

| Use Case | Dynamic Tables | Tasks |
|----------|---------------|-------|
| Declarative SQL transforms | :material-check: | |
| Complex procedural logic | | :material-check: |
| Automatic dependency resolution | :material-check: | |
| Custom scheduling | | :material-check: |
| Incremental processing | :material-check: (auto) | Manual |

## Layered Pipeline

```sql
-- Silver layer: cleaned
CREATE DYNAMIC TABLE silver.customers
  TARGET_LAG = '30 minutes'
  WAREHOUSE = transform_wh
  AS
  SELECT
    id,
    TRIM(LOWER(email)) AS email,
    COALESCE(first_name, 'Unknown') AS first_name,
    last_name,
    signup_date
  FROM bronze.raw_customers
  WHERE email IS NOT NULL;

-- Gold layer: aggregated
CREATE DYNAMIC TABLE gold.customer_metrics
  TARGET_LAG = '1 hour'
  WAREHOUSE = transform_wh
  AS
  SELECT
    c.id,
    c.email,
    COUNT(o.order_id) AS total_orders,
    SUM(o.amount) AS lifetime_value,
    MAX(o.order_date) AS last_order_date
  FROM silver.customers c
  LEFT JOIN silver.orders o ON c.id = o.customer_id
  GROUP BY 1, 2;
```

## Monitoring Refresh

```sql
SELECT *
FROM TABLE(INFORMATION_SCHEMA.DYNAMIC_TABLE_REFRESH_HISTORY(
  NAME => 'gold.customer_metrics'
))
ORDER BY refresh_start_time DESC
LIMIT 10;
```
