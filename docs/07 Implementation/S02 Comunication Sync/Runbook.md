# S02 – Communication Sync

# Runbook

---

# Metadata

| Property | Value |
|----------|-------|
| Scenario ID | S02 |
| Name | Communication Sync |
| Phase | Implementation |
| Version | 1.0 |
| Status | Planned |
| Owner | Integration Team |
| Last Updated | YYYY-MM-DD |

---

# Purpose

This Runbook provides the operational procedure required to implement the **Communication Sync** scenario.

Unlike the **Build Checklist**, which defines **what** must be implemented, this document describes **how** each implementation phase shall be executed.

The Runbook is intended to be followed sequentially during implementation.

---

# Scope

This document covers the complete implementation of the Communication Sync scenario, including:

- Webhook configuration
- Communication event routing
- Payload validation
- Entity lookup
- Data transformation
- Note creation
- Recording integration
- AI Summary integration
- Logging
- Error handling
- Scenario validation

This document does not cover infrastructure setup or Lead synchronization, which are documented in **S00** and **S01** respectively.

---

# Required Resources

## Platforms

- Make
- Aloware
- Kommo

---

## Documentation

- Technical Sheet
- Implementation Design
- Mapping Model
- Technical Design
- Build Checklist

---

## Credentials

The following credentials shall already exist:

- Aloware API Connection
- Kommo OAuth Connection

No credentials shall be created during this procedure.

---

# Execution Workflow

```text
Preparation
      │
      ▼
Scenario Creation
      │
      ▼
Webhook Configuration
      │
      ▼
Payload Validation
      │
      ▼
Event Routing
      │
      ▼
Entity Lookup
      │
      ▼
Data Transformation
      │
      ▼
Optional Enrichment
      │
      ▼
Create Kommo Note
      │
      ▼
Logging
      │
      ▼
Validation
      │
      ▼
Completed
```

---

# Phase 1 – Preparation

Reference

PRE-001 → PRE-009

## Objective

Verify that every prerequisite required by the scenario is available.

## Procedure

Verify:

- S00 Infrastructure completed.
- S01 Lead Sync operational.
- Shared Make connections available.
- Communication webhooks configured.
- Shared variables available.
- Communication templates available.
- Required mappings configured.
- Aloware Contact IDs available in Kommo.

## Expected Result

Implementation environment is ready.

---

# Phase 2 – Scenario Creation

Reference

CFG-001 → CFG-006

## Objective

Create the Communication Sync scenario.

## Procedure

- Create a new Make scenario.
- Apply naming convention.
- Store the scenario in the implementation folder.
- Configure execution settings.
- Enable execution history.

## Expected Result

An operational Make scenario exists.

---

# Phase 3 – Webhook Configuration

Reference

CFG-101 → CFG-105

## Objective

Receive communication events from Aloware.

## Procedure

Create the webhook module.

Register the endpoint within Aloware.

Generate sample communication events.

Capture payload examples for:

- Call
- SMS
- Voicemail
- Recording
- AI Summary

Validate webhook reception.

## Expected Result

Communication events are successfully received.

---

# Phase 4 – Payload Validation

Reference

CFG-201 → CFG-205

## Objective

Validate incoming webhook data.

## Procedure

Verify:

- Event type
- Required fields
- Contact Identifier
- Payload integrity

Reject unsupported or invalid payloads.

## Expected Result

Only valid communication events continue processing.

---

# Phase 5 – Event Routing

Reference

CFG-301 → CFG-307

## Objective

Route communication events according to their type.

## Procedure

Configure routing logic for:

- Call
- SMS
- Voicemail
- Recording
- AI Summary

Validate that every supported event follows the correct processing path.

## Expected Result

Every communication event reaches the appropriate processing branch.

---

# Phase 6 – Entity Lookup

Reference

CFG-401 → CFG-405

## Objective

Locate the corresponding CRM entity.

## Procedure

Search using:

- Aloware Contact ID
- Kommo Contact
- Kommo Lead

Validate that exactly one matching entity is found.

Terminate execution if no valid entity exists.

## Expected Result

The correct Lead or Contact is identified.

---

# Phase 7 – Data Transformation

Reference

MAP-001 → MAP-009

## Objective

Transform communication information into the Kommo Note format.

## Procedure

Normalize:

- Communication type
- Timestamps
- Phone numbers (if applicable)

Format:

- Call metadata
- SMS body
- Voicemail details
- Communication templates

Build the final Note payload.

Validate payload completeness.

## Expected Result

A valid Kommo Note payload is generated.

---

# Phase 8 – Optional Enrichment

Reference

CFG-501 → CFG-506

## Objective

Enrich the communication Note when additional information is available.

## Procedure

Recording

- Validate recording availability.
- Append recording URL.

AI Summary

- Validate summary availability.
- Format summary.
- Append summary.

If enrichment data is unavailable, continue without interruption.

## Expected Result

The Note includes every available communication artifact.

---

# Phase 9 – Note Creation

Reference

CFG-601 → CFG-604

## Objective

Create the communication Note in Kommo.

## Procedure

Execute the Create Note API request.

Associate the Note with the correct entity.

Validate API response.

Store returned identifiers.

## Expected Result

The communication is successfully registered in Kommo.

---

# Phase 10 – Logging

Reference

CFG-701 → CFG-706

## Objective

Record complete execution information.

## Procedure

Log:

- Execution ID
- Event Type
- Lead ID
- Contact ID
- Note ID
- API Requests
- API Responses
- Processing Time
- Errors
- Retry Count

## Expected Result

Complete execution trace exists.

---

# Phase 11 – Error Handling

Reference

CFG-801 → CFG-806

## Objective

Handle unexpected execution failures.

## Procedure

Recoverable errors

- Retry execution according to the shared retry policy.

Non-recoverable errors

- Abort execution.
- Register failure.
- Preserve execution context.
- Notify operations when required.

## Expected Result

The scenario behaves predictably under failure conditions.

---

# Phase 12 – Validation

Reference

VAL-001 → VAL-010

## Objective

Verify successful implementation.

## Procedure

Execute every validation defined in **Testing.md**.

Verify:

- Webhook reception.
- Payload validation.
- Event routing.
- Entity lookup.
- Note creation.
- Recording integration.
- AI Summary integration.
- Logging.
- Error handling.

## Expected Result

The scenario passes every validation.

---

# Rollback Procedure

Rollback shall be executed if critical failures occur during implementation.

Steps:

1. Disable the scenario.
2. Remove temporary routing configuration.
3. Restore previous webhook configuration.
4. Remove temporary mappings.
5. Restore previous communication templates.
6. Validate environment integrity.

Rollback shall never remove communication history already synchronized into Kommo unless explicitly approved.

---

# Troubleshooting Guide

| Issue | Possible Cause | Resolution |
|---------|----------------|------------|
| Webhook not received | Invalid endpoint | Verify Aloware webhook configuration |
| Unsupported event ignored | Event routing configuration | Review router filters |
| Contact not found | Missing Contact ID | Verify S01 synchronization |
| Note not created | Invalid payload | Validate Note mapping |
| Recording missing | Recording URL unavailable | Verify event payload |
| AI Summary missing | Summary not generated | Validate AI processing |
| Duplicate Notes | Duplicate detection failure | Review idempotency logic |
| Authentication error | Invalid credentials | Verify Make connections |
| API timeout | Temporary platform issue | Retry execution |

---

# Exit Criteria

The implementation shall be considered complete when:

- Every Build Checklist task has been completed.
- Every validation has passed.
- Every test case has passed.
- Communication Notes are correctly created.
- Recording links are included when available.
- AI Summaries are included when available.
- Logging is operational.
- Error handling has been validated.
- Technical review completed.
- Functional review completed.

---

# Related Documentation

## Scenario

- Technical Sheet
- Implementation Design
- Build Checklist
- Testing

## Architecture

- Architecture Design
- Technical Design
- Integration Flows Design
- Mapping Model