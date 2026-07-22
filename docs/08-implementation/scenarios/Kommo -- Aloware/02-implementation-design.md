# S01 – Lead Sync

# Implementation Design

---

# Metadata

| Property | Value |
|----------|-------|
| Scenario ID | S01 |
| Name | Lead Sync |
| Category | Business |
| Phase | Implementation |
| Version | 1.0 |
| Status | Planned |
| Owner | Integration Team |
| Last Updated | YYYY-MM-DD |

---

# 1. Purpose

This document describes the technical implementation of the **Lead Sync** scenario.

Unlike the Technical Sheet, which defines **what** the scenario must accomplish, this document specifies **how** the scenario will be implemented within Make.

It defines the execution flow, technical components, processing stages, validations, transformations, integrations and operational behavior.

---

# 2. Implementation Overview

The scenario synchronizes business leads from Kommo into Aloware.

Execution begins after Kommo generates a business event indicating that a lead is ready for outbound communication.

The scenario validates the event, retrieves the complete business information, transforms the data into the Aloware model, creates or updates the contact, assigns the outbound sequence and persists the generated Aloware Contact ID back into Kommo.

---

# 3. Implementation Architecture

```text
                Kommo
                  │
                  │
          Lead Updated Webhook
                  │
                  ▼
              Make Scenario
                  │
        ┌─────────┴─────────┐
        │                   │
 Validate Event      Load Lead Details
        │                   │
        └─────────┬─────────┘
                  │
          Business Validation
                  │
                  ▼
          Data Transformation
                  │
                  ▼
           Owner Mapping
                  │
                  ▼
     Search Existing Contact
          │              │
          │              │
     Exists?           Not Found
          │              │
          ▼              ▼
 Update Contact     Create Contact
          └──────┬───────┘
                 ▼
        Assign Sequence
                 │
                 ▼
 Update Kommo Contact ID
                 │
                 ▼
          Execution Logging
                 │
                 ▼
              Completed
```

---

# 4. Execution Flow

The scenario is executed sequentially.

## Stage 1 – Receive Event

Receive webhook notification from Kommo.

Outputs:

- Lead ID
- Pipeline
- Stage
- Event Metadata

---

## Stage 2 – Retrieve Business Data

Retrieve complete business entities.

Objects:

- Lead
- Contact
- Company (if applicable)
- Responsible User
- Custom Fields

---

## Stage 3 – Business Validation

Validate whether synchronization should continue.

Validations include:

- Stage eligible
- Phone available
- Lead active
- Required fields present
- Mapping available

Failure terminates execution.

---

## Stage 4 – Data Transformation

Transform Kommo entities into the Aloware data model.

Activities include:

- Normalize phone numbers
- Normalize names
- Prepare payload
- Resolve configuration IDs

---

## Stage 5 – Owner Mapping

Determine the destination Aloware Agent.

Lookup:

Responsible User

↓

Agent Mapping Table

↓

Aloware Agent ID

---

## Stage 6 – Contact Synchronization

Search contact.

Decision:

Existing Contact

↓

Update

or

Missing Contact

↓

Create

The scenario shall guarantee idempotent behavior.

---

## Stage 7 – Sequence Assignment

Assign the synchronized contact to the configured outbound sequence.

Assignment depends on:

- Pipeline
- Stage
- Business configuration

---

## Stage 8 – Reverse Synchronization

Persist generated Aloware Contact ID inside Kommo.

Purpose:

Maintain bidirectional relationship.

---

## Stage 9 – Logging

Register:

- Execution
- Success
- Failure
- API responses
- Retry attempts
- Processing time

---

# 5. Make Scenario Design

The scenario shall be implemented using the following logical modules.

| Order | Module | Purpose |
|--------|---------|----------|
| 1 | Webhook | Receive Kommo event |
| 2 | Get Lead | Retrieve Lead |
| 3 | Get Contact | Retrieve Contact |
| 4 | Validation | Validate business rules |
| 5 | Data Transformation | Build payload |
| 6 | Agent Lookup | Resolve agent |
| 7 | Search Contact | Search Aloware |
| 8 | Router | Create / Update |
| 9 | Create Contact | New contact |
| 10 | Update Contact | Existing contact |
| 11 | Assign Sequence | Assign outbound workflow |
| 12 | Update Kommo | Persist Contact ID |
| 13 | Logger | Register execution |

---

# 6. Business Decision Points

## Decision 1

Is the pipeline stage eligible?

No

↓

Terminate

---

## Decision 2

Does the lead contain a valid phone?

No

↓

Terminate

---

## Decision 3

Is an Agent Mapping available?

No

↓

Terminate

---

## Decision 4

Does the contact already exist?

Yes

↓

Update

No

↓

Create

---

## Decision 5

Was synchronization successful?

Yes

↓

Persist Contact ID

No

↓

Log Failure

---

# 7. Data Transformation Design

The following transformations shall be performed.

| Source | Target | Transformation |
|----------|----------|----------------|
| Name | Full Name | Normalize |
| Phone | Phone | International Format |
| Email | Email | Direct |
| Owner | Agent | Mapping Lookup |
| Pipeline | Sequence | Configuration Lookup |
| Stage | Sequence | Configuration Lookup |

---

# 8. API Operations

## Kommo

Operations:

- Receive Webhook
- Get Lead
- Get Contact
- Update Contact

---

## Aloware

Operations:

- Search Contact
- Create Contact
- Update Contact
- Assign Sequence

---

# 9. Error Handling Design

Recoverable Errors

- API Timeout
- Rate Limit
- Temporary Network Failure

Action

Retry.

---

Non-Recoverable Errors

- Invalid Mapping
- Missing Phone
- Authentication Failure
- Invalid Payload

Action

Abort execution.

Register detailed logs.

---

# 10. Logging Design

Each execution shall generate logs containing:

Execution

- Scenario
- Execution ID
- Timestamp

Business

- Lead ID
- Contact ID
- Agent
- Sequence

Technical

- API Requests
- API Responses
- Errors
- Retry Count
- Duration

---

# 11. Performance Considerations

Implementation shall minimize:

- API requests
- Duplicate searches
- Sequential latency

Whenever possible:

- Reuse retrieved objects.
- Avoid redundant API calls.
- Cache configuration values.

---

# 12. Security Considerations

The scenario shall never expose:

- OAuth Tokens
- API Tokens
- Credentials
- Secrets

Sensitive information shall remain inside shared connections.

---

# 13. Dependencies

Infrastructure

- S00 Infrastructure

Configuration

- Agent Mapping
- Stage Mapping
- Sequence Mapping

External

- Kommo API
- Aloware API

---

# 14. Expected Deliverables

Upon implementation, the scenario shall provide:

- Operational webhook.
- Complete synchronization workflow.
- Contact creation/update.
- Automatic sequence assignment.
- Reverse synchronization.
- Execution logging.
- Error handling.
- Retry strategy.

---

# 15. Related Documentation

## Functional

- S01 Technical Sheet

## Operational

- S01 Build Checklist
- S01 Runbook
- S01 Testing

## Architecture

- Architecture Design
- Technical Design
- Mapping Model
- Integration Flow Design

---

# 16. Acceptance Criteria

Implementation shall be considered complete when:

- Webhook receives supported events.
- Lead data is successfully retrieved.
- Business validations execute correctly.
- Data transformation is validated.
- Contact is correctly created or updated.
- Sequence assignment succeeds.
- Kommo stores the Aloware Contact ID.
- Logging captures every execution.
- Error handling behaves as designed.
- All defined test cases pass successfully.