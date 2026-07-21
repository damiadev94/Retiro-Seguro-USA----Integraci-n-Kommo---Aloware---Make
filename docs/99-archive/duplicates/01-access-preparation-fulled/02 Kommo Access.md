# Kommo Access

**Version:** 1.0

**Status:** Pending

**Phase:** 3.1 — Environment Preparation

---

# Purpose

This document records all access information, credentials, permissions, and configuration required to integrate Kommo CRM with Make.

All fields should be completed and validated before implementation begins.

---

# Workspace Information

| Field | Value | Status |
|-------|-------|--------|
| Workspace Name | Damian Tecnico Externo | ■ |
| Workspace URL | https://retirosegurousa.kommo.com | ■ |
| Subdomain | retirosegurousa | ■ |
| Account ID | 35128700 | ■ |
| Region | US | ■ |

---

# Administrator Information

| Field | Value | Status |
|-------|-------|--------|
| Administrator Name | Damian Tecnico Externo | ■ |
| Administrator Email | damian_l@hotmail.es | ■ |
| User ID | 15581551 | ■ |
| Role | Administrador | ■ |
| Admin Permissions Verified | | ■ |

---

# OAuth Integration (PENDIENTE)

| Field | Value | Status |
|-------|-------|--------|
| Integration Name | | ☐ |
| Integration ID (Client ID) | | ☐ |
| Client Secret | | ☐ |
| Redirect URI | | ☐ |
| Authorization URL | | ☐ |
| Access Token | | ☐ |
| Refresh Token | | ☐ |
| Token Expiration | | ☐ |

---

# OAuth Scopes (PENDIENTE)

| Scope | Required | Granted |
|--------|----------|---------|
| Leads | ☑ | ☐ |
| Contacts | ☑ | ☐ |
| Companies | ☑ | ☐ |
| Tasks | ☑ | ☐ |
| Notes | ☑ | ☐ |
| Users | ☑ | ☐ |
| Pipelines | ☑ | ☐ |
| Catalogs | ☐ | ☐ |
| Custom Fields | ☑ | ☐ |
| Webhooks | ☑ | ☐ |

---

# API Configuration

| Field | Value | Status |
|-------|-------|--------|
| API Base URL | https://retirosegurousa.kommo.com | ■ |
| API Version | v4 | ■ |
| Authentication Method | OAuth 2.0 | ■ |
| REST API Accessible | PENDIENTE | ☐ |

---

# Webhook Configuration

| Field | Value | Status |
|-------|-------|--------|
| Webhook URL | | ☐ |
| Webhook Secret | | ☐ |
| Webhook Permissions | | ☐ |
| Webhook Created | | ☐ |

---

# Business Objects Validation

| Object | Accessible | Notes |
|----------|------------|-------|
| Leads | ■ | |
| Contacts | ■ | |
| Companies | ■ | |
| Pipelines | ■ | |
| Stages | ■ | |
| Users | ■ | User IDs are not displayed in the Kommo UI. They are obtained through the REST API. |
| Custom Fields | ⚠ Partial | Fields are visible, but the current user cannot manage them. The settings gear is not available. Validation pending with an administrator account or via REST API. |
| Tasks | N/A | Not required for this integration. Validation skipped. |
| Notes | ⏳ Pending | Se validará mediante la API durante la configuración OAuth. |

---

# API Validation

| Validation | Status | Notes |
|------------|--------|-------|
| Authentication | ☐ | |
| Get Account | ☐ | |
| List Pipelines | ☐ | |
| List Stages | ☐ | |
| List Users | ☐ | |
| List Custom Fields | ☐ | |
| Get Lead | ☐ | |
| Update Lead | ☐ | |
| Create Note | ☐ | |

---

# Required Information from Customer

## Credentials

- [x] Workspace URL
- [x] Administrator Account
- [ ] OAuth Integration
- [ ] Client ID
- [ ] Client Secret

## Permissions

- [x] Administrator Access
- [ ] API Access
- [ ] Webhook Management
- [x] Integration Management

---

# Environment Checklist

| Item | Status |
|------|--------|
| Workspace Verified | ☐ |
| Administrator Verified | ☐ |
| OAuth Configured | ☐ |
| Tokens Generated | ☐ |
| API Accessible | ☐ |
| Permissions Validated | ☐ |
| Webhooks Ready | ☐ |
| Environment Ready | ☐ |

---

# Notes

## Known Issues

-

## Pending Actions

-

## Customer Comments

-

---

# Approval

| Role | Name | Date |
|------|------|------|
| Customer | | |
| Integration Engineer | | |