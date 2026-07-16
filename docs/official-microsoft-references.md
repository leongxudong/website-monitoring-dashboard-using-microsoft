# Official Microsoft References

This page collects official Microsoft references that support the technologies used in this project.

The screenshots below are externally referenced from Microsoft Learn. They are not copied into this repository. Replace them with sanitized internal screenshots if this repository is adapted into internal documentation.

## Power Automate Scheduled Cloud Flow

Microsoft Learn documents scheduled cloud flows for tasks that need to run at a defined interval.

Reference:

- https://learn.microsoft.com/en-us/power-automate/run-scheduled-tasks

Official Microsoft Learn screenshot:

![Microsoft Learn screenshot: Build a scheduled cloud flow](https://learn.microsoft.com/en-us/power-automate/media/run-scheduled-tasks/select-recurrence-aa.png)

Project relevance:

- Used to run website checks every 5 minutes.
- Supports recurring monitoring workflow design.
- Forms the trigger layer of the monitoring architecture.

## SharePoint / Microsoft Lists Connector

Microsoft Learn documents the SharePoint connector used by Power Automate to work with SharePoint and list items.

Reference:

- https://learn.microsoft.com/en-us/connectors/sharepointonline/

Project relevance:

- Used to create monitoring log items.
- Supports storing structured query results in a Microsoft List.
- Provides the data source later used for reporting.

## Power BI / Power Query SharePoint Online List Connector

Microsoft Learn documents the SharePoint Online List connector for Power Query, including use with Power BI.

Reference:

- https://learn.microsoft.com/en-us/power-query/connectors/sharepoint-online-list

Official Microsoft Learn screenshot:

![Microsoft Learn screenshot: SharePoint Online Lists connector dialog](https://learn.microsoft.com/en-us/power-query/connectors/media/sharepoint-online-list/sharepoint-online-list-url.png)

Project relevance:

- Planned approach for connecting Microsoft List monitoring logs into Power BI.
- Supports the monthly performance review dashboard.
- Enables analysis of uptime, failure rate, alert count, and response time trends.

## Power Automate Email Notification

Microsoft Learn documents Power Automate email scenarios, including sending email through Outlook actions and using dynamic content in the body.

Reference:

- https://learn.microsoft.com/en-us/power-automate/email-top-scenarios

Official Microsoft Learn screenshot:

![Microsoft Learn screenshot: Power Automate Send an email V2 with dynamic content](https://learn.microsoft.com/en-us/power-automate/media/email/dynamic-content.png)

Project relevance:

- Used for major outage notification.
- Supports dynamic alert content such as website name, timestamp, status, and duration.

## Microsoft Teams Connector

Microsoft Learn documents the Microsoft Teams connector for Power Automate, including actions for posting messages in chats or channels.

Reference:

- https://learn.microsoft.com/en-us/connectors/teams/

Project relevance:

- Planned enhancement for channel-based website outage alerts.
- Useful for operational visibility and incident collaboration.
- Should be tuned to avoid duplicating every email notification.

## Notes on Use of Official Screenshots

The screenshot links above are hosted by Microsoft Learn and are used only as references to the Microsoft product interface. They should not be treated as screenshots of this project implementation.

For an internal implementation record, replace them with sanitized screenshots of:

1. The scheduled Power Automate trigger.
2. The website query action.
3. The Microsoft List logging action.
4. The alert condition block.
5. The email or Teams notification action.
6. The Power BI dashboard once built.

Before publishing implementation screenshots, remove or mask:

- Tenant identifiers
- Internal site names not intended for disclosure
- Email addresses
- Flow IDs
- List IDs
- Channel names
- Access tokens, secrets, or API keys
- Internal error messages