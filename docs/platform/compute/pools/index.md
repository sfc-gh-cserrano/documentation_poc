---
icon: material/application-brackets
title: Compute Pools
---

# :material-application-brackets: Compute Pools

## Overview

Compute pools provide GPU and CPU resources for Snowpark Container Services.

## Configuration

```sql
CREATE COMPUTE POOL ml_pool
  MIN_NODES = 1
  MAX_NODES = 5
  INSTANCE_FAMILY = GPU_NV_S;
```

## Instance Families

| Family | vCPU | Memory | GPU | Use Case |
|--------|------|--------|-----|----------|
| CPU_X64_XS | 1 | 6 GB | — | Lightweight services |
| CPU_X64_S | 3 | 13 GB | — | Web apps |
| CPU_X64_M | 6 | 28 GB | — | Data processing |
| GPU_NV_S | 7 | 30 GB | 1x T4 | ML inference |
| GPU_NV_M | 11 | 58 GB | 1x A10G | Model training |

## Monitoring

```sql
SELECT * FROM TABLE(SYSTEM$GET_COMPUTE_POOL_STATUS('ml_pool'));
```
