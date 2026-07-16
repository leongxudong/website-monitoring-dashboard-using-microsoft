# Power BI Dashboard Plan

## Purpose

The planned Power BI dashboard will turn Microsoft List monitoring logs into monthly service performance reporting.

The dashboard should help answer:

- Was the website generally available during the month?
- How many checks failed?
- Were there sustained outages or only transient failures?
- How many alerts were sent?
- Did alert tuning reduce unnecessary noise?
- Are website response times trending upward?

## Data Source

Primary data source:

```text
Microsoft List: Website Monitoring Log
```

Planned connection method:

```text
Power BI / Power Query SharePoint Online List connector
```

## Suggested Dashboard Pages

### 1. Executive Summary

| Visual | Purpose |
|---|---|
| Availability % card | Shows overall monthly uptime |
| Total checks card | Shows monitoring volume |
| Failed checks card | Shows failure count |
| Major outage count card | Shows material incidents |
| Total downtime minutes card | Shows estimated downtime |
| Alert count card | Shows notification volume |

### 2. Availability Trend

| Visual | Purpose |
|---|---|
| Daily availability line chart | Shows availability trend by day |
| Failed checks column chart | Shows concentration of failures |
| Calendar heatmap | Highlights outage-heavy dates |

### 3. Outage and Alert Review

| Visual | Purpose |
|---|---|
| Outage table | Lists major outage events |
| Alert state breakdown | Shows healthy, warning, major outage, recovered states |
| Alert channel breakdown | Compares email vs Teams once Teams is added |
| Suppression count | Shows how many transient failures did not trigger alerts |

### 4. Response Performance

| Visual | Purpose |
|---|---|
| Average response time trend | Shows website performance over time |
| Max response time chart | Highlights spikes |
| Response time distribution | Shows whether performance is stable or variable |

### 5. Data Quality and Operations

| Visual | Purpose |
|---|---|
| Missing HTTP status count | Identifies incomplete logs |
| Flow run failures | Tracks monitoring workflow issues |
| Last successful check | Confirms current monitoring freshness |

## Suggested Metrics

| Metric | Formula / Logic |
|---|---|
| Total Checks | Count of all list items |
| Successful Checks | Count where `IsSuccess = Yes` |
| Failed Checks | Count where `IsSuccess = No` |
| Availability % | Successful Checks / Total Checks * 100 |
| Failure Rate % | Failed Checks / Total Checks * 100 |
| Estimated Downtime Minutes | Failed Checks * 5 |
| Major Outage Count | Count where `AlertState = Major Outage` |
| Alert Count | Count where `AlertSent = Yes` |
| Average Response Time | Average of `ResponseTimeMs` |
| Longest Failure Window | Max of grouped outage duration |

## Recommended Filters

- Month
- Week
- Day
- Target website
- Environment
- Severity
- Alert state
- Alert channel
- Failure category

## Monthly Performance Review Narrative

A monthly reporting summary can use this format:

```text
During the reporting month, the website monitoring workflow completed <Total Checks> checks at 5-minute intervals.

Overall availability was <Availability %>. There were <Failed Checks> failed checks, of which <Major Outage Count> met the major outage threshold. <Alert Count> alert notifications were sent.

The longest detected outage was <Duration>. Most failures were classified as <Failure Category>. Alert tuning helped suppress short transient failures and reduce unnecessary email notifications.
```

## Suggested Dashboard Layout

```text
Page 1: Executive Summary
- Availability %
- Total checks
- Failed checks
- Estimated downtime
- Major outage count
- Alert count

Page 2: Availability Trend
- Availability by day
- Failed checks by day
- Outage timeline

Page 3: Alert Quality
- Alerts sent
- Suppressed transient failures
- Alert state distribution
- False positives, if tagged

Page 4: Response Performance
- Average response time
- Max response time
- Response time trend
```

## Data Preparation Notes

- Convert `CheckTimestamp` to the correct local time zone before reporting.
- Ensure `IsSuccess` is consistently treated as Boolean.
- Use fixed choice values for `Severity`, `AlertState`, and `FailureCategory`.
- Group records by `IncidentId` where available.
- Avoid treating every failed check as a separate incident.
- Separate monitoring workflow failures from actual website failures.

## Future Dashboard Enhancements

- Add SLA / uptime target line.
- Add incident grouping logic.
- Add month-on-month trend.
- Add recovery time calculation.
- Add alert suppression effectiveness metric.
- Add Teams alert acknowledgement tracking.
- Add data freshness indicator.
- Add exportable monthly management summary.