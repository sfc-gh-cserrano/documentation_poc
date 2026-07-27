---
icon: material/server-network
title: Multi-Cluster Warehouses
---

# :material-server-network: Multi-Cluster Warehouses

Multi-cluster warehouses automatically scale compute to handle concurrency spikes.

See also: [Warehouse Overview](index.md) | [Sizing Guide](sizing.md)

## When to Use Multi-Cluster

- Dashboard workloads with 20+ concurrent users
- Unpredictable query bursts during business hours
- Avoiding queue times during peak demand

## Configuration

```sql
ALTER WAREHOUSE analytics_wh SET
  MIN_CLUSTER_COUNT = 1
  MAX_CLUSTER_COUNT = 6
  SCALING_POLICY = 'STANDARD';
```

## Scaling Policies

| Policy | Behavior | Best For |
|--------|----------|----------|
| STANDARD | Scales out after 20s of queueing, scales in after 2-3 checks | Most workloads |
| ECONOMY | Scales out only after 6 min of sustained queueing | Cost-sensitive, tolerant of wait |

## Monitoring Cluster Usage

```sql
SELECT
  warehouse_name,
  cluster_number,
  AVG(avg_running) AS avg_queries,
  MAX(avg_queued_load) AS peak_queued
FROM SNOWFLAKE.ACCOUNT_USAGE.WAREHOUSE_LOAD_HISTORY
WHERE start_time > DATEADD('day', -7, CURRENT_TIMESTAMP())
GROUP BY 1, 2
ORDER BY 1, 2;
```

!!! warning
    Multi-cluster warehouses multiply credit consumption. A 3-cluster Medium warehouse uses 12 credits/hour at peak (4 credits x 3 clusters).
