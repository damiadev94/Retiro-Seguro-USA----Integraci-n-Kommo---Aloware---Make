# Field Mapping Specification

**Version:** 1.0

**Status:** Pending

**Phase:** 3.3 — Configuration Discovery

---

# Purpose

This document defines how data is mapped between Kommo CRM and Aloware.

Its objective is to ensure consistent, accurate, and traceable synchronization of information across both platforms by documenting every field involved in the integration.

---

# Scope

This specification covers:

- Contact fields
- Lead fields
- Ownership fields
- Communication fields
- Custom fields
- Data transformations
- Synchronization direction
- Validation rules

---

# Mapping Principles

The field mapping follows these principles:

- Preserve data integrity.
- Avoid unnecessary duplication.
- Respect each platform's System of Record.
- Reuse existing fields whenever possible.
- Minimize data transformation.
- Maintain identifier traceability.

---

# Systems of Record

| Entity | System of Record |
|---------|------------------|
| Contacts | Kommo |
| Leads | Kommo |
| Pipelines | Kommo |
| Pipeline Stages | Kommo |
| Users | Kommo |
| Agents | Aloware |
| Calls | Aloware |
| SMS | Aloware |
| Call Recordings | Aloware |
| AI Summaries | Aloware |

---

# Contact Field Mapping

| Kommo Field | Aloware Field | Direction | Transformation | Required |
|--------------|---------------|-----------|----------------|----------|
| Contact ID | External Reference | Kommo → Aloware | None | ✅ |
| Name | Name | Kommo → Aloware | None | ✅ |
| Phone | Phone Number | Kommo → Aloware | Normalize E.164 | ✅ |
| Email | Email | Kommo → Aloware | None | Optional |
| Responsible User | Assigned Agent | Kommo → Aloware | Agent Mapping | ✅ |

---

# Lead Field Mapping

| Kommo Field | Aloware Field | Direction | Transformation | Required |
|--------------|---------------|-----------|----------------|----------|
| Lead ID | External Lead Reference | Kommo → Aloware | None | ✅ |
| Lead Name | Notes / Reference | Kommo → Aloware | None | Optional |
| Pipeline | Campaign / List Selection | Kommo → Aloware | Stage Mapping | ✅ |
| Stage | Trigger Action | Kommo → Aloware | Business Rule | ✅ |

---

# Ownership Mapping

| Kommo | Aloware | Transformation |
|--------|----------|----------------|
| Responsible User ID | Agent ID | Agent Mapping Table |
| Responsible User Name | Agent Name | Lookup |

---

# Communication Mapping

The following information is synchronized from Aloware back to Kommo.

| Aloware Field | Kommo Destination | Direction | Notes |
|---------------|-------------------|-----------|-------|
| Call ID | Note | Aloware → Kommo | Reference |
| Call Status | Note | Aloware → Kommo | Human-readable |
| Call Duration | Note | Aloware → Kommo | Seconds |
| Recording URL | Note | Aloware → Kommo | Link |
| AI Summary | Note | Aloware → Kommo | Optional |
| SMS Content | Note | Aloware → Kommo | Optional |
| Event Timestamp | Note | Aloware → Kommo | ISO-8601 |

---

# Custom Field Mapping

Document every custom field used by the integration.

| Kommo Custom Field | Aloware Field | Purpose | Required |
|--------------------|---------------|---------|----------|
| Aloware Contact ID | Contact ID | Cross-reference | ✅ |
| Last Call Date | Call Date | Reporting | Optional |
| Last Call Status | Call Status | Reporting | Optional |

---

# Data Transformations

The following transformations are applied during synchronization.

| Data Type | Transformation |
|-----------|----------------|
| Phone Number | Normalize to E.164 format |
| Date/Time | Convert to ISO-8601 |
| Boolean | Convert to platform-specific format |
| Empty Values | Ignore unless required |
| Text | Trim leading/trailing spaces |
| URLs | Preserve original value |

---

# Validation Rules

Before synchronization, the following validations must be satisfied.

| Validation | Action if Invalid |
|------------|-------------------|
| Phone Number Present | Reject |
| Phone Number Valid | Reject |
| Contact Exists | Create or Update |
| Agent Mapping Exists | Stop Processing |
| Required Field Missing | Reject |
| Invalid Data Type | Reject |

---

# Synchronization Rules

| Rule | Description |
|------|-------------|
| Contacts originate in Kommo | Kommo is the authoritative source for contact information. |
| Communication originates in Aloware | Calls, SMS, recordings, and AI summaries are owned by Aloware. |
| No bidirectional ownership | A field has only one authoritative source. |
| IDs are never modified | External identifiers remain immutable after creation. |

---

# Error Handling

| Condition | Action |
|-----------|--------|
| Missing Required Field | Stop synchronization |
| Invalid Phone Number | Log error and reject |
| Missing Agent Mapping | Stop processing |
| Missing Stage Mapping | Stop processing |
| Duplicate Record | Update existing record |
| API Validation Error | Retry according to Retry Strategy |

---

# Mapping Dependencies

The following specifications must exist before implementation.

- Stage Mapping Specification
- Agent Mapping Specification
- Custom Fields Specification
- Tags & Labels Specification

---

# Validation Checklist

- [ ] All required fields identified
- [ ] Field ownership defined
- [ ] Transformations documented
- [ ] Validation rules documented
- [ ] Synchronization direction defined
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
| Field Mapping Completed | ☐ Yes ☐ No |
| Ready for Implementation | ☐ Yes ☐ No |