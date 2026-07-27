---
icon: material/tag-multiple
title: Classification
---

# :material-tag-multiple: Classification

## Active Models

| Model | Task | Features | F1 Score |
|-------|------|----------|----------|
| Churn Predictor | Binary classification | 42 | 0.87 |
| Lead Scoring | Multi-class | 28 | 0.79 |
| Ticket Router | Multi-class | 15 | 0.91 |
| Fraud Detection | Binary classification | 65 | 0.94 |

## Example: Snowflake ML Classification

```sql
CREATE SNOWFLAKE.ML.CLASSIFICATION churn_model(
  INPUT_DATA => TABLE(churn_training_view),
  TARGET_COLNAME => 'is_churned'
);

-- Score new customers
SELECT
  customer_id,
  churn_model!PREDICT(INPUT_DATA => OBJECT_CONSTRUCT(*)) AS prediction
FROM curated.active_customers;
```

## Feature Importance

| Rank | Feature | Importance |
|------|---------|------------|
| 1 | days_since_last_login | 0.23 |
| 2 | support_tickets_30d | 0.18 |
| 3 | usage_trend_slope | 0.15 |
| 4 | contract_months_remaining | 0.12 |
| 5 | feature_adoption_pct | 0.09 |
