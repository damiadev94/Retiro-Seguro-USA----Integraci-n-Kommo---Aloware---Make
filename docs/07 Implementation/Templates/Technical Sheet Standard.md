# <Scenario ID> – <Scenario Name>

# Technical Sheet

---

# Metadata

| Property | Value |
|----------|-------|
| Scenario ID | <SXX> |
| Name | <Scenario Name> |
| Category | <Infrastructure / Business / Utility> |
| Phase | Implementation |
| Version | <1.0> |
| Status | <Draft / Planned / In Progress / Completed> |
| Priority | <Critical / High / Medium / Low> |
| Owner | <Owner> |
| Last Updated | <YYYY-MM-DD> |

---

# 1. Purpose

## Objective

> Describe the primary objective of the scenario.
>
> Explain why the scenario exists and what business capability it provides.
>
> Do not describe implementation details.

---

# 2. Business Capability

> Describe the business capability implemented by this scenario.
>
> Example:
>
> - Lead Synchronization
> - Contact Synchronization
> - Communication Synchronization
> - Infrastructure Management

---

# 3. Description

> Provide a high-level functional description.
>
> Explain:
>
> - What the scenario does.
> - Why it exists.
> - How it participates in the integration.
>
> Avoid implementation details.

---

# 4. Responsibilities

## Responsible For

> List the responsibilities owned by this scenario.

Example:

- <Responsibility 1>
- <Responsibility 2>
- <Responsibility 3>

---

## Not Responsible For

> Explicitly define the responsibilities outside the scope of this scenario.

Example:

- <Out of Scope 1>
- <Out of Scope 2>
- <Out of Scope 3>

---

# 5. Scope

Describe the functional scope.

Include:

- <Scope Item>
- <Scope Item>
- <Scope Item>

Do not include implementation steps.

---

# 6. Trigger

## Type

<Select one>

- Manual
- Webhook
- Scheduled
- API
- Event
- Internal

---

## Execution

Describe when and under which conditions the scenario executes.

---

# 7. Source System

Specify the system that originates the event.

Example:

- Kommo
- Aloware
- Shopify
- Stripe

---

# 8. Target System

Specify the destination system.

---

# 9. Components

Describe every logical component involved in this scenario.

For each component include:

## <Component Name>

### Purpose

<Describe the purpose>

### Responsibilities

- <Item>
- <Item>

### Dependencies

- <Dependency>

Repeat as necessary.

---

# 10. Inputs

Describe every required input.

Include:

- Events
- Payloads
- Parameters
- Credentials
- Variables
- IDs

---

# 11. Outputs

Describe every expected output.

Examples:

- API Request
- Updated Contact
- Created Note
- Assigned Lead
- Notification
- Log Entry

---

# 12. Implementation Boundary

## Included

List everything that belongs to this scenario.

Example:

- <Item>
- <Item>

---

## Excluded

List everything intentionally outside this scenario.

Example:

- <Item>
- <Item>

---

# 13. Dependencies

Describe dependencies.

Examples:

- Infrastructure
- Other scenarios
- External services
- Shared resources

If none:

None.

---

# 14. Consumers

List every scenario that consumes the outputs produced here.

Example:

- S02
- Reporting
- Monitoring

If none:

None.

---

# 15. Preconditions

Describe every condition that must already be true before execution.

Example:

- Credentials available.
- Webhooks configured.
- Shared configuration loaded.

---

# 16. Postconditions

Describe the expected system state after successful execution.

---

# 17. Technical Constraints

Document implementation restrictions.

Examples:

- API limits
- Authentication requirements
- Timeout restrictions
- Payload size
- Rate Limits
- Idempotency

---

# 18. Error Handling Strategy

Describe how failures should be handled.

Include:

- Retry
- Abort
- Ignore
- Escalation
- Logging
- Notifications

---

# 19. Monitoring

Describe how this scenario should be monitored.

Include:

- Health Checks
- Logs
- Metrics
- Alerts
- Dashboards

---

# 20. Related Documentation

## Project Documentation

- <Document>

---

## Architecture

- <Document>

---

## Scenario Documentation

- Implementation Design
- Build Checklist
- Runbook
- Testing

---

# 21. Acceptance Criteria

Describe the conditions required to consider the scenario complete.

Example:

- Requirement satisfied.
- Validation completed.
- No Critical Issues.
- Approved for Production.