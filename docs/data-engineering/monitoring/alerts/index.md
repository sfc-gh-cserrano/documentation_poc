---
icon: material/bell-alert
title: Alerts
---

# :material-bell-alert: Alerts

## Configured Alerts

| Alert | Condition | Action |
|-------|-----------|--------|
| Pipeline Failure | Task error state | Slack + PagerDuty |
| Data Freshness | Lag > 4 hours | Slack notification |
| Credit Spike | Usage > 2x baseline | Email to team |
| Query Timeout | Duration > 30 min | Auto-cancel + alert |

## Related Pages

- [Configuring Alerts](configuring.md) — Step-by-step alert creation guide
- [Alert Runbook](runbook.md) — SOPs when alerts fire

```sql
CREATE ALERT pipeline_failure_alert
  WAREHOUSE = monitoring_wh
  SCHEDULE = '5 MINUTE'
  IF (EXISTS (
    SELECT 1
    FROM TABLE(INFORMATION_SCHEMA.TASK_HISTORY())
    WHERE STATE = 'FAILED'
      AND COMPLETED_TIME > DATEADD('MINUTE', -10, CURRENT_TIMESTAMP())
  ))
  THEN
    CALL SYSTEM$SEND_EMAIL(
      'ops_notifications',
      'oncall@acme.com',
      'Pipeline Failure Detected',
      'A task has failed in the last 10 minutes. Check TASK_HISTORY for details.'
    );
```
