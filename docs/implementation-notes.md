# Implementation Notes

## Scope

These notes describe a **generic reference implementation** for website availability monitoring with Microsoft Power Automate and Microsoft Lists. They are intentionally detached from any production environment, employer, client, internal standard, or confidential operating process.

## Reference Workflow

```text
Scheduled trigger
    -> Query example public endpoint
    -> Evaluate response
    -> Create monitoring log item in Microsoft List
    -> Check configurable alert threshold
    -> Send notification if threshold is met
```

An illustrative example might use a 5-minute query interval and alert after three consecutive failed checks. Those values are demonstration settings only; real thresholds should be selected from service criticality, recovery objectives, false-positive tolerance, cost, and response capability.

## Recommended Power Automate Structure

### Trigger

Use a scheduled cloud-flow recurrence trigger and set the time zone explicitly.

### Website Query

Use an HTTP action or equivalent connector to perform an availability query against a non-sensitive target.

Capture where appropriate:

- status code;
- response time;
- sanitized error category;
- timeout result; and
- timestamp.

### Logging

Use Microsoft Lists or another approved data store to record each run. Logging both healthy and failed checks enables availability calculations and helps distinguish outages from isolated failures.

### Alert Evaluation

Useful control points include:

- Is the latest check successful?
- How many consecutive failures have occurred?
- When did the current failure window begin?
- Has an alert already been sent for this outage?
- Should duplicate alerts be suppressed?
- Has the service recovered?

## Common Problems and Mitigations

| Problem | Cause | Generic mitigation |
|---|---|---|
| Too many alerts | Alert generated on every failed query | Track alert state and suppress duplicates |
| False outage alerts | One-off timeout or transient issue | Require repeated failures before escalation |
| Poor uptime calculation | Only failures are logged | Log every check consistently |
| Duplicate incident count | Each failed check treated as separate incident | Group failures into an incident window |
| Difficult reporting | Inconsistent field values | Use stable schemas and controlled values |
| Sensitive error leakage | Raw response content stored | Keep only sanitized diagnostic categories |

## Example State Fields

A separate state record can contain:

| Field | Purpose |
|---|---|
| TargetName | Generic endpoint label |
| TargetUrl | Public endpoint URL |
| CurrentState | Healthy, Warning, Outage |
| CurrentIncidentId | Active incident reference |
| FirstFailedTimestamp | Start of current failure window |
| LastCheckTimestamp | Most recent check |
| LastAlertTimestamp | Most recent notification |
| ConsecutiveFailureCount | Current failure streak |
| ConsecutiveSuccessCount | Recovery streak |

This keeps current-state evaluation separate from the append-only historical log.

## Reporting Considerations

When connecting Power BI to the monitoring dataset:

- keep field names stable;
- transform timestamps consistently;
- use controlled values for status/severity;
- group failed checks into outage events rather than treating each failure as a separate incident; and
- avoid exposing sensitive error text or operational identifiers in shared reports.

## Notification Considerations

Email or Teams notifications should contain only the information needed to validate and respond to the availability issue. Avoid duplicating every failed check across multiple channels.

A generic alert might include:

- endpoint label;
- current status;
- first failed timestamp;
- failure duration;
- latest sanitized error category; and
- a generic action such as “validate availability and begin triage if confirmed.”

## Maintenance Considerations

- periodically review thresholds and false positives;
- verify flow ownership and continuity arrangements;
- review connector permissions;
- test alerting and recovery logic;
- define log-retention limits; and
- ensure example or portfolio material remains synthetic and non-sensitive.

## Public Portfolio Boundary

Do not publish:

- employer or client names/domains;
- internal standards or SLA/SLO values;
- tenant, subscription, flow, connector, mailbox or channel identifiers;
- credentials, keys, tokens or service-account details;
- production screenshots or logs;
- internal escalation paths; or
- sensitive error/incident data.

Safe portfolio content should use generic architecture, synthetic data, placeholder endpoints such as `example.com`, and clearly illustrative thresholds.