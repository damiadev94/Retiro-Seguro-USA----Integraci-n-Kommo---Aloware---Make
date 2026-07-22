# S00 – Infrastructure

# Runbook

---

# Metadata

| Property | Value |
|----------|-------|
| Scenario ID | S00 |
| Name | Infrastructure |
| Phase | Implementation |
| Version | 1.1 |
| Status | Approved |
| Owner | Integration Team |
| Last Updated | YYYY-MM-DD |

---

# Purpose

This Runbook defines the execution workflow required to prepare the shared infrastructure used by all integration scenarios between Kommo CRM and Aloware.

The objective is to ensure that every platform, authentication method, webhook, shared configuration, and operational component is correctly configured and validated before implementing any business scenario.

This Runbook does **not** implement business logic.

Detailed procedures are documented in the corresponding Standard Operating Procedures (SOPs).

---

# Scope

This Runbook includes:

- Workspace preparation
- Platform authentication
- Shared infrastructure
- Webhook registration
- Shared configuration
- Operational services
- Validation
- Documentation
- Infrastructure approval

This Runbook does **not** include:

- Lead synchronization
- Contact synchronization
- Dialer assignment
- SMS synchronization
- Call synchronization

Those processes are implemented in functional scenarios (S01+).

---

# Required Platforms

- Make
- Kommo CRM
- Aloware

---

# Required Documentation

- Technical Sheet
- Implementation Design
- Build Checklist
- Mapping Model

---

# Required Credentials

| Platform | Credential |
|-----------|------------|
| Make | Workspace Access |
| Kommo | Long-lived Token |
| Aloware | API Token |

---

# Required Configuration

| Item | Source |
|------|--------|
| Kommo Base URL | Environment Configuration |
| Kommo Long-lived Token | Private Integration |
| Aloware Base URL | Environment Configuration |
| Aloware API Token | Aloware |
| Pipeline Mapping | Mapping Model |
| Stage Mapping | Mapping Model |
| Agent Mapping | Mapping Model |

---

# Execution Workflow

Preparation
    │
    ▼
Workspace Validation
    │
    ▼
Authentication
    │
    ▼
Kommo Webhook Configuration
    │
    ▼
Shared Configuration
    │
    ▼
Operational Components
    │
    ▼
Infrastructure Validation
    │
    ▼
Documentation
    │
    ▼
Approval

---

# Phase 1 — Preparation

## Objective

Verify that all implementation prerequisites are available.

| Task | SOP |
|------|-----|
| PRE-001 Verify Organization | SOP-MAKE-001 |
| PRE-002 Verify Team | SOP-MAKE-001 |
| PRE-003 Verify Workspace | SOP-MAKE-001 |
| PRE-004 Verify Administrator Access | SOP-MAKE-001 |
| PRE-005 Verify Documentation | SOP Lifecycle |

### Exit Criteria

- Workspace accessible.
- Documentation available.
- Required credentials obtained.

### Validation

- Organization accessible.
- Workspace operational.

---

# Phase 2 — Workspace

## Objective

Prepare the Make workspace according to project standards.

| Task | SOP |
|------|-----|
| CFG-001 Configure Folder Structure | SOP-INF-007 |
| CFG-002 Apply Naming Convention | SOP-INF-008 |
| CFG-003 Create Infrastructure Scenario | SOP-MAKE-001 |

### Exit Criteria

Workspace prepared.

### Validation

Infrastructure scenario created.

---

# Phase 3 — Authentication

## Objective

Configure and validate every platform connection.

| Task | SOP |
|------|-----|
| CFG-101 Configure Kommo Authentication | SOP-KOM-001 |
| CFG-102 Validate Kommo Long-lived Token | SOP-KOM-001 |
| CFG-103 Configure Aloware Authentication | SOP-ALO-001 |
| CFG-104 Validate Aloware API Token | SOP-ALO-001 |
| CFG-105 Perform HTTP Connectivity Test | SOP-INF-001 |

### Expected Result

- Kommo responds HTTP 200.
- Aloware responds HTTP 200.

### Validation

Example validation:

```
GET /api/v4/account
```

Result:

```
HTTP 200 OK
```

### Exit Criteria

All platform connections validated.

---

# Phase 4 — Webhooks

## Objective

Configure and validate the inbound webhook infrastructure required to receive events from external systems.

At this stage, only the infrastructure shared by the integration is configured. Webhooks specific to individual business scenarios are implemented within their corresponding scenario documentation.

---

## Tasks

| ID | Task | Status |
|----|------|--------|
| CFG-201 | Create Make Custom Webhook (Kommo) | Pending |
| CFG-202 | Register Kommo Webhook | Pending |
| CFG-203 | Receive Test Payload | Pending |
| CFG-204 | Capture Sample Payload | Pending |
| CFG-205 | Validate Payload Schema | Pending |

---

## Implementation

### CFG-201 — Create Make Custom Webhook

Create a Custom Webhook in Make that will receive events from Kommo.

Deliverable:

- Active Make Webhook URL

Validation:

- Webhook URL generated successfully.

---

### CFG-202 — Register Kommo Webhook

Register the Make Webhook URL in Kommo.

Event:

- Lead Status Changed

