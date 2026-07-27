---
icon: material/view-dashboard
title: Dashboards
---

# :material-view-dashboard: Dashboards

## Operational Dashboards

| Dashboard | Refresh | Audience | Tool |
|-----------|---------|----------|------|
| Pipeline Health | 5 min | Data Engineering | Streamlit |
| Credit Usage | 15 min | Finance / Ops | Sigma |
| Query Performance | 1 min | Platform Team | Grafana |
| Data Quality | 1 hour | Data Stewards | Streamlit |

## Key Metrics Tracked

- **Pipeline SLA**: % of tasks completing within target lag
- **Data Freshness**: Time since last successful load per source
- **Credit Burn Rate**: Credits/hour by warehouse and service
- **Error Rate**: Failed tasks / total tasks (rolling 24h)
- **Query Concurrency**: Active queries by warehouse over time
