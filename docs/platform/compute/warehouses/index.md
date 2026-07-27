---
icon: material/warehouse
title: Warehouses
---

# :material-warehouse: Warehouses

## Overview

Virtual warehouses provide the compute power for executing queries and DML operations.

## Sizing Guide

| Size | Credits/Hour | Use Case |
|------|-------------|----------|
| X-Small | 1 | Development, light queries |
| Small | 2 | Dashboard workloads |
| Medium | 4 | ETL pipelines |
| Large | 8 | Heavy transformations |
| X-Large | 16 | Large-scale data processing |

## Configuration

```sql
CREATE WAREHOUSE analytics_wh
  WAREHOUSE_SIZE = 'MEDIUM'
  AUTO_SUSPEND = 60
  AUTO_RESUME = TRUE
  MIN_CLUSTER_COUNT = 1
  MAX_CLUSTER_COUNT = 3
  SCALING_POLICY = 'STANDARD';
```

## Best Practices

- Set `AUTO_SUSPEND` to 60 seconds for interactive workloads
- Use multi-cluster warehouses for concurrent dashboard users
- Separate ETL and BI workloads into dedicated warehouses

## Related Pages

- [Sizing Guide](sizing.md) — Detailed benchmarks for choosing the right size
- [Multi-Cluster Warehouses](multi-cluster.md) — Scaling for concurrency
