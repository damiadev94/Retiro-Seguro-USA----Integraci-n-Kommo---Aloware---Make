# SOP-INF-003 Create Webhook

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-INF-003 |
| Domain | Infrastructure |
| Title | Create Webhook |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

# Purpose

Define the standard procedure for creating, configuring, and validating a webhook endpoint used to receive real-time events from external platforms.

A webhook acts as the entry point for event-driven integrations, allowing external systems to notify the integration platform whenever a business event occurs.

This SOP establishes a consistent process for implementing webhook endpoints that are secure, reliable, and reusable across integration projects.

---

# Scope

This SOP applies whenever an external system must send events to an integration platform through an HTTP webhook.

Typical webhook sources include:

- CRM platforms
- ERP systems
- E-commerce platforms
- Communication platforms
- Payment gateways
- Custom applications
- Third-party SaaS services

This procedure covers webhook creation and validation but does not include platform-specific webhook configuration.

---

# Prerequisites

Before starting, verify that:

- The integration platform is available.
- The target scenario or workflow has been created.
- The source platform supports webhooks.
- Required permissions have been granted.
- Authentication requirements have been identified.
- Naming conventions have been reviewed.

---

# Inputs

The following information may be required:

| Input | Required |
|---------|----------|
| Source Platform | Yes |
| Event(s) to Receive | Yes |
| Target Scenario | Yes |
| Authentication Method | If applicable |
| Webhook Secret | If applicable |
| Payload Specification | Recommended |
| HTTP Method | Usually POST |

---

# Procedure

## Step 1 — Identify the Business Event

Determine which event should trigger the integration.

Examples include:

- Lead Created
- Lead Updated
- Contact Updated
- Call Completed
- SMS Received
- Order Created
- Payment Successful

Each webhook should be associated with a clearly defined business event.

---

## Step 2 — Create the Webhook Endpoint

Within the integration platform:

1. Create a new webhook.
2. Associate it with the appropriate scenario or workflow.
3. Generate the webhook endpoint URL.
4. Save the configuration.

Ensure that the webhook is dedicated to a single business purpose whenever possible.

---

## Step 3 — Apply the Naming Convention

Assign a descriptive name following the organization's naming standard.

Recommended format:

```text
<Source Platform> | <Business Event>
```

Examples:

```text
Kommo | Lead Updated

Aloware | Call Completed

Stripe | Payment Succeeded
```

Avoid generic names such as:

```text
Webhook

Incoming

Receiver
```

---

## Step 4 — Configure the Source Platform

Register the generated webhook URL within the source application.

Configure:

- Endpoint URL
- HTTP Method
- Event subscriptions
- Authentication
- Retry behavior (if supported)

Verify that only the required events are subscribed.

---

## Step 5 — Configure Authentication

If the source platform supports webhook authentication:

- Configure signing secrets.
- Configure authorization headers.
- Configure shared secrets or tokens.
- Enable request signature verification if supported.

Authentication mechanisms should comply with the organization's security policies.

---

## Step 6 — Validate the Payload

Review the webhook payload specification.

Verify:

- Event structure
- Required fields
- Data types
- Identifiers
- Timestamp format
- Optional fields

Ensure the receiving workflow can process the payload correctly.

---

## Step 7 — Test Event Delivery

Trigger a test event from the source platform.

Confirm that:

- The webhook receives the request.
- The request reaches the intended workflow.
- The payload is correctly parsed.
- No processing errors occur.

If available, use the platform's webhook testing feature.

---

## Step 8 — Document the Webhook

Record the following information:

- Webhook name
- Source platform
- Business event
- Receiving workflow
- Authentication method
- Payload specification
- Environment
- Owner

Do not document sensitive credentials or secrets.

---

# Validation

The procedure is successful when:

- The webhook endpoint is active.
- Events are successfully delivered.
- Payloads are received without errors.
- Authentication succeeds (if applicable).
- The receiving workflow starts correctly.
- Event data is parsed successfully.

---

# Expected Result

A secure and operational webhook endpoint has been created and configured to receive real-time events from the source platform.

The webhook is documented, validated, and ready for production use.

---

# Common Errors

| Error | Cause | Impact |
|------|------|--------|
| Invalid webhook URL | Incorrect endpoint configuration | Events are not delivered |
| Authentication failure | Invalid secret or signature | Requests rejected |
| Incorrect subscribed events | Wrong configuration | Missing or unexpected events |
| Payload format mismatch | Different schema than expected | Processing failures |
| Duplicate event processing | No idempotency strategy | Duplicate records |

---

# Troubleshooting

| Problem | Resolution |
|----------|------------|
| No webhook requests received | Verify the endpoint URL, event subscriptions, and source platform configuration. |
| Authentication fails | Validate secrets, headers, and signature verification settings. |
| Workflow does not start | Confirm that the webhook is correctly associated with the intended workflow. |
| Payload cannot be processed | Compare the received payload with the expected schema and update mappings if necessary. |
| Duplicate events occur | Implement idempotency or event deduplication before processing. |

---

# Rollback

If the webhook was configured incorrectly:

1. Disable the webhook endpoint.
2. Remove the incorrect configuration from the source platform.
3. Create a new webhook following this SOP.
4. Update the source platform with the new endpoint.
5. Execute validation tests before reactivating the integration.

---

# Best Practices

- Create one webhook for each business event whenever practical.
- Subscribe only to the events required by the integration.
- Always validate incoming payloads.
- Implement authentication whenever supported.
- Design workflows to be idempotent.
- Log incoming webhook requests for troubleshooting.
- Monitor webhook failures and delivery statistics.
- Keep webhook documentation up to date.
- Periodically review subscribed events.

---

# References

- SOP-INF-001 — Create Make Connection
- SOP-INF-004 — Configure Error Handler
- SOP-INF-005 — Configure Retry Policy
- SOP-INF-006 — Configure Logging
- SOP-INF-008 — Naming Convention
- SOP-INF-010 — Secrets Management
- SOP Template

---

# Revision History

| Version | Date | Author | Changes |
|----------|------|--------|---------|
| 1.0 | YYYY-MM-DD | Solution Architect | Initial version |