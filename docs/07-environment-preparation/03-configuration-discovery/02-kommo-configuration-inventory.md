# Kommo Configuration Inventory

**Version:** 1.0

**Status:** Pending

**Phase:** 3.3 — Configuration Discovery

---

# Purpose

This document inventories the current Kommo CRM configuration required for the Kommo ↔ Aloware integration.

Its objective is to document the customer's existing CRM configuration so that all implementation decisions are based on the actual environment.

---

# Scope

This inventory includes:

- Account information
- Pipelines
- Pipeline stages
- Users
- Contacts
- Leads
- Custom fields
- Tags
- Sources
- Webhooks
- API configuration
- Integration settings

---

# Account Information

| Item | Value |
|------|-------|
| Account Name | |
| Account ID | |
| Domain | |
| Region | |
| API Version | v4 |
| Time Zone | |
| Currency | |
| Language | |

---

# Pipelines

Document every sales pipeline used by the customer.

| Pipeline ID | Pipeline Name | Active | Notes |
|-------------|---------------|--------|-------|
| | | ☐ | |

---

# Pipeline Stages

Document every stage that participates in the integration.

| Pipeline | Stage ID | Stage Name | Trigger Integration | Notes |
|----------|----------|------------|---------------------|-------|
| | | | ☐ Yes ☐ No | |

---

# Users

Inventory all users that may own leads or participate in the integration.

| User ID | User Name | Email | Active | Requires Agent Mapping |
|---------|-----------|-------|--------|------------------------|
| | | | ☐ | ☐ |

---

# Lead Configuration

## Lead Status

| Item | Value |
|------|-------|
| Multiple Pipelines Enabled | |
| Required Fields | |
| Lead Sources Used | |

---

## Lead Fields

List all standard lead fields relevant to the integration.

| Field | Used | Notes |
|------|------|-------|
| Name | ☐ | |
| Price | ☐ | |
| Pipeline | ☐ | |
| Stage | ☐ | |
| Responsible User | ☐ | |
| Created Date | ☐ | |
| Updated Date | ☐ | |

---

# Contact Configuration

## Standard Fields

| Field | Used | Notes |
|------|------|-------|
| First Name | ☐ | |
| Last Name | ☐ | |
| Phone | ☐ | |
| Email | ☐ | |

---

# Custom Fields

Document every custom field used by the integration.

| Field ID | Field Name | Entity | Type | Required | Notes |
|----------|------------|--------|------|----------|-------|
| | | Lead / Contact | | ☐ | |

---

# Required Custom Fields

The following custom fields are expected for the integration.

| Field | Entity | Purpose | Exists |
|------|--------|---------|--------|
| Aloware Contact ID | Contact | Stores Aloware Contact Identifier | ☐ |
| Last Call Status | Contact / Lead | Optional | ☐ |
| Last Call Date | Contact / Lead | Optional | ☐ |

---

# Tags

Document tags that participate in the integration.

| Tag ID | Tag Name | Used by Integration | Notes |
|--------|----------|--------------------|-------|
| | | ☐ | |

---

# Sources

Inventory lead sources used by the customer.

| Source | Active | Notes |
|--------|--------|-------|
| | ☐ | |

---

# Webhooks

Document existing outbound webhooks configured in Kommo.

| Event | Endpoint | Active | Notes |
|------|----------|--------|-------|
| | | ☐ | |

---

# API Configuration

| Item | Value |
|------|-------|
| API Version | v4 |
| Authentication Method | OAuth 2.0 |
| Client ID | |
| Redirect URI | |
| Integration ID | |

---

# Permissions

Verify the integration has access to the required resources.

| Resource | Permission Verified |
|----------|---------------------|
| Leads | ☐ |
| Contacts | ☐ |
| Pipelines | ☐ |
| Stages | ☐ |
| Users | ☐ |
| Custom Fields | ☐ |
| Notes | ☐ |
| Webhooks | ☐ |

---

# Business Rules Identified

Document customer-specific rules that affect CRM behavior.

| Rule | Description |
|------|-------------|
| | |

---

# Integration Dependencies

Identify configuration elements required by the integration.

| Dependency | Status |
|------------|--------|
| Pipeline Identified | ☐ |
| Trigger Stages Identified | ☐ |
| Responsible Users Identified | ☐ |
| Custom Fields Identified | ☐ |
| Tags Identified | ☐ |
| Webhooks Configured | ☐ |

---

# Configuration Summary

| Category | Status |
|----------|--------|
| Account Information | ☐ Complete |
| Pipelines | ☐ Complete |
| Stages | ☐ Complete |
| Users | ☐ Complete |
| Contacts | ☐ Complete |
| Leads | ☐ Complete |
| Custom Fields | ☐ Complete |
| Tags | ☐ Complete |
| Webhooks | ☐ Complete |
| API Configuration | ☐ Complete |

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
| Kommo Configuration Fully Documented | ☐ Yes ☐ No |
| Ready for Mapping Specifications | ☐ Yes ☐ No |