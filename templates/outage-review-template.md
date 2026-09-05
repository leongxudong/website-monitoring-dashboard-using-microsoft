# Outage / Monitoring Review Template

> Generic reference template only. Use synthetic examples in public copies and keep production thresholds, targets, owners, incident details and operational statistics out of this repository.

## Review Period

| Field | Value |
|---|---|
| Period | `<Month / Date Range>` |
| Reviewed by | `<Generic Role>` |
| Review date | `<Date>` |
| Data source | `<Monitoring Dataset>` |

## Executive Summary

```text
During the review period, the monitoring workflow completed <Total Checks> checks.

Overall availability was <Availability %>. There were <Failed Checks> failed checks and <Outage Count> grouped outage event(s). <Alert Count> notification(s) were generated.

The most significant synthetic/example issue lasted approximately <Duration>. Alerting behaviour was assessed as <Effective / Needs Tuning> against the configured reference threshold.
```

## Review Metrics

| Metric | Value |
|---|---:|
| Total checks |  |
| Successful checks |  |
| Failed checks |  |
| Availability % |  |
| Calculated downtime |  |
| Outage count |  |
| Intermittent failure count |  |
| Alerts sent |  |
| Suppressed transient failures |  |
| False positives |  |
| Average response time |  |
| Maximum response time |  |

## Outage Events

| Incident ID | Start Time | Recovery Time | Duration | Severity | Alert Sent | Notes |
|---|---|---|---:|---|---|---|
| `<SYNTHETIC-ID>` |  |  |  |  |  |  |

## Alert Quality Review

| Question | Assessment |
|---|---|
| Were notifications generated only for material conditions? |  |
| Were there duplicate alerts? |  |
| Were there missed alerts? |  |
| Were transient failures correctly suppressed? |  |
| Does the configured threshold remain appropriate for the reference scenario? |  |
| Are the selected notification channels appropriate? |  |

## Root Cause / Follow-Up Notes

```text
Use synthetic or generic categories in public examples, such as hosting issue, DNS issue, certificate issue, network issue, application issue, maintenance, or false positive.
```

## Improvement Actions

| Action | Owner Role | Due Date | Status |
|---|---|---|---|
|  |  |  |  |

## Threshold Review

| Configurable Parameter | Current Example | Recommended Change | Rationale |
|---|---|---|---|
| Monitoring interval | `<Example>` |  |  |
| Alert threshold | `<Example>` |  |  |
| Recovery confirmation | `<Example>` |  |  |

## Dashboard Notes

```text
Record whether the reference visuals were accurate, whether synthetic data-quality issues were observed, and whether additional metrics would improve the generic design.
```

## Closure

| Role | Name / Placeholder | Date |
|---|---|---|
| Reviewer |  |  |
| Service owner role |  |  |
| Technical owner role |  |  |

## Public Portfolio Boundary

Never populate a public copy with real employer/client domains, internal thresholds, SLA/SLO values, actual outage dates/statistics, production incident IDs, staff names, recipient lists, confidential root-cause details, or operational screenshots.