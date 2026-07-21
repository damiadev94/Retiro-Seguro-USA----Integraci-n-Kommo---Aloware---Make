# Stage Mapping Specification

**Version:** 1.0

**Status:** Pending

**Phase:** 3.3 — Configuration Discovery

---

# Purpose

This document defines how Kommo pipeline stages map to actions within the Kommo ↔ Aloware integration.

Its objective is to identify which stage transitions trigger automation workflows, the corresponding actions executed in Aloware, and the business rules governing those events.

---

# Scope

This specification covers:

- Pipelines
- Pipeline stages
- Stage transition events
- Trigger conditions
- Aloware actions
- Synchronization rules
- Validation requirements

---

# Mapping Principles

The stage mapping follows these principles:

- Stage transitions are the primary business events.
- Only approved stages trigger integrations.
- Each stage has a clearly defined action.
- Trigger behavior must be deterministic.
- Business rules take precedence over technical implementation.

---

# Trigger Event

The integration is initiated when a lead changes to a configured stage within a Kommo pipeline.

| Event | Description |
|-------|-------------|
| Lead Stage Changed | A lead is moved to a configured pipeline stage. |

---

# Stage Mapping

Document every stage that participates in the integration.

| Pipeline | Stage ID | Stage Name | Trigger Integration | Aloware Action | Notes |
|----------|----------|------------|---------------------|----------------|-------|
| | | | ☐ Yes ☐ No | | |

---

# Trigger Configuration

For each mapped stage, define the expected behavior.

| Stage | Trigger Event | Execution |
|--------|---------------|-----------|
| | Lead enters stage | Execute immediately / Delayed |

---

# Aloware Actions

Possible actions executed after a stage transition.

| Action | Description |
|--------|-------------|
| Create Contact | Create the contact if it does not already exist. |
| Update Contact | Synchronize contact information. |
| Assign Agent | Assign the mapped Aloware agent. |
| Add to Power Dialer List | Add the contact to the configured dialing list. |
| Update Campaign | Associate the contact with a campaign. |
| No Action | Stage change is informational only. |

---

# Business Rules

Document the business logic associated with each stage.

| Stage | Business Rule |
|--------|---------------|
| | |

---

# Execution Conditions

A stage transition should only trigger the integration when all required conditions are met.

| Condition | Required |
|-----------|----------|
| Lead Exists | ✅ |
| Contact Exists | ✅ |
| Phone Number Available | ✅ |
| Agent Mapping Available | ✅ |
| Stage Mapping Defined | ✅ |

---

# Synchronization Rules

| Rule | Description |
|------|-------------|
| One execution per stage transition | Prevent duplicate processing of the same event. |
| Ignore unchanged stages | No action if the stage remains the same. |
| Process only configured stages | Unmapped stages are ignored. |
| Preserve lead ownership | Responsible user remains managed by Kommo. |

---

# Validation Rules

| Validation | Action if Invalid |
|------------|-------------------|
| Stage Not Mapped | Ignore event |
| Missing Pipeline | Stop processing |
| Missing Agent Mapping | Stop processing |
| Missing Phone Number | Reject synchronization |
| Invalid Contact | Reject synchronization |

---

# Error Handling

| Condition | Action |
|-----------|--------|
| Duplicate Webhook | Ignore duplicate event |
| Stage Mapping Missing | Log error and stop |
| Aloware API Error | Retry according to Retry Strategy |
| Validation Failure | Log error and stop |

---

# Dependencies

This specification depends on:

- Kommo Configuration Inventory
- Aloware Configuration Inventory
- Field Mapping Specification
- Agent Mapping Specification

---

# Validation Checklist

- [ ] All integration stages identified
- [ ] Trigger events documented
- [ ] Aloware actions defined
- [ ] Business rules documented
- [ ] Validation rules completed
- [ ] Customer approval completed

---

# Observations

-

---

# Approval

| Role | Name | Date |
|------|------|------|
| Integration Engineer | | |
| Customer | | |

---

# Final Result

| Item | Status |
|------|--------|
| Stage Mapping Completed | ☐ Yes ☐ No |
| Ready for Implementation | ☐ Yes ☐ No |