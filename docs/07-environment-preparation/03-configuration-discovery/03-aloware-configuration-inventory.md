# Aloware Configuration Inventory

**Version:** 1.0

**Status:** Pending

**Phase:** 3.3 — Configuration Discovery

---

# Purpose

This document inventories the current Aloware configuration required for the Kommo ↔ Aloware integration.

Its objective is to document the customer's communication platform configuration so that the integration can be implemented using the actual production environment.

---

# Scope

This inventory includes:

- Account information
- Users and agents
- Phone numbers
- Teams
- Campaigns
- Power Dialer lists
- Contact configuration
- Call configuration
- SMS configuration
- AI features
- Webhooks
- API configuration
- Integration settings

---

# Account Information

| Item | Value |
|------|-------|
| Account Name | |
| Account ID | |
| Workspace | |
| Region | |
| Time Zone | |
| Language | |
| API Version | |

---

# Agents

Document all agents that participate in the integration.

| Agent ID | Agent Name | Email | Active | Mapped to Kommo User |
|----------|------------|-------|--------|----------------------|
| | | | ☐ | ☐ |

---

# Teams

Document the teams configured in Aloware.

| Team ID | Team Name | Active | Notes |
|---------|-----------|--------|-------|
| | | ☐ | |

---

# Phone Numbers

Inventory all phone numbers available to the account.

| Number ID | Phone Number | Type | Assigned To | Active |
|-----------|--------------|------|-------------|--------|
| | | Local / Toll-Free | | ☐ |

---

# Campaigns

Document campaigns used by the integration.

| Campaign ID | Campaign Name | Active | Notes |
|-------------|---------------|--------|-------|
| | | ☐ | |

---

# Power Dialer Lists

Document all Power Dialer lists that may receive contacts from Kommo.

| List ID | List Name | Campaign | Active | Used by Integration |
|---------|-----------|----------|--------|---------------------|
| | | | ☐ | ☐ |

---

# Contact Configuration

## Standard Contact Fields

| Field | Used | Notes |
|------|------|-------|
| Name | ☐ | |
| Phone Number | ☐ | |
| Email | ☐ | |
| Company | ☐ | |

---

## Custom Contact Fields

| Field ID | Field Name | Type | Required | Notes |
|----------|------------|------|----------|-------|
| | | | ☐ | |

---

# Call Configuration

Document call-related settings relevant to the integration.

| Setting | Value |
|---------|-------|
| Call Recording Enabled | |
| Automatic Call Logging | |
| Call Disposition Required | |
| Voicemail Enabled | |
| Call Duration Tracking | |

---

# SMS Configuration

Document SMS settings used by the customer.

| Setting | Value |
|---------|-------|
| SMS Enabled | |
| Two-Way Messaging | |
| SMS Templates Configured | |
| Automatic SMS Logging | |

---

# AI Features

Document AI capabilities enabled in Aloware.

| Feature | Enabled | Notes |
|---------|---------|-------|
| AI Call Summary | ☐ | |
| AI Transcription | ☐ | |
| AI Sentiment Analysis | ☐ | |
| AI Call Insights | ☐ | |

---

# Webhooks

Document outbound webhooks configured in Aloware.

| Event | Endpoint | Active | Notes |
|------|----------|--------|-------|
| | | ☐ | |

---

# API Configuration

| Item | Value |
|------|-------|
| API Version | |
| Authentication Method | API Key |
| API Base URL | |
| API Key Configured | ☐ |
| Rate Limit | |

---

# Permissions

Verify the API has access to the required resources.

| Resource | Permission Verified |
|----------|---------------------|
| Contacts | ☐ |
| Agents | ☐ |
| Calls | ☐ |
| SMS | ☐ |
| Campaigns | ☐ |
| Lists | ☐ |
| Webhooks | ☐ |

---

# Integration Dependencies

Identify Aloware configuration required for the integration.

| Dependency | Status |
|------------|--------|
| Agents Identified | ☐ |
| Campaigns Identified | ☐ |
| Power Dialer Lists Identified | ☐ |
| Phone Numbers Identified | ☐ |
| AI Features Identified | ☐ |
| Webhooks Configured | ☐ |

---

# Business Rules Identified

Document customer-specific communication rules that affect the integration.

| Rule | Description |
|------|-------------|
| | |

---

# Configuration Summary

| Category | Status |
|----------|--------|
| Account Information | ☐ Complete |
| Agents | ☐ Complete |
| Teams | ☐ Complete |
| Phone Numbers | ☐ Complete |
| Campaigns | ☐ Complete |
| Power Dialer Lists | ☐ Complete |
| Contact Configuration | ☐ Complete |
| Call Configuration | ☐ Complete |
| SMS Configuration | ☐ Complete |
| AI Features | ☐ Complete |
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
| Aloware Configuration Fully Documented | ☐ Yes ☐ No |
| Ready for Mapping Specifications | ☐ Yes ☐ No |