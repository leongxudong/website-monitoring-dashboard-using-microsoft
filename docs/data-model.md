# Microsoft List Data Model

## Purpose

The Microsoft List acts as a generic monitoring log store. Each scheduled website query creates one list item so availability checks can be reviewed, filtered, exported, and used for reporting.

This is a reference schema only. Do not use employer/client system names, production URLs, operational identifiers, or sensitive response data in public examples.

## Recommended List Name

```text
Website Monitoring Log
```

Use a neutral name and synthetic example data.

## Recommended Columns

| Column Name | Type | Required | Purpose |
|---|---|---:|---|
| Title | Single line of text | Yes | Human-readable record title, e.g. `Example Website - 2026-07-16 09:00` |
| CheckTimestamp | Date and time | Yes | Date and time of the monitoring query |
| TargetName | Single line of text | Yes | Generic name of monitored endpoint |
| TargetUrl | Hyperlink or single line of text | Yes | Example/public endpoint URL |
| Environment | Choice | No | Lab, test, production-like, or other generic value |
| HttpStatusCode | Number | No | HTTP response status, where available |
| IsSuccess | Yes/No | Yes | Whether the check was successful |
| ResponseTimeMs | Number | No | Response time in milliseconds, if captured |
| FailureCategory | Choice | No | Timeout, DNS, HTTP error, connection refused, content mismatch, unknown |
| ErrorMessage | Multiple lines of text | No | Sanitized error category/text only |
| ConsecutiveFailureCount | Number | No | Count of back-to-back failed checks |
| FirstFailedTimestamp | Date and time | No | Start time of current failure window |
| FailureDurationMinutes | Number | No | Duration since first failed check |
| Severity | Choice | Yes | Informational, Low, Medium, High, Critical |
| Sensitivity | Choice | No | Public informational, business important, critical service |
| AlertRequired | Yes/No | Yes | Whether this check requires notification |
| AlertSent | Yes/No | Yes | Whether an alert was sent |
| AlertChannel | Choice | No | None, Email, Teams, Email and Teams |
| AlertState | Choice | No | Healthy, Warning, Outage, Recovered |
| IncidentId | Single line of text | No | Generic identifier for grouping related records |
| FlowRunId | Single line of text | No | Optional workflow-run identifier; do not publish real production IDs |
| Notes | Multiple lines of text | No | Sanitized review notes |

## Minimal Viable Columns

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
Outage
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

## Synthetic Example Records

| CheckTimestamp | TargetName | HttpStatusCode | IsSuccess | Severity | AlertSent | AlertState |
|---|---|---:|---|---|---|---|
| 2026-07-16 09:00 | Example Website | 200 | Yes | Informational | No | Healthy |
| 2026-07-16 09:05 | Example Website | 0 | No | Low | No | Warning |
| 2026-07-16 09:10 | Example Website | 0 | No | Medium | No | Warning |
| 2026-07-16 09:15 | Example Website | 0 | No | High | Yes | Outage |
| 2026-07-16 09:20 | Example Website | 200 | Yes | Informational | No | Recovered |

These timestamps and thresholds are synthetic and exist only to demonstrate state transitions.

## Data Quality Considerations

- Use consistent timestamps and time zones.
- Avoid storing sensitive response content.
- Use fixed choice values for fields used in reporting.
- Group records by a synthetic incident ID where needed.
- Do not expose production flow-run IDs or operational notes in a public repository.

## Example Calculations

```text
Availability % = Successful Checks / Total Checks * 100
Failure Rate % = Failed Checks / Total Checks * 100
```

Approximate downtime based on failed checks is only a rough heuristic. A better approach is to calculate outage windows from first-failure and recovery timestamps.

## Public Portfolio Boundary

Only synthetic values belong in this repository. Do not publish employer/client names, real monitored domains, internal severity models, operational IDs, production timestamps/logs, incident references, or sensitive errors.