# SOP-MAKE-002 Configure Trigger

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-MAKE-002 |
| Domain | Make |
| Title | Configure Trigger |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

# Purpose

Define the standard procedure for configuring workflow triggers in Make.

The trigger is the entry point of every scenario and determines when and how the workflow begins. A properly configured trigger ensures reliable execution, minimizes unnecessary operations, and provides predictable workflow behavior.

This SOP standardizes trigger configuration for all Make scenarios.

---

# Scope

This SOP applies whenever a Make scenario requires a trigger to initiate execution.

Typical trigger types include:

- Webhooks
- Scheduled execution
- Instant events
- Polling modules
- Email triggers
- Queue listeners
- File monitoring
- HTTP requests
- Platform-specific event listeners

This SOP focuses exclusively on trigger configuration and does not cover downstream workflow implementation.

---

# Prerequisites

Before starting, verify that:

- The scenario has been created.
- Required platform connections are available.
- Business events have been identified.
- Trigger requirements have been documented.
- Authentication has been configured when required.

---

# Inputs

The following information may be required:

| Input | Required |
|---------|----------|
| Integration Design | Yes |
| Trigger Type | Yes |
| Source Platform | Yes |
| Connection | Recommended |
| Business Event | Recommended |

---

# Procedure

## Step 1 — Identify the Trigger Event

Determine which business event should start the workflow.

Examples include:

- Contact created
- Lead updated
- Call completed
- File uploaded
- Scheduled synchronization
- HTTP request received
- Email received

Every scenario should have a clearly defined triggering event.

---

## Step 2 — Select the Appropriate Trigger Type

Choose the trigger mechanism that best matches the business event.

Typical options include:

### Instant Triggers

Workflow starts immediately after an external event occurs.

Examples:

- Webhooks
- Instant CRM events
- Messaging events

---

### Scheduled Triggers

Workflow executes according to a defined schedule.

Examples:

- Every hour
- Daily
- Weekly
- Monthly
- Custom intervals

---

### Polling Triggers

Workflow periodically checks for new or updated information.

Examples:

- Watch Records
- Watch Files
- Watch Emails
- Watch Orders

Polling should only be used when instant events are unavailable.

---

## Step 3 — Configure the Connection

Associate the trigger with the appropriate platform connection.

Verify:

- Authentication
- Permissions
- Environment
- Account
- API access

The trigger should always use an approved connection.

---

## Step 4 — Configure Trigger Parameters

Configure the settings required by the selected trigger.

Typical parameters include:

- Event type
- Resource
- Folder
- Object type
- Pipeline
- Date filter
- Update window
- Search criteria

Configure only the parameters required by the business process.

---

## Step 5 — Configure Initial Filters

When supported by the trigger, configure filters to reduce unnecessary executions.

Examples include:

- Record status
- Event type
- Object category
- Date range
- Custom fields

Filtering at the trigger level improves workflow efficiency.

---

## Step 6 — Validate Trigger Connectivity

Verify that the trigger can successfully communicate with the source platform.

Confirm:

- Connection status
- Authentication
- Required permissions
- Endpoint accessibility
- Event registration

Connectivity issues should be resolved before continuing.

---

## Step 7 — Execute a Test Trigger

Generate a test event or wait for a natural event to occur.

Verify that:

- The scenario starts.
- Input data is received.
- Required fields are available.
- Trigger metadata is correct.

Testing should confirm that the workflow starts under the expected conditions.

---

## Step 8 — Validate the Received Data

Inspect the incoming payload.

Verify:

- Required fields exist.
- Data types are correct.
- Event metadata is complete.
- Payload structure matches documentation.

Unexpected payload structures should be investigated before implementation continues.

---

## Step 9 — Document the Trigger

Record the trigger configuration.

Document:

- Trigger type
- Source platform
- Business event
- Connection
- Filters
- Scheduling configuration (if applicable)
- Dependencies

Documentation should allow the trigger to be reproduced without additional investigation.

---

# Validation

The procedure is considered successful when:

- The correct trigger type is configured.
- Authentication succeeds.
- The trigger receives valid events.
- Required data is available.
- The scenario starts correctly.
- Trigger configuration has been documented.

---

# Expected Result

A reliable trigger is configured and validated, allowing the scenario to begin execution automatically whenever the defined business event occurs.

---

# Common Errors

| Error | Cause | Impact |
|------|------|--------|
| Incorrect trigger selected | Business requirements misunderstood | Workflow executes incorrectly |
| Missing permissions | Connection not authorized | Trigger cannot start |
| Polling configured unnecessarily | Instant trigger available | Increased API consumption |
| Trigger receives excessive events | Missing filters | Unnecessary workflow executions |
| Payload differs from expectations | Incorrect event configuration | Downstream processing failures |

---

# Troubleshooting

| Problem | Resolution |
|----------|------------|
| Trigger never starts | Verify the event configuration, connection, and required permissions. |
| Scenario executes too frequently | Review trigger filters and scheduling configuration. |
| Payload is incomplete | Confirm that the correct event type and resource are configured. |
| Authentication fails | Reauthorize the platform connection and verify credentials. |
| Duplicate executions occur | Review trigger conditions and implement deduplication where appropriate. |

---

# Rollback

If the trigger configuration causes operational issues:

1. Disable the scenario.
2. Remove the incorrect trigger configuration.
3. Restore the previous validated configuration.
4. Verify connectivity.
5. Execute controlled testing before returning to production.

---

# Best Practices

- Select the simplest trigger that satisfies the business requirement.
- Prefer instant triggers over polling whenever available.
- Configure trigger-level filters to reduce unnecessary executions.
- Validate incoming payloads before implementing downstream logic.
- Use dedicated connections for production environments.
- Document every trigger configuration.
- Keep trigger configuration independent of business processing.
- Test triggers using representative business events.
- Avoid unnecessary polling intervals.
- Review trigger performance periodically.

---

# References

- SOP-MAKE-001 — Create Scenario
- SOP-MAKE-003 — Configure Router
- SOP-MAKE-004 — Configure Filters
- SOP-MAKE-007 — Configure Scheduling
- SOP-MAKE-009 — Test Scenario
- SOP-HTTP-001 — Create HTTP Request
- SOP-INF-001 — Create Make Connection
- SOP Template
- Integration Documentation Framework

---

# Revision History

| Version | Date | Author | Changes |
|----------|------|--------|---------|
| 1.0 | YYYY-MM-DD | Solution Architect | Initial version |