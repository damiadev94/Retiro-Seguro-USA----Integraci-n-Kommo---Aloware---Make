# SCENARIO CATALOG

**Project:** Kommo ↔ Aloware Integration via Make

**Version:** 1.0

**Status:** Draft

**Phase:** 4 — Implementation

---

# 1. Purpose

## Objective

This document defines the complete catalog of Make scenarios required to implement the Kommo ↔ Aloware integration.

Its purpose is to provide a structured inventory of every implementation unit, defining the responsibility, scope, dependencies and implementation order of each scenario.

Each scenario represents an independent business capability and serves as the primary implementation unit throughout the project.

---

# 2. Scope

This catalog includes every Make scenario required to implement the approved integration architecture.

For each scenario the catalog identifies:

- Purpose
- Responsibility
- Source system
- Target system
- Trigger mechanism
- Primary business process
- Dependencies
- Priority
- Implementation order

Detailed implementation instructions are intentionally excluded and documented within each Scenario Design and Runbook.

---

# 3. Scenario Classification

The implementation is divided into three categories of scenarios.

## Infrastructure

Shared platform configuration and reusable components required by multiple business scenarios.

---

## Business Synchronization

Scenarios responsible for synchronizing business information between Kommo and Aloware.

---

## Shared Services

Reusable processes supporting multiple scenarios.

Examples include:

- Error Handling
- Logging
- Retry
- Lookup
- Utilities

---

# 4. Scenario Catalog

| ID | Name | Category | Source | Target | Priority | Status |
|----|------|----------|---------|---------|----------|--------|
| S00 | Infrastructure | Infrastructure | Make | Make | Critical | Pending |
| S01 | Lead Sync | Business Synchronization | Kommo | Aloware | Critical | Pending |
| S02 | Communication Sync | Business Synchronization | Aloware | Kommo | Critical | Pending |

---

# 5. Scenario Summary

---

## S00 — Infrastructure

### Purpose

Prepare the shared implementation environment required by all integration scenarios.

### Responsibilities

- Configure platform connections
- Configure shared variables
- Configure webhook endpoints
- Configure reusable functions
- Configure logging
- Configure global error handling

### Trigger

Manual implementation.

### Source

Make

### Target

Make

### Dependencies

None

---

## S01 — Lead Sync

### Purpose

Synchronize commercial information from Kommo into Aloware.

### Responsibilities

- Receive Kommo webhook
- Validate payload
- Retrieve CRM information
- Transform business data
- Lookup existing contact
- Create or update contact
- Assign responsible agent
- Assign communication sequence
- Log execution

### Trigger

Kommo Webhook

### Source

Kommo CRM

### Target

Aloware

### Dependencies

- S00 completed

---

## S02 — Communication Sync

### Purpose

Synchronize communication activity generated in Aloware back into Kommo.

### Responsibilities

- Receive communication webhook
- Validate payload
- Resolve customer
- Resolve Lead
- Register communication
- Register Recording
- Register AI Summary
- Register SMS
- Log execution

### Trigger

Aloware Webhook

### Source

Aloware

### Target

Kommo CRM

### Dependencies

- S00 completed

---

# 6. Scenario Dependencies

| Scenario | Depends On |
|----------|------------|
| S00 | None |
| S01 | S00 |
| S02 | S00 |

Business scenarios are independent from each other and communicate only through the participating platforms.

No scenario shall invoke another scenario directly.

---

# 7. Implementation Order

The scenarios shall be implemented in the following order.

| Order | Scenario | Reason |
|--------|----------|--------|
| 1 | S00 | Shared platform configuration |
| 2 | S01 | Primary business synchronization |
| 3 | S02 | Communication synchronization |

Implementation shall not continue until the current scenario has successfully completed validation.

---

# 8. Validation Ownership

| Scenario | Functional Validation | Technical Validation | Acceptance |
|----------|-----------------------|----------------------|------------|
| S00 | Infrastructure | Platform Connectivity | Ready |
| S01 | Commercial Synchronization | API Validation | Approved |
| S02 | Communication Synchronization | API Validation | Approved |

---

# 9. Related Documentation

Each scenario shall have its own documentation set.

| Scenario | Design | Runbook | Testing |
|----------|--------|----------|----------|
| S00 | S00 Infrastructure Design | RB-S00 | TC-S00 |
| S01 | S01 Lead Sync Design | RB-S01 | TC-S01 |
| S02 | S02 Communication Sync Design | RB-S02 | TC-S02 |

---

# 10. Exit Criteria

The Scenario Catalog is considered complete when:

- Every required scenario has been identified.
- Each scenario has a unique responsibility.
- Dependencies are documented.
- Implementation order is defined.
- Every scenario references its Design, Runbook and Test documentation.