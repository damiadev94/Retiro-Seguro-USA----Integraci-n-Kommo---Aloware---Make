# Field Mapping

**Version:** 1.0

**Status:** Draft

**Phase:** 2 — Technical Design

---

# Purpose

This document defines how business information is mapped between Kommo CRM and Aloware.

Its purpose is to identify which business entities and attributes participate in the integration, establish their conceptual correspondence between platforms, and define the ownership of each mapped field.

This document focuses on **what is mapped**, not **how it is transformed**. Data conversion, formatting, and normalization rules are documented separately.

---

# Scope

This document defines:

- Business entities participating in synchronization
- Conceptual field correspondence
- Field ownership
- Synchronization direction
- Mapping principles

This document intentionally excludes:

- Data transformations
- Validation rules
- API payloads
- Endpoint specifications
- Implementation details

---

# Mapping Objectives

The field mapping model has the following objectives:

- Maintain semantic consistency between platforms.
- Clearly identify the origin of every synchronized value.
- Avoid duplicate ownership.
- Simplify future maintenance.
- Facilitate implementation and testing.

---

# Mapping Principles

## Conceptual Mapping

Mappings are based on business meaning rather than field names.

Equivalent information may have different representations in each platform.

---

## Ownership Preservation

Each mapped field has a single authoritative source.

The destination system must never overwrite information owned by the source system.

---

## Directional Mapping

Mappings are directional.

A field may be synchronized:

- Kommo → Aloware
- Aloware → Kommo
- Both directions (only when ownership remains unambiguous)

---

## Selective Synchronization

Only fields required by the integration are synchronized.

Internal platform attributes remain outside the integration scope.

---

# Business Entity Mapping

The integration currently involves the following business entities.

| Business Entity | Kommo | Aloware | Synchronization |
|-----------------|--------|----------|-----------------|
| Lead | ✓ | Reference | Kommo → Aloware |
| Contact | ✓ | ✓ | Kommo → Aloware |
| Company | ✓ | Reference | Kommo → Aloware |
| Sales Owner | ✓ | Agent | Kommo → Aloware |
| Pipeline Stage | ✓ | List / Campaign | Kommo → Aloware |
| Call Activity | Reference | ✓ | Aloware → Kommo |
| SMS Activity | Reference | ✓ | Aloware → Kommo |
| Call Recording | Reference | ✓ | Aloware → Kommo |
| AI Summary | Reference | ✓ | Aloware → Kommo |

---

# Conceptual Field Categories

Instead of defining individual fields at this stage, mappings are organized into logical categories.

## Identification Fields

Examples include:

- Lead ID
- Contact ID
- Company ID
- External IDs
- Phone identifiers

These fields uniquely identify synchronized entities.

---

## Contact Information

Examples include:

- Name
- Phone number
- Email
- Company association

Used to identify communication recipients.

---

## Commercial Information

Examples include:

- Pipeline
- Stage
- Sales owner
- Lead status
- Commercial attributes

Owned by Kommo.

---

## Communication Information

Examples include:

- Call result
- Call duration
- Recording URL
- SMS content
- AI Summary

Owned by Aloware.

---

## Metadata

Examples include:

- Creation timestamps
- Update timestamps
- Source platform
- Synchronization identifiers

Used for operational purposes.

---

# Mapping Matrix

The following matrix defines the conceptual ownership of synchronized information.

| Field Category | Owner | Direction |
|----------------|-------|-----------|
| Lead Information | Kommo | Kommo → Aloware |
| Contact Information | Kommo | Kommo → Aloware |
| Company Information | Kommo | Kommo → Aloware |
| Sales Assignment | Kommo | Kommo → Aloware |
| Pipeline Information | Kommo | Kommo → Aloware |
| Call Data | Aloware | Aloware → Kommo |
| SMS Data | Aloware | Aloware → Kommo |
| Recording Data | Aloware | Aloware → Kommo |
| AI Summary | Aloware | Aloware → Kommo |

---

# Mapping Characteristics

The field mapping follows these characteristics.

## Explicit

Every synchronized field must have a documented correspondence.

---

## Traceable

The origin of every synchronized value must be identifiable.

---

## Deterministic

A field always maps to the same destination attribute.

---

## Maintainable

Changes to mappings should affect only the corresponding mapping definition.

---

## Extensible

Additional fields may be incorporated without redesigning the mapping model.

---

# Mapping Constraints

The following constraints apply.

- Fields without business value should not be synchronized.
- Computed values should remain in their originating system unless explicitly required.
- Internal platform identifiers should not be exposed unnecessarily.
- Mapping definitions should remain independent of API implementation details.

---

# Future Detailed Mapping

Detailed attribute-level mappings will be documented during implementation.

Typical information includes:

- Source field
- Destination field
- Data type
- Required status
- Default value
- Nullable behavior
- Synchronization direction
- Transformation reference

This document serves as the conceptual foundation for those implementation mappings.

---

# Related Documents

This document should be read together with:

- Synchronization Model
- Stage Mapping
- Agent Mapping
- Data Transformation Rules
- Validation Rules
- API Objects
- Data Mapping Requirements