Validation:

- Kommo accepts the webhook configuration.
- Test event reaches Make.

---

### CFG-203 — Receive Test Payload

Generate a Lead stage change inside Kommo.

Validation:

- Webhook execution appears in Make.
- HTTP request successfully received.

---

### CFG-204 — Capture Sample Payload

Export the complete webhook payload.

Deliverables:

- Sample JSON payload
- Stored inside the project artifacts

Validation:

- Payload contains all expected fields.

---

### CFG-205 — Validate Payload Schema

Validate the webhook payload against the integration requirements.

Expected fields:

- Lead ID
- Pipeline ID
- Status ID
- Previous Status ID
- Responsible User ID
- Tags

Document:

- Available fields
- Missing fields
- Architectural implications

Result:

- Payload approved for downstream processing.

---

## Out of Scope

The following webhook configurations are intentionally excluded from S00 because they belong to functional scenarios:

| Scenario | Responsibility |
|----------|----------------|
| S01 — Kommo → Aloware | Uses the shared Kommo webhook configured in S00. |
| S02 — Aloware → Kommo | Creates and configures the Aloware webhook, captures payloads, and validates the event schema. |

---

## Deliverables

- Active Kommo Webhook
- Successful webhook execution
- Sample payload
- Payload validation completed

---

# Phase 5 — Shared Configuration

## Objective

Configure reusable infrastructure values.

| Task | SOP |
|------|-----|
| CFG-301 Configure Shared Constants | SOP-INF-002 |
| CFG-302 Configure Base URLs | SOP-INF-002 |
| CFG-303 Configure Pipeline IDs | SOP-INF-002 |
| CFG-304 Configure Stage IDs | SOP-INF-002 |
| CFG-305 Configure Agent Mapping | SOP-INF-002 |
| CFG-306 Configure Environment Constants | SOP-INF-009 |

### Shared Configuration

Typical shared configuration includes:

- Kommo Base URL
- Aloware Base URL
- Pipeline IDs
- Stage IDs
- Agent Mapping
- Environment constants

### Exit Criteria

Shared configuration documented.

---

# Phase 6 — Operational Components

## Objective

Prepare reusable operational services.

| Task | SOP |
|------|-----|
| CFG-401 Configure Logging | SOP-INF-006 |
| CFG-402 Configure Error Handler | SOP-INF-004 |
| CFG-403 Configure Retry Policy | SOP-INF-005 |
| CFG-404 Configure Error Notifications | SOP-INF-004 |

### Exit Criteria

Operational services available.

---

# Phase 7 — Infrastructure Validation

## Objective

Validate that the infrastructure is production-ready.

| Task | SOP |
|------|-----|
| VAL-001 Workspace Validation | SOP-TST-006 |
| VAL-002 Authentication Validation | SOP-TST-006 |
| VAL-003 Webhook Validation | SOP-TST-003 |
| VAL-004 Shared Configuration Validation | SOP-TST-006 |
| VAL-005 Operational Components Validation | SOP-TST-006 |

### Validation Checklist

Infrastructure must confirm:

- Workspace operational
- Kommo authentication successful
- Aloware authentication successful
- HTTP connectivity verified
- Webhooks receiving events
- Sample payload captured
- Shared configuration available
- Logging operational
- Error Handler operational
- Retry Policy configured

### Exit Criteria

Infrastructure validated.

---

# Phase 8 — Documentation

## Objective

Record the final infrastructure state.

| Task | SOP |
|------|-----|
| DOC-001 Update Technical Sheet | SOP Template |
| DOC-002 Update Build Checklist | SOP Template |
| DOC-003 Register Validation Evidence | SOP Template |
| DOC-004 Update Project Documentation | SOP Template |

### Deliverables

- Technical Sheet
- Validation Evidence
- Updated Build Checklist
- Infrastructure Verification Report

### Exit Criteria

Documentation completed.

---

# Phase 9 — Approval

## Objective

Approve the infrastructure for functional implementation.

| Task | SOP |
|------|-----|
| APP-001 Final Technical Review | SOP-OPS-001 |
| APP-002 Infrastructure Approval | SOP Lifecycle |
| APP-003 Enable Functional Scenarios | SOP Lifecycle |

### Exit Criteria

Infrastructure approved.

---

# Rollback Strategy

If infrastructure validation fails:

1. Stop implementation.
2. Remove incomplete configuration.
3. Restore previous configuration.
4. Record the incident.
5. Correct the issue.
6. Repeat validation.

---

# Success Criteria

Infrastructure implementation is considered successful when:

- Workspace configured.
- Authentication validated.
- Webhooks operational.
- Sample payload captured.
- Shared configuration documented.
- Logging configured.
- Error handling configured.
- Retry strategy configured.
- Validation completed.
- Documentation updated.
- Infrastructure approved.

At this point, implementation of functional scenarios (S01+) may begin.

---

# Deliverables

- Infrastructure Scenario
- Validated Connections
- Registered Webhooks
- Shared Configuration
- Infrastructure Verification Report
- Updated Documentation

---

# Related Documentation

- Technical Sheet
- Implementation Design
- Build Checklist
- Testing
- Mapping Model
- SOP Library