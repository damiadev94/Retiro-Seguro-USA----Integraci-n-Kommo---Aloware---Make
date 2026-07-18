# Custom Fields Specification

**Version:** 1.0

**Status:** Pending

**Phase:** 3.3 — Configuration Discovery

---

# Purpose

This document defines the custom fields required for the Kommo ↔ Aloware integration.

Its objective is to identify, document, and standardize all customer-specific fields used to store integration data, ensuring consistent synchronization, traceability, and reporting across both platforms.

---

# Scope

This specification covers:

- Existing custom fields
- Required custom fields
- Field ownership
- Field data types
- Synchronization rules
- Validation requirements
- Field creation requirements

---

# Field Design Principles

Custom fields should follow these principles:

- Create custom fields only when standard fields are insufficient.
- Each field must have a single business purpose.
- Avoid duplicate information.
- Store integration identifiers separately from business data.
- Maintain compatibility with future integrations.

---

# Systems of Record

| Field Category | System of Record |
|---------------|------------------|
| CRM Business Data | Kommo |
| Communication Data | Aloware |
| Integration Identifiers | Kommo |
| Reporting Fields | Kommo |

---

# Existing Custom Fields

Document any custom fields already available in the customer's Kommo account.

| Field ID | Field Name | Entity | Type | Required | Used by Integration |
|----------|------------|--------|------|----------|---------------------|
| | | Lead / Contact | | ☐ | ☐ |

---

# Required Custom Fields

The following fields are recommended for the integration.

| Field Name | Entity | Type | Required | Purpose |
|------------|--------|------|----------|---------|
| Aloware Contact ID | Contact | Text | ✅ | Stores the unique Aloware Contact Identifier |
| Last Call Date | Contact | Date/Time | Optional | Reporting and visibility |
| Last Call Status | Contact | Text | Optional | Displays latest call outcome |
| Last SMS Date | Contact | Date/Time | Optional | SMS reporting |
| Last Communication Source | Contact | Text | Optional | Indicates the latest communication channel |

---

# Field Definitions

## Aloware Contact ID

| Property | Value |
|----------|-------|
| Entity | Contact |
| Data Type | Text |
| Required | Yes |
| System of Record | Kommo |
| Synchronization | Kommo ↔ Aloware |
| Editable by Users | No |

**Purpose**

Stores the unique identifier assigned by Aloware to maintain a persistent relationship between both platforms.

---

## Last Call Date

| Property | Value |
|----------|-------|
| Entity | Contact |
| Data Type | Date/Time |
| Required | No |
| System of Record | Aloware |
| Synchronization | Aloware → Kommo |

**Purpose**

Stores the timestamp of the most recent completed call.

---

## Last Call Status

| Property | Value |
|----------|-------|
| Entity | Contact |
| Data Type | Text |
| Required | No |
| System of Record | Aloware |
| Synchronization | Aloware → Kommo |

**Purpose**

Stores the outcome of the most recent call (e.g., Answered, No Answer, Voicemail).

---

## Last SMS Date

| Property | Value |
|----------|-------|
| Entity | Contact |
| Data Type | Date/Time |
| Required | No |
| System of Record | Aloware |
| Synchronization | Aloware → Kommo |

**Purpose**

Stores the timestamp of the latest SMS interaction.

---

## Last Communication Source

| Property | Value |
|----------|-------|
| Entity | Contact |
| Data Type | Text |
| Required | No |
| System of Record | Aloware |
| Synchronization | Aloware → Kommo |

**Purpose**

Indicates the communication channel responsible for the latest customer interaction (Call, SMS, etc.).

---

# Field Synchronization

| Field | Direction | Update Rule |
|-------|-----------|-------------|
| Aloware Contact ID | Kommo ↔ Aloware | Set once after contact creation |
| Last Call Date | Aloware → Kommo | Update after completed call |
| Last Call Status | Aloware → Kommo | Update after completed call |
| Last SMS Date | Aloware → Kommo | Update after SMS event |
| Last Communication Source | Aloware → Kommo | Update after every communication event |

---

# Validation Rules

| Validation | Action if Invalid |
|------------|-------------------|
| Required Field Missing | Stop processing |
| Invalid Data Type | Reject update |
| Duplicate Identifier | Reject configuration |
| Empty Integration Identifier | Stop synchronization |
| Invalid Date Format | Reject update |

---

# Field Creation Requirements

Before implementation, verify:

- [ ] Required fields already exist
- [ ] Missing fields have been created
- [ ] Correct data types configured
- [ ] Field visibility configured
- [ ] Field permissions configured
- [ ] API accessibility verified

---

# Dependencies

This specification depends on:

- Kommo Configuration Inventory
- Field Mapping Specification
- Stage Mapping Specification
- Agent Mapping Specification

---

# Validation Checklist

- [ ] Existing custom fields inventoried
- [ ] Required custom fields identified
- [ ] Field purposes documented
- [ ] Synchronization rules defined
- [ ] Validation rules documented
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
| Custom Fields Specification Completed | ☐ Yes ☐ No |
| Ready for Implementation | ☐ Yes ☐ No |