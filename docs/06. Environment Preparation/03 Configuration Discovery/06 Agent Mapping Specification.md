# Agent Mapping Specification

**Version:** 1.0

**Status:** Pending

**Phase:** 3.3 — Configuration Discovery

---

# Purpose

This document defines how Kommo users are mapped to Aloware agents.

Its objective is to ensure that lead ownership in Kommo is consistently translated into agent assignment within Aloware, enabling calls, SMS, and other communication activities to be routed to the correct representative.

---

# Scope

This specification covers:

- Kommo users
- Aloware agents
- User-to-agent mappings
- Assignment rules
- Ownership synchronization
- Validation requirements
- Error handling

---

# Mapping Principles

The agent mapping follows these principles:

- Each Kommo user maps to a single Aloware agent.
- Lead ownership remains managed by Kommo.
- Aloware assignments are derived from Kommo ownership.
- Mappings are explicit and documented.
- Agent identifiers remain immutable after configuration.

---

# Ownership Model

| Entity | System of Record |
|---------|------------------|
| Lead Owner | Kommo |
| Contact Owner | Kommo |
| Assigned Agent | Aloware |

---

# Agent Mapping Table

Document every user participating in the integration.

| Kommo User ID | Kommo User | Aloware Agent ID | Aloware Agent | Active | Default Assignment |
|---------------|------------|------------------|---------------|--------|--------------------|
| | | | | ☐ | ☐ |

---

# Assignment Rules

Define how the integration determines the assigned Aloware agent.

| Rule | Description |
|------|-------------|
| Existing Mapping | Assign the mapped Aloware agent. |
| User Not Mapped | Stop processing and log an error. |
| Inactive Agent | Stop processing until a valid mapping exists. |
| Lead Reassigned | Update the assigned agent in Aloware if required by business rules. |
| Default Assignment Enabled | Assign the configured default agent when applicable. |

---

# Synchronization Rules

| Rule | Description |
|------|-------------|
| Kommo is authoritative | Responsible users are managed exclusively in Kommo. |
| Assignment is one-way | User assignments flow from Kommo to Aloware only. |
| No reverse synchronization | Agent changes in Aloware do not update Kommo ownership. |
| One user per agent | Each Kommo user should map to one Aloware agent. |

---

# Validation Rules

Before assigning an agent, the following validations must pass.

| Validation | Action if Invalid |
|------------|-------------------|
| Responsible User Exists | Stop processing |
| User Mapping Exists | Stop processing |
| Agent Exists | Stop processing |
| Agent Active | Stop processing |
| Duplicate Mapping | Reject configuration |

---

# Default Assignment

If the customer chooses to use a fallback agent, document it here.

| Item | Value |
|------|-------|
| Default Agent Enabled | ☐ Yes ☐ No |
| Default Agent ID | |
| Default Agent Name | |
| Business Justification | |

---

# Exception Handling

| Scenario | Action |
|----------|--------|
| No Responsible User | Reject synchronization |
| User Mapping Missing | Log error and stop |
| Agent Inactive | Log error and stop |
| Agent Deleted | Log error and stop |
| Duplicate Agent Mapping | Reject configuration until corrected |

---

# Mapping Dependencies

This specification depends on:

- Kommo Configuration Inventory
- Aloware Configuration Inventory
- Field Mapping Specification
- Stage Mapping Specification

---

# Validation Checklist

- [ ] All Kommo users identified
- [ ] All Aloware agents identified
- [ ] User-to-agent mappings documented
- [ ] Default assignment configured (if applicable)
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
| Agent Mapping Completed | ☐ Yes ☐ No |
| Ready for Implementation | ☐ Yes ☐ No |