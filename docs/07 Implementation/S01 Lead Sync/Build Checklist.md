# S01 – Lead Sync

# Build Checklist

---

# Metadata

| Property | Value |
|----------|-------|
| Scenario ID | S01 |
| Name | Lead Sync |
| Phase | Implementation |
| Version | 1.0 |
| Status | Planned |
| Owner | Integration Team |
| Last Updated | YYYY-MM-DD |

---

# Purpose

This document defines the complete implementation checklist required to build the **Lead Sync** scenario.

Each task represents a single executable implementation activity.

Detailed implementation procedures are documented in the corresponding Runbook.

---

# Task Classification

| Prefix | Description |
|---------|-------------|
| PRE | Preparation |
| CFG | Configuration |
| MAP | Mapping |
| VAL | Validation |
| TST | Testing |
| DOC | Documentation |
| APP | Approval |

---

# Phase 1 – Preparation

## Scenario Preparation

- [ ] PRE-001 Verify S00 Infrastructure is operational.
- [ ] PRE-002 Verify Kommo connection.
- [ ] PRE-003 Verify Aloware connection.
- [ ] PRE-004 Verify webhook endpoint availability.
- [ ] PRE-005 Verify shared configuration.
- [ ] PRE-006 Verify Agent Mapping configuration.
- [ ] PRE-007 Verify Stage Mapping configuration.
- [ ] PRE-008 Verify Sequence Mapping configuration.
- [ ] PRE-009 Verify required Custom Fields.
- [ ] PRE-010 Verify implementation environment.

---

# Phase 2 – Scenario Creation

## Make Scenario

- [ ] CFG-001 Create new Make Scenario.
- [ ] CFG-002 Configure scenario name.
- [ ] CFG-003 Assign scenario folder.
- [ ] CFG-004 Configure scheduling settings.
- [ ] CFG-005 Enable execution history.
- [ ] CFG-006 Configure scenario metadata.

---

# Phase 3 – Webhook Configuration

## Kommo Webhook

- [ ] CFG-101 Create webhook module.
- [ ] CFG-102 Register webhook endpoint.
- [ ] CFG-103 Validate webhook reception.
- [ ] CFG-104 Store sample payload.
- [ ] CFG-105 Document payload structure.

---

# Phase 4 – Data Retrieval

## Kommo Objects

- [ ] CFG-201 Configure Get Lead module.
- [ ] CFG-202 Configure Get Contact module.
- [ ] CFG-203 Configure Get Company module (if applicable).
- [ ] CFG-204 Configure Get Responsible User.
- [ ] CFG-205 Retrieve Custom Fields.
- [ ] CFG-206 Validate retrieved data.

---

# Phase 5 – Business Validation

## Validation Rules

- [ ] CFG-301 Validate pipeline.
- [ ] CFG-302 Validate stage.
- [ ] CFG-303 Validate phone number.
- [ ] CFG-304 Validate required fields.
- [ ] CFG-305 Validate owner.
- [ ] CFG-306 Validate Agent Mapping.
- [ ] CFG-307 Validate Sequence Mapping.
- [ ] CFG-308 Configure validation filters.

---

# Phase 6 – Data Transformation

## Payload Construction

- [ ] MAP-001 Normalize phone number.
- [ ] MAP-002 Normalize contact name.
- [ ] MAP-003 Normalize email.
- [ ] MAP-004 Map owner.
- [ ] MAP-005 Map sequence.
- [ ] MAP-006 Build Aloware payload.
- [ ] MAP-007 Validate payload.

---

# Phase 7 – Contact Synchronization

## Contact Lookup

- [ ] CFG-401 Configure Search Contact module.
- [ ] CFG-402 Configure duplicate detection.
- [ ] CFG-403 Configure router.

### Contact Creation

- [ ] CFG-404 Configure Create Contact module.
- [ ] CFG-405 Map Create payload.
- [ ] CFG-406 Validate Create response.

### Contact Update

- [ ] CFG-407 Configure Update Contact module.
- [ ] CFG-408 Map Update payload.
- [ ] CFG-409 Validate Update response.

---

# Phase 8 – Sequence Assignment

## Outbound Sequence

- [ ] CFG-501 Configure Assign Sequence module.
- [ ] CFG-502 Configure Sequence Mapping.
- [ ] CFG-503 Validate assignment response.

---

# Phase 9 – Reverse Synchronization

## Kommo Update

- [ ] CFG-601 Configure Update Contact module.
- [ ] CFG-602 Persist Aloware Contact ID.
- [ ] CFG-603 Validate update.

---

# Phase 10 – Logging

## Operational Logging

- [ ] CFG-701 Configure execution logging.
- [ ] CFG-702 Configure success logging.
- [ ] CFG-703 Configure error logging.
- [ ] CFG-704 Configure retry logging.
- [ ] CFG-705 Configure execution identifiers.

---

# Phase 11 – Error Handling

## Exception Management

- [ ] CFG-801 Configure retry handlers.
- [ ] CFG-802 Configure timeout handling.
- [ ] CFG-803 Configure API error handling.
- [ ] CFG-804 Configure validation failure handling.
- [ ] CFG-805 Configure unexpected exception handling.

---

# Phase 12 – Scenario Validation

## Functional Validation

- [ ] VAL-001 Validate webhook execution.
- [ ] VAL-002 Validate Lead retrieval.
- [ ] VAL-003 Validate Contact retrieval.
- [ ] VAL-004 Validate business rules.
- [ ] VAL-005 Validate transformations.
- [ ] VAL-006 Validate Create Contact.
- [ ] VAL-007 Validate Update Contact.
- [ ] VAL-008 Validate Sequence Assignment.
- [ ] VAL-009 Validate Reverse Synchronization.
- [ ] VAL-010 Validate execution logging.

---

# Phase 13 – Testing

## Scenario Testing

- [ ] TST-001 Execute happy path.
- [ ] TST-002 Execute duplicate scenario.
- [ ] TST-003 Execute invalid stage.
- [ ] TST-004 Execute missing phone.
- [ ] TST-005 Execute missing mapping.
- [ ] TST-006 Execute API timeout.
- [ ] TST-007 Execute authentication failure.
- [ ] TST-008 Execute retry validation.
- [ ] TST-009 Execute idempotency validation.

---

# Phase 14 – Documentation

## Project Documentation

- [ ] DOC-001 Update implementation notes.
- [ ] DOC-002 Capture evidence.
- [ ] DOC-003 Update scenario documentation.
- [ ] DOC-004 Register implementation decisions.
- [ ] DOC-005 Register known limitations.

---

# Phase 15 – Approval

## Implementation Approval

- [ ] APP-001 Verify Build Checklist completion.
- [ ] APP-002 Verify Runbook completion.
- [ ] APP-003 Verify Testing completion.
- [ ] APP-004 Technical Review.
- [ ] APP-005 Functional Review.
- [ ] APP-006 Approve scenario implementation.

---

# Completion Criteria

The Build Checklist shall be considered complete only when:

- All implementation tasks have been completed.
- All validations have passed.
- All testing has been successfully executed.
- Documentation has been updated.
- Technical approval has been granted.
- Functional approval has been granted.

---

# Related Documentation

## Scenario Documentation

- Technical Sheet
- Implementation Design
- Runbook
- Testing

## Project Documentation

- Scenario Catalog
- Implementation Plan
- Architecture Design
- Technical Design
- Mapping Model