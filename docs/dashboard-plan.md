# Power BI Dashboard Plan

## Purpose

This document outlines a generic Power BI dashboard for converting website-monitoring logs into service-performance reporting.

It is a reference design only. All targets, thresholds, review periods, metrics and example values should remain synthetic and configurable.

## Data Source

Example source:

```text
Microsoft List: Website Monitoring Log
```

Example connection method:

```text
Power BI / Power Query SharePoint Online List connector
```

## Suggested Dashboard Pages

### 1. Executive Summary

| Visual | Purpose |
|---|---|
| Availability % card | Overall availability for selected period |
| Total checks card | Monitoring volume |
| Failed checks card | Failure count |
| Outage count card | Distinct material incidents |
| Total downtime card | Estimated or calculated downtime |
| Alert count card | Notification volume |

### 2. Availability Trend

| Visual | Purpose |
|---|---|
| Availability line chart | Show availability trend over time |
| Failed checks chart | Show concentration of failures |
| Calendar heatmap | Highlight periods with more failures |

### 3. Outage and Alert Review

| Visual | Purpose |
|---|---|
| Outage table | List grouped outage events |
| Alert-state breakdown | Healthy, warning, outage, recovered |
| Alert-channel breakdown | Compare configured channels |
| Suppression count | Show transient failures that did not trigger alerts |

### 4. Response Performance

| Visual | Purpose |
|---|---|
| Average response-time trend | Show endpoint performance over time |
| Max response-time chart | Highlight spikes |
| Response-time distribution | Show stability/variance |

### 5. Data Quality

| Visual | Purpose |
|---|---|
| Missing status count | Identify incomplete records |
| Workflow failures | Separate monitoring failures from endpoint failures |
| Last successful check | Confirm monitoring freshness |

## Suggested Metrics

| Metric | Formula / Logic |
|---|---|
| Total Checks | Count of all monitoring records |
| Successful Checks | Count where `IsSuccess = Yes` |
| Failed Checks | Count where `IsSuccess = No` |
| Availability % | Successful Checks / Total Checks * 100 |
| Failure Rate % | Failed Checks / Total Checks * 100 |
| Outage Count | Count of grouped outage events |
| Alert Count | Count where `AlertSent = Yes` |
| Average Response Time | Average of `ResponseTimeMs` |
| Longest Failure Window | Maximum grouped outage duration |

Avoid hard-coding a fixed monitoring interval into downtime calculations. Prefer first-failure and recovery timestamps where available.

## Recommended Filters

- Reporting period
- Target endpoint
- Environment/classification
- Severity
- Alert state
- Alert channel
- Failure category

## Generic Review Narrative

```text
During the selected reporting period, the monitoring workflow completed <Total Checks> checks.

Overall availability was <Availability %>. There were <Failed Checks> failed checks and <Outage Count> grouped outage event(s). <Alert Count> notifications were sent.

The longest detected outage was <Duration>. Review alerting and suppression behaviour against the configured service requirements before changing thresholds.
```

## Data Preparation Notes

- Convert timestamps consistently before reporting.
- Treat `IsSuccess` as Boolean.
- Use controlled values for status/severity fields.
- Group records by `IncidentId` or outage window where available.
- Separate monitoring-platform failures from endpoint failures.
- Use synthetic/public-safe data for portfolio screenshots.

## Possible Enhancements

- Configurable service target/SLO reference line
- Incident grouping
- Period-on-period trend
- Recovery-time calculation
- Alert-suppression effectiveness
- Data-freshness indicator
- Exportable management summary

## Public Portfolio Boundary

Do not include production service targets, real domains, SLA/SLO values, internal severity definitions, actual outage statistics, recipient lists, production screenshots, incident IDs, or operational logs in public dashboard examples.