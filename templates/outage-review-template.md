# Outage / Monitoring Review Template

## Review Period

| Field | Value |
|---|---|
| Month | `<Month Year>` |
| Reviewed by | `<Name / Role>` |
| Review date | `<Date>` |
| Data source | Microsoft List: Website Monitoring Log |

## Executive Summary

```text
During the review period, the website monitoring workflow completed <Total Checks> checks.

Overall availability was <Availability %>. There were <Failed Checks> failed checks and <Major Outage Count> major outage event(s). <Alert Count> alert(s) were sent.

The most significant issue occurred on <Date>, lasting approximately <Duration>. Alerting behaviour was assessed as <Effective / Needs Tuning>.
```

## Monthly Metrics

| Metric | Value |
|---|---:|
| Total checks |  |
| Successful checks |  |
| Failed checks |  |
| Availability % |  |
| Estimated downtime minutes |  |
| Major outage count |  |
| Intermittent failure count |  |
| Alerts sent |  |
| Suppressed transient failures |  |
| False positives |  |
| Average response time |  |
| Maximum response time |  |

## Outage Events

| Incident ID | Start Time | Recovery Time | Duration | Severity | Alert Sent | Notes |
|---|---|---|---:|---|---|---|
|  |  |  |  |  |  |  |

## Alert Quality Review

| Question | Assessment |
|---|---|
| Were alerts sent only for material issues? |  |
| Were there duplicate alerts? |  |
| Were there missed alerts? |  |
| Were transient failures correctly suppressed? |  |
| Should the 15-minute threshold be adjusted? |  |
| Should Teams alerting be added or changed? |  |

## Root Cause / Follow-Up Notes

```text
Document any known causes, such as hosting issue, DNS issue, certificate issue, network issue, application issue, planned maintenance, or false positive.
```

## Improvement Actions

| Action | Owner | Due Date | Status |
|---|---|---|---|
|  |  |  |  |

## Threshold Review

| Current Threshold | Recommended Change | Rationale |
|---|---|---|
| 5-minute monitoring interval |  |  |
| 15-minute major outage alert threshold |  |  |

## Dashboard Notes

```text
Record whether Power BI visuals were accurate, whether data quality issues were observed, and whether additional metrics are needed for management reporting.
```

## Approval / Closure

| Role | Name | Date |
|---|---|---|
| Reviewer |  |  |
| Service owner |  |  |
| IT owner |  |  |