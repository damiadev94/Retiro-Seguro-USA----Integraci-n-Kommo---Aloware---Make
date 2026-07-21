# Agent Mapping

**Version:** 1.0

**Status:** Draft

**Phase:** 2 — Technical Design

---

# Purpose

This document defines the conceptual mapping between users in Kommo CRM and agents in Aloware.

Its purpose is to establish how ownership and responsibility for customer interactions are synchronized across both platforms while preserving a single authoritative source for user assignments.

This document defines **who corresponds to whom**, not the implementation details of user synchronization.

---

# Scope

This document defines:

- User ownership
- Agent correspondence
- Assignment synchronization
- Mapping principles
- Mapping constraints

This document intentionally excludes:

- User provisioning
- Authentication
- Permission management
- API implementation
- Workflow configuration
- Synchronization logic

---

# Objectives

The agent mapping model has the following objectives:

- Maintain consistent ownership across platforms.
- Ensure communication activities are assigned to the correct agent.
- Prevent assignment conflicts.
- Support scalable user management.
- Simplify future organizational changes.

---

# Ownership

User assignments are owned by Kommo CRM.

Aloware receives agent assignments to execute communication activities but does not determine commercial ownership.

| Domain | System of Record |
|---------|------------------|
| Sales Owner | Kommo CRM |
| Lead Assignment | Kommo CRM |
| Communication Agent | Aloware |

Ownership is never transferred.

---

# Synchronization Direction

```text
Kommo CRM
     │
     │ Owner Assignment
     ▼
    Make
     │
     ▼
  Aloware Agent
```

Assignments originate in Kommo and are propagated to Aloware.

Changes performed directly in Aloware should not modify ownership in Kommo.

---

# Mapping Strategy

The integration follows a **one-to-one conceptual mapping** between sales owners and communication agents whenever possible.

Each commercial owner is associated with a corresponding operational agent responsible for customer communications.

This mapping allows both systems to remain aligned while preserving their independent user management.

---

# Conceptual Mapping

The mapping relates business responsibilities rather than platform-specific identifiers.

| Kommo Role | Aloware Role |
|-------------|--------------|
| Sales Owner | Communication Agent |
| Account Manager | Assigned Agent |
| Sales Representative | Calling Agent |
| Team Member | Operational Agent |

The exact user identifiers are documented separately during implementation.

---

# Assignment Behavior

When the owner of a lead changes in Kommo:

1. The assignment event is generated.
2. Make receives the event.
3. The corresponding Aloware agent is identified.
4. The communication assignment is updated.
5. Future communication activities are associated with the mapped agent.

Only the affected lead is updated.

---

# Mapping Characteristics

## One-Way Synchronization

Assignments are synchronized exclusively from Kommo to Aloware.

---

## Explicit Relationships

Every synchronized owner should have an explicitly defined corresponding agent.

Implicit mappings should be avoided.

---

## Stable Assignments

A user should always map to the same operational agent unless the mapping configuration is intentionally updated.

---

## Independent User Management

Each platform maintains its own user accounts.

The integration synchronizes assignments rather than user administration.

---

# Unmapped Users

Some users may not participate in the integration.

Examples include:

- Administrators
- Read-only users
- Support personnel
- Inactive accounts

If no corresponding agent exists:

- The synchronization should not assign the lead automatically.
- The event should be logged for operational review.
- Existing assignments should remain unchanged unless otherwise defined.

---

# Organizational Changes

The mapping model supports organizational evolution.

Examples include:

- New sales representatives
- New communication agents
- Team restructuring
- User deactivation
- Role reassignment

Mapping definitions should be updated before organizational changes become operational.

---

# Design Principles

The agent mapping model follows these principles:

- Kommo owns commercial assignments.
- Aloware reflects operational responsibility.
- One owner corresponds to one operational agent whenever possible.
- User administration remains independent in each platform.
- Mapping relationships are explicit and documented.
- Assignment synchronization should be deterministic.

---

# Future Detailed Mapping

The implementation phase will introduce a detailed mapping specification including:

- Kommo User ID
- Kommo User Name
- Kommo Email
- Aloware Agent ID
- Aloware Agent Name
- Synchronization Status
- Active Flag
- Notes

This document serves as the conceptual foundation for that specification.

---

# Related Documents

This document should be read together with:

- Synchronization Model
- Field Mapping
- Stage Mapping
- Data Transformation Rules
- Validation Rules
- Integration Flows Design