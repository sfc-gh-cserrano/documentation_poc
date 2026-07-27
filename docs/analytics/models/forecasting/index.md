---
icon: material/chart-timeline-variant
title: Forecasting
---

# :material-chart-timeline-variant: Forecasting

## Active Models

| Model | Target | Horizon | Refresh | Accuracy (MAPE) |
|-------|--------|---------|---------|-----------------|
| Revenue Forecast | Monthly revenue | 12 months | Weekly | 4.2% |
| Demand Planning | Daily orders | 30 days | Daily | 6.8% |
| Capacity Planning | Compute credits | 7 days | Daily | 3.1% |

## Snowflake ML Forecasting

```sql
CREATE SNOWFLAKE.ML.FORECAST revenue_model(
  INPUT_DATA => TABLE(training_data_view),
  TIMESTAMP_COLNAME => 'ds',
  TARGET_COLNAME => 'revenue',
  SERIES_COLNAME => 'region'
);

-- Generate predictions
CALL revenue_model!FORECAST(
  FORECASTING_PERIODS => 12,
  CONFIG_OBJECT => {'prediction_interval': 0.95}
);
```

## Model Registry

```sql
SELECT *
FROM MODEL_REGISTRY.MODELS
WHERE STATUS = 'ACTIVE'
ORDER BY LAST_TRAINED DESC;
```
