# Implementation Notes

## Current Implementation

The current implementation uses Power Automate to run a scheduled monitoring workflow. The workflow queries the target website every 5 minutes and records each result into a Microsoft List.

Email alerting is configured for major outages. The alert logic was tuned after the first version generated excessive emails during extended downtime or intermittent failures.

## Current Workflow Summary

```text
Scheduled trigger every 5 minutes
    -> Query website
    -> Evaluate response
    -> Create monitoring log item in Microsoft List
    -> Check alert threshold
    -> Send email if major outage threshold is met
```

## Existing Operational Decision

The workflow uses a 5-minute query interval because the monitoring case is aligned to a 5-minute uptime guideline.

However, alerts are not sent immediately after one failed check. A major outage alert is generated only after approximately 15 minutes of sustained or repeated failure. This reduces alert fatigue and makes alerts more meaningful.

## Recommended Power Automate Structure

### Trigger

Use a scheduled cloud flow recurrence trigger.

Recommended settings:

| Setting | Value |
|---|---|
| Frequency | Minute |
| Interval | 5 |
| Time zone | Set explicitly based on operational reporting requirement |

### Website Query

Use an HTTP action or equivalent connector/action to perform a website availability query.

Capture where possible:

- Status code
- Response time
- Error message
- Timeout result
- Timestamp

### Logging

Use the SharePoint / Microsoft Lists `Create item` action to store the result.

Each run should create a log item even if the website is healthy. This is important because uptime reporting requires successful checks as well as failed checks.

### Alert Evaluation

Use condition logic to decide whether to send an alert.

Recommended control points:

- Is the latest check successful?
- How many consecutive failures have occurred?
- When did the current failure window begin?
- Has an alert already been sent for this outage?
- Should the alert be suppressed?
- Has the website recovered?

## Common Problems and Mitigations

| Problem | Cause | Mitigation |
|---|---|---|
| Too many email alerts | Alert sent on every failed query | Add alert state and suppression logic |
| False outage alerts | One-off timeout or transient network issue | Require repeated failures before major alert |
| Hard to calculate uptime | Only failed checks are logged | Log every check, including successful checks |
| Duplicate incident count | Each failed check treated as separate incident | Use an `IncidentId` or failure window grouping |
| Difficult Power BI reporting | Inconsistent list values | Use choice fields and fixed values |
| Unclear root cause | Error messages not captured | Store sanitized failure category and error text |

## Recommended Alert State Fields

To improve reliability, add the following fields to the Microsoft List or maintain a separate state-tracking list:

| Field | Purpose |
|---|---|
| AlertState | Healthy, Warning, Major Outage, Recovered |
| ConsecutiveFailureCount | Determines if failure is transient or sustained |
| FirstFailedTimestamp | Marks start of current failure window |
| LastAlertTimestamp | Supports suppression of duplicate alerts |
| IncidentId | Groups checks that belong to the same outage |
| RecoveryTimestamp | Supports outage duration calculation |

## Suggested State List

For cleaner alert management, consider using a separate Microsoft List:

```text
Website Monitoring State
```

Suggested columns:

| Column | Purpose |
|---|---|
| TargetName | Website or endpoint name |
| TargetUrl | Website URL |
| CurrentState | Healthy, Warning, Major Outage |
| CurrentIncidentId | Active incident reference |
| FirstFailedTimestamp | Start of current failure window |
| LastCheckTimestamp | Most recent check time |
| LastAlertTimestamp | Most recent alert sent time |
| ConsecutiveFailureCount | Current failure streak |
| ConsecutiveSuccessCount | Current recovery streak |

This avoids repeatedly scanning the full log list to determine current status.

## Power BI Implementation Notes

When connecting Power BI to the Microsoft List:

- Use the SharePoint Online List connector.
- Prefer fixed column names and stable choice values.
- Consider using the 2.0 connector implementation where suitable.
- Transform timestamp fields carefully.
- Avoid using free-text fields as slicers.
- Group failed checks into outage events rather than counting every failed check as one incident.

## Teams Alerting Considerations

Teams alerting is useful for operational visibility, but it should not simply replicate every email alert.

Recommended Teams use cases:

- Post major outage notification into an IT operations channel.
- Post recovery notification into the same thread or channel.
- Include key fields only: website, status, start time, duration, latest error, action required.
- Avoid sending every 5-minute failure as a Teams message.

## Maintenance Considerations

- Review alert thresholds monthly.
- Review false positives and suppressed alerts.
- Confirm the Power Automate flow owner and backup owner.
- Confirm connector permissions and service account approach.
- Periodically test alerting logic.
- Ensure the Microsoft List does not grow without retention planning.
- Export or archive older logs if volume grows.

## Portfolio Documentation Boundaries

Do not publish:

- Internal mailbox names
- Tenant IDs
- Flow IDs
- Full production screenshots
- Internal incident channels
- Credentials or API keys
- Detailed system routing
- Sensitive error response content

Acceptable to publish:

- Sanitized architecture
- Generic workflow logic
- Public website monitoring concept
- Non-sensitive thresholds
- Example data model
- Sanitized sample data
- High-level dashboard plan