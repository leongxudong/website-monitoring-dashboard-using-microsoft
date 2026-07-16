# Microsoft List Data Model

## Purpose

The Microsoft List acts as the monitoring log store. Each scheduled website query should create one list item so that availability checks can be reviewed, filtered, exported, and used for Power BI reporting.

## Recommended List Name

```text
Website Monitoring Log
```

Use a neutral list name. Avoid embedding sensitive internal system names if the list may later be exported or used in wider reporting.

## Recommended Columns

| Column Name | Type | Required | Purpose |
|---|---|---:|---|
| Title | Single line of text | Yes | Human-readable record title, e.g. `AWWA Website - 2026-07-16 09:00` |
| CheckTimestamp | Date and time | Yes | Date and time of the monitoring query |
| TargetName | Single line of text | Yes | Friendly name of monitored website |
| TargetUrl | Hyperlink or single line of text | Yes | Website URL being checked |
| Environment | Choice | No | Production, staging, test, or other environment |
| HttpStatusCode | Number | No | HTTP response status, where available |
| IsSuccess | Yes/No | Yes | Whether the check was successful |
| ResponseTimeMs | Number | No | Response time in milliseconds, if captured |
| FailureCategory | Choice | No | Timeout, DNS, HTTP error, connection refused, content mismatch, unknown |
| ErrorMessage | Multiple lines of text | No | Sanitized error text from failed query |
| ConsecutiveFailureCount | Number | No | Count of back-to-back failed checks |
| FirstFailedTimestamp | Date and time | No | Start time of current failure window |
| FailureDurationMinutes | Number | No | Duration since first failed check |
| Severity | Choice | Yes | Informational, Low, Medium, High, Critical |
| Sensitivity | Choice | No | Public informational, business important, critical service |
| AlertRequired | Yes/No | Yes | Whether this check requires notification |
| AlertSent | Yes/No | Yes | Whether alert was sent for this check |
| AlertChannel | Choice | No | None, Email, Teams, Email and Teams |
| AlertState | Choice | No | Healthy, Warning, Major Outage, Recovered |
| IncidentId | Single line of text | No | Identifier for grouping related outage records |
| FlowRunId | Single line of text | No | Power Automate run identifier, if captured |
| Notes | Multiple lines of text | No | Manual review notes |

## Minimal Viable Columns

If the list needs to stay simple, start with the following fields:

| Column Name | Type |
|---|---|
| CheckTimestamp | Date and time |
| TargetName | Single line of text |
| TargetUrl | Single line of text |
| HttpStatusCode | Number |
| IsSuccess | Yes/No |
| ErrorMessage | Multiple lines of text |
| Severity | Choice |
| AlertSent | Yes/No |

## Choice Field Values

### Severity

```text
Informational
Low
Medium
High
Critical
```

### FailureCategory

```text
None
Timeout
DNS
HTTP Error
Connection Error
Content Mismatch
SSL Certificate
Unknown
```

### AlertState

```text
Healthy
Warning
Major Outage
Recovered
Suppressed
```

### AlertChannel

```text
None
Email
Teams
Email and Teams
```

## Example Records

| CheckTimestamp | TargetName | HttpStatusCode | IsSuccess | Severity | AlertSent | AlertState |
|---|---|---:|---|---|---|---|
| 2026-07-16 09:00 | Public Website | 200 | Yes | Informational | No | Healthy |
| 2026-07-16 09:05 | Public Website | 0 | No | Low | No | Warning |
| 2026-07-16 09:10 | Public Website | 0 | No | Medium | No | Warning |
| 2026-07-16 09:15 | Public Website | 0 | No | High | Yes | Major Outage |
| 2026-07-16 09:20 | Public Website | 200 | Yes | Informational | No | Recovered |

## Data Quality Considerations

- Use consistent timestamps and time zones.
- Avoid storing sensitive response content.
- Store sanitized error messages only.
- Use fixed choice values for severity and alert state.
- Avoid free-text values for fields that will be used in Power BI filters.
- Capture flow run identifiers where possible to support troubleshooting.

## Power BI Readiness

For Power BI reporting, the list should support calculations such as:

- Total checks
- Successful checks
- Failed checks
- Uptime percentage
- Outage count
- Longest outage
- Average response time
- Alert count
- False positive count, if manually tagged

## Suggested Calculations

### Availability Percentage

```text
Availability % = Successful Checks / Total Checks * 100
```

### Failure Rate

```text
Failure Rate % = Failed Checks / Total Checks * 100
```

### Approximate Downtime Minutes

```text
Downtime Minutes = Failed Checks * Monitoring Interval Minutes
```

For this implementation:

```text
Downtime Minutes = Failed Checks * 5
```

This is an approximation. Actual outage duration should be calculated using the first failed timestamp and recovery timestamp where possible.