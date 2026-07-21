# S02 – Communication Sync

# Implementation Design

---

# Metadata

| Property | Value |
|----------|-------|
| Scenario ID | S02 |
| Name | Communication Sync |
| Category | Business |
| Phase | Implementation |
| Version | 1.0 |
| Status | Planned |
| Owner | Integration Team |
| Last Updated | YYYY-MM-DD |

---

# 1. Purpose

This document describes the technical implementation of the **Communication Sync** scenario.

Unlike the Technical Sheet, which defines **what** the scenario must accomplish, this document specifies **how** the scenario will be implemented within Make.

It defines the execution flow, routing logic, business validations, data transformations, API interactions and operational behavior required to synchronize communication events from Aloware into Kommo.

---

# 2. Implementation Overview

The scenario synchronizes communication activities generated in Aloware into Kommo.

Execution begins whenever Aloware emits a supported communication event through a webhook.

The scenario identifies the event type, validates the payload, locates the corresponding business entity in Kommo, formats the communication into a standardized Note and registers it within the CRM timeline.

Depending on the communication type, additional information such as recording URLs or AI-generated summaries may be included.

---

# 3. Implementation Architecture

```text
                    Aloware
                        │
                Communication Event
                        │
                        ▼
                 Incoming Webhook
                        │
                        ▼
                  Make Scenario
                        │
                Validate Payload
                        │
                        ▼
               Identify Event Type
                        │
        ┌───────────────┼────────────────┐
        │               │                │
        ▼               ▼                ▼
      Call             SMS         Other Events
        │               │                │
        └───────────────┼────────────────┘
                        ▼
             Retrieve Kommo Entity
                        │
                        ▼
             Build Communication Note
                        │
          ┌─────────────┼─────────────┐
          │                           │
          ▼                           ▼
 Recording Available?          AI Summary Available?
          │                           │
          ▼                           ▼
 Append Recording URL       Append AI Summary
          └─────────────┬─────────────┘
                        ▼
               Create Kommo Note
                        │
                        ▼
                 Execution Logging
                        │
                        ▼
                    Completed
```

---

# 4. Execution Flow

The scenario executes sequentially after receiving an incoming webhook.

---

## Stage 1 – Receive Communication Event

Receive webhook notification from Aloware.

Outputs

- Event Type
- Contact Identifier
- Communication Metadata
- Timestamp

---

## Stage 2 – Validate Payload

Validate webhook integrity.

Validation includes:

- Supported Event Type
- Required Fields
- Contact Identifier
- Payload Structure

Invalid payloads terminate execution.

---

## Stage 3 – Identify Communication Type

Determine which communication has been received.

Supported types include:

- Call
- SMS
- Voicemail
- Recording
- AI Summary

Each type follows a dedicated processing path while sharing the same synchronization workflow.

---

## Stage 4 – Retrieve Kommo Entity

Locate the corresponding CRM entity.

Lookup priority:

- Aloware Contact ID
- Kommo Contact
- Kommo Lead

Execution terminates if no entity is found.

---

## Stage 5 – Data Transformation

Transform communication data into the Kommo Note model.

Activities include:

- Timestamp normalization
- Text formatting
- Communication template selection
- Metadata formatting

---

## Stage 6 – Optional Enrichment

Depending on the received event:

Recording

- Append recording URL.

AI Summary

- Append formatted AI summary.

SMS

- Append message body.

Call

- Append call metadata.

---

## Stage 7 – Note Creation

Create the communication Note in Kommo.

The Note shall include:

- Communication Type
- Agent
- Timestamp
- Communication Details
- Recording (if available)
- AI Summary (if available)

---

## Stage 8 – Logging

Register execution details.

Log:

- Event Type
- Contact
- Note ID
- Execution Time
- API Responses
- Errors

---

# 5. Make Scenario Design

The scenario shall be implemented using the following logical modules.

| Order | Module | Purpose |
|--------|---------|----------|
| 1 | Webhook | Receive Aloware Event |
| 2 | Payload Validation | Validate payload |
| 3 | Event Router | Route communication type |
| 4 | Contact Lookup | Find Kommo entity |
| 5 | Data Transformation | Build Note payload |
| 6 | Recording Processor | Append recording URL |
| 7 | AI Summary Processor | Append summary |
| 8 | Create Note | Register communication |
| 9 | Logger | Register execution |

---

# 6. Business Decision Points

## Decision 1

Is the event supported?

No

↓

Ignore Event

---

## Decision 2

Is the payload valid?

No

↓

Abort Execution

---

## Decision 3

Does the corresponding Kommo entity exist?

No

↓

Abort Execution

Log Failure

---

## Decision 4

Does the event include a recording?

Yes

↓

Append Recording URL

---

## Decision 5

Does the event include an AI Summary?

Yes

↓

Append AI Summary

---

## Decision 6

Was the Note successfully created?

Yes

↓

Complete Execution

No

↓

Log Failure

---

# 7. Data Transformation Design

| Source | Target | Transformation |
|----------|----------|----------------|
| Event Type | Note Title | Communication Template |
| Call Duration | Note | Text Formatting |
| SMS Content | Note | Direct Mapping |
| Recording URL | Note | URL Formatting |
| AI Summary | Note | Rich Text Formatting |
| Timestamp | Note Date | Date Normalization |
| Agent | Note Metadata | Direct Mapping |

---

# 8. API Operations

## Aloware

Operations:

- Receive Webhook

---

## Kommo

Operations:

- Search Contact
- Search Lead
- Create Note

---

# 9. Error Handling Design

## Recoverable Errors

- API Timeout
- Temporary Connectivity Failure
- Rate Limit

Action

Retry execution.

---

## Non-Recoverable Errors

- Unknown Contact
- Invalid Payload
- Unsupported Event
- Authentication Failure

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

- Communication Type
- Contact ID
- Lead ID
- Agent

Technical

- API Requests
- API Responses
- Processing Time
- Retry Count
- Error Details

---

# 11. Performance Considerations

Implementation shall minimize:

- Contact lookups
- API requests
- Execution latency

Whenever possible:

- Reuse retrieved entities.
- Avoid duplicate lookups.
- Reuse shared configuration.
- Minimize routing complexity.

---

# 12. Security Considerations

The scenario shall never expose:

- API Tokens
- OAuth Credentials
- Secrets

Only authenticated webhook requests shall be processed.

Sensitive information shall remain inside shared Make connections.

---

# 13. Dependencies

Infrastructure

- S00 Infrastructure

Business

- S01 Lead Sync

Configuration

- Communication Templates
- Shared Variables

External

- Aloware Webhooks
- Kommo API

---

# 14. Expected Deliverables

Upon implementation, the scenario shall provide:

- Operational communication webhook.
- Communication routing.
- Kommo Note creation.
- Recording integration.
- AI Summary integration.
- Execution logging.
- Error handling.
- Retry strategy.

---

# 15. Related Documentation

## Functional

- S02 Technical Sheet

## Operational

- S02 Build Checklist
- S02 Runbook
- S02 Testing

## Architecture

- Architecture Design
- Technical Design
- Integration Flows Design
- Mapping Model

---

# 16. Acceptance Criteria

Implementation shall be considered complete when:

- Supported communication events are successfully received.
- Payload validation executes correctly.
- Event routing functions correctly.
- Kommo entities are successfully identified.
- Communication Notes are created successfully.
- Recording URLs are included when available.
- AI Summaries are included when available.
- Logging captures every execution.
- Error handling behaves as designed.
- All defined test cases pass successfully.