# Stage Mapping

**Version:** 1.0

**Status:** Draft

**Phase:** 2 — Technical Design

---

# Purpose

This document defines the conceptual mapping between the sales pipeline stages managed in Kommo CRM and the operational states, lists, or communication workflows managed in Aloware.

Its purpose is to establish how changes in the commercial lifecycle are translated into communication actions while preserving the ownership of each platform.

This document defines **which business states correspond between systems**, not the automation logic used to process them.

---

# Scope

This document defines:

- Stage ownership
- Stage synchronization principles
- Conceptual stage correspondence
- Synchronization direction
- Mapping constraints

This document intentionally excludes:

- Make scenarios
- API implementation
- Workflow configuration
- Automation rules
- Validation logic

---

# Objectives

The stage mapping model has the following objectives:

- Maintain alignment between sales and communication processes.
- Ensure that communication workflows reflect the current commercial status.
- Avoid ambiguous stage relationships.
- Preserve a single commercial source of truth.
- Simplify future pipeline changes.

---

# Ownership

Pipeline stages belong exclusively to Kommo CRM.

Aloware consumes this information to organize communication activities but does not own or manage the commercial lifecycle.

| Domain | System of Record |
|---------|------------------|
| Sales Pipeline | Kommo CRM |
| Lead Stage | Kommo CRM |
| Communication Lists | Aloware |
| Dialing Campaigns | Aloware |

Stage synchronization is therefore **unidirectional**.

---

# Synchronization Direction

```text
Kommo CRM
     │
     │ Pipeline Stage Changes
     ▼
    Make
     │
     ▼
 Aloware Lists / Campaigns
```

Changes originating in Aloware must never modify the sales pipeline in Kommo.

---

# Mapping Strategy

The integration follows a **business-state mapping** strategy.

Rather than attempting to replicate the pipeline structure, each commercial stage is associated with the operational communication state that best represents the desired customer interaction.

This approach allows both systems to evolve independently while maintaining consistent behavior.

---

# Conceptual Mapping

Each relevant sales stage may correspond to one operational destination in Aloware.

| Kommo Business Stage | Aloware Operational State |
|----------------------|---------------------------|
| New Lead | Initial Contact Queue |
| Contact Attempt | Outbound Calling Queue |
| Qualified Lead | Active Follow-up Queue |
| Proposal Sent | Follow-up Campaign |
| Negotiation | Priority Contact Queue |
| Won | Customer Communication Flow |
| Lost | Closed / Archived |

The exact stage names will be documented in the implementation specification.

---

# Mapping Characteristics

## One-Way Synchronization

Commercial stages are synchronized only from Kommo to Aloware.

---

## Explicit Mapping

Every synchronized stage must have an explicitly defined destination.

Undefined mappings should never rely on implicit behavior.

---

## Stable Relationships

Each business stage should always produce the same operational destination.

Mappings should remain predictable and deterministic.

---

## Business-Oriented

Mappings represent business intent rather than technical implementation.

Operational states should reflect the communication strategy associated with each sales stage.

---

# Synchronization Behavior

When a mapped stage changes in Kommo:

1. The business event is generated.
2. Make receives the event.
3. The stage mapping is evaluated.
4. The corresponding operational destination is identified.
5. Aloware is updated accordingly.

Only the affected lead is synchronized.

---

# Unmapped Stages

Not every stage necessarily participates in the integration.

Stages without communication relevance may be excluded.

If a stage has no defined mapping:

- No synchronization is executed.
- The event is ignored.
- No communication workflow is modified.

This prevents unintended automation.

---

# Pipeline Evolution

Sales pipelines may evolve over time.

To support future changes:

- Stage mappings should remain independent of implementation.
- New stages should be documented before activation.
- Removed stages should be deprecated in the mapping documentation.
- Existing mappings should remain stable whenever possible.

---

# Design Principles

The stage mapping model follows these principles:

- Kommo owns the commercial lifecycle.
- Aloware reflects communication readiness.
- One business stage produces one predictable operational outcome.
- Mappings are explicit and documented.
- Business meaning takes precedence over technical naming.
- Pipeline evolution should not require architectural redesign.

---

# Future Detailed Mapping

The implementation phase will introduce a detailed mapping specification including:

- Kommo Pipeline ID
- Kommo Stage ID
- Kommo Stage Name
- Aloware List ID
- Aloware Campaign ID
- Synchronization Trigger
- Processing Conditions
- Notes

This document serves as the conceptual foundation for that specification.

---

# Related Documents

This document should be read together with:

- Synchronization Model
- Field Mapping
- Agent Mapping
- Integration Flows Design
- Data Transformation Rules