# Tags & Labels Specification

**Version:** 1.0

**Status:** Pending

**Phase:** 3.3 — Configuration Discovery

---

# Purpose

This document defines the tags and labels used by the Kommo ↔ Aloware integration.

Its objective is to standardize the use of tags for classification, filtering, reporting, and automation while ensuring they are applied consistently throughout the integration.

---

# Scope

This specification covers:

- Existing tags
- Required tags
- Tag ownership
- Tag application rules
- Automation rules
- Naming conventions
- Validation requirements

---

# Tagging Principles

Tags should follow these principles:

- Each tag must have a single business purpose.
- Tags classify information but do not represent workflow states.
- Workflow progression must be managed through pipeline stages, not tags.
- Tags should be reusable across automations whenever possible.
- Naming should be consistent and easily understood by business users.

---

# Systems of Record

| Category | System of Record |
|----------|------------------|
| CRM Tags | Kommo |
| Communication Metadata | Aloware |
| Integration Tags | Kommo |

---

# Existing Tags

Document all tags currently configured in Kommo.

| Tag ID | Tag Name | Description | Used by Integration |
|--------|----------|-------------|---------------------|
| | | | ☐ |

---

# Required Tags

Document tags required for the integration.

| Tag Name | Purpose | Required |
|----------|---------|----------|
| Imported from Aloware | Identifies contacts synchronized from Aloware | Optional |
| Power Dialer | Indicates the contact has been added to a Power Dialer list | Optional |
| Call Completed | Indicates a completed call has been processed | Optional |
| SMS Sent | Indicates an SMS interaction has been synchronized | Optional |
| Integration Error | Identifies records requiring manual review | Optional |

> **Note:** These tags are examples. The final list should be validated with the customer and aligned with existing CRM conventions.

---

# Tag Definitions

## Imported from Aloware

| Property | Value |
|----------|-------|
| Platform | Kommo |
| Applied By | Make |
| Purpose | Identify contacts originating from Aloware synchronization |
| Removed Automatically | No |

---

## Power Dialer

| Property | Value |
|----------|-------|
| Platform | Kommo |
| Applied By | Make |
| Purpose | Indicate the contact has been assigned to a Power Dialer list |
| Removed Automatically | Optional |

---

## Call Completed

| Property | Value |
|----------|-------|
| Platform | Kommo |
| Applied By | Make |
| Purpose | Indicate a completed call has been synchronized |
| Removed Automatically | Optional |

---

## SMS Sent

| Property | Value |
|----------|-------|
| Platform | Kommo |
| Applied By | Make |
| Purpose | Indicate an SMS interaction has been synchronized |
| Removed Automatically | Optional |

---

## Integration Error

| Property | Value |
|----------|-------|
| Platform | Kommo |
| Applied By | Make |
| Purpose | Flag records requiring manual intervention |
| Removed Automatically | After issue resolution |

---

# Tag Application Rules

| Event | Tag Applied |
|------|-------------|
| Contact created in Aloware | Imported from Aloware |
| Contact added to Power Dialer | Power Dialer |
| Call completed | Call Completed |
| SMS synchronized | SMS Sent |
| Synchronization failure | Integration Error |

---

# Tag Removal Rules

| Tag | Removal Condition |
|-----|-------------------|
| Imported from Aloware | Never removed unless contact is archived |
| Power Dialer | Contact removed from dialing workflow (if applicable) |
| Call Completed | Normally retained |
| SMS Sent | Normally retained |
| Integration Error | Issue resolved and synchronization completed successfully |

---

# Naming Conventions

Tags should follow these conventions:

- Use descriptive business names.
- Avoid abbreviations unless widely understood.
- Use Title Case.
- Avoid duplicate meanings.
- Keep names concise and consistent.

**Examples**

| Recommended | Avoid |
|-------------|-------|
| Call Completed | CALL_DONE |
| Power Dialer | PD |
| Integration Error | ERR_01 |

---

# Validation Rules

| Validation | Action if Invalid |
|------------|-------------------|
| Duplicate Tag | Reject configuration |
| Undefined Tag | Do not apply |
| Missing Required Tag | Log warning |
| Invalid Tag Name | Rename before implementation |

---

# Dependencies

This specification depends on:

- Kommo Configuration Inventory
- Field Mapping Specification
- Stage Mapping Specification
- Agent Mapping Specification

---

# Validation Checklist

- [ ] Existing tags inventoried
- [ ] Required tags identified
- [ ] Tag purposes documented
- [ ] Application rules defined
- [ ] Removal rules defined
- [ ] Naming conventions validated
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
| Tags & Labels Specification Completed | ☐ Yes ☐ No |
| Ready for Implementation | ☐ Yes ☐ No |