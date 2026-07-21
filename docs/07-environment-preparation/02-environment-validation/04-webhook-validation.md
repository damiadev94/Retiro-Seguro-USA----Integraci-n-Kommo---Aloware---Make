# Webhook Validation

**Version:** 1.0

**Status:** Pending

**Phase:** 3.2 — Environment Validation

---

# Purpose

This document validates webhook communication between Kommo, Make, and Aloware.

The objective is to verify that webhook events are correctly generated, delivered, received, and processed before implementation begins.

This validation focuses exclusively on webhook communication and event delivery. API connectivity and authentication are validated in separate documents.

---

# Scope

Platforms included:

- Kommo CRM
- Make
- Aloware

---

# Validation Objectives

- Verify webhook generation.
- Verify webhook delivery.
- Verify payload integrity.
- Verify HTTP responses.
- Verify event processing.
- Detect delivery failures before implementation.

---

# Validation Environment

| Item | Value |
|------|-------|
| Environment | Development / Production |
| Validation Date | |
| Integration Engineer | |
| Make Workspace | |

---

# Kommo → Make Validation

## Webhook Configuration

| Item | Value |
|------|-------|
| Webhook URL | |
| Events Configured | |
| Authentication | |

---

## Validation Tests

| Test | Expected Result | Actual Result | Status |
|------|-----------------|---------------|--------|
| Lead Created | Webhook Received | | ☐ |
| Lead Updated | Webhook Received | | ☐ |
| Lead Stage Changed | Webhook Received | | ☐ |
| Contact Updated | Webhook Received | | ☐ |
| HTTP Response | 200 OK | | ☐ |
| Payload Complete | Yes | | ☐ |

---

## Payload Validation

| Validation | Status |
|------------|--------|
| Event Type Present | ☐ |
| Lead ID Present | ☐ |
| Contact ID Present | ☐ |
| Pipeline Information Present | ☐ |
| Stage Information Present | ☐ |
| Timestamp Present | ☐ |

---

## Result

| Item | Status |
|------|--------|
| Webhook Received | ☐ |
| Payload Valid | ☐ |
| Validation Passed | ☐ |

---

# Aloware → Make Validation

## Webhook Configuration

| Item | Value |
|------|-------|
| Webhook URL | |
| Events Configured | |
| Authentication | |

---

## Validation Tests

| Test | Expected Result | Actual Result | Status |
|------|-----------------|---------------|--------|
| Call Completed | Webhook Received | | ☐ |
| SMS Sent | Webhook Received | | ☐ |
| Contact Updated | Webhook Received | | ☐ |
| AI Summary Generated | Webhook Received | | ☐ |
| HTTP Response | 200 OK | | ☐ |
| Payload Complete | Yes | | ☐ |

---

## Payload Validation

| Validation | Status |
|------------|--------|
| Event Type Present | ☐ |
| Contact ID Present | ☐ |
| Agent Information Present | ☐ |
| Call Information Present | ☐ |
| AI Summary Present (if applicable) | ☐ |
| Timestamp Present | ☐ |

---

## Result

| Item | Status |
|------|--------|
| Webhook Received | ☐ |
| Payload Valid | ☐ |
| Validation Passed | ☐ |

---

# Make Webhook Processing

## Validation Tests

| Test | Expected Result | Actual Result | Status |
|------|-----------------|---------------|--------|
| Incoming Webhook Triggered | Success | | ☐ |
| Payload Parsed | Success | | ☐ |
| Variables Extracted | Success | | ☐ |
| Scenario Started | Success | | ☐ |
| Execution Logged | Success | | ☐ |

---

## Result

| Item | Status |
|------|--------|
| Processing Successful | ☐ |
| Scenario Triggered | ☐ |
| Validation Passed | ☐ |

---

# Cross-Platform Event Validation

| Event Flow | Expected Result | Actual Result | Status |
|------------|-----------------|---------------|--------|
| Kommo → Make | Success | | ☐ |
| Aloware → Make | Success | | ☐ |
| Duplicate Events Handled | Success | | ☐ |
| Invalid Payload Rejected | Success | | ☐ |

---

# Validation Summary

| Platform | Status |
|----------|--------|
| Kommo Webhooks | ☐ Passed ☐ Failed |
| Aloware Webhooks | ☐ Passed ☐ Failed |
| Make Processing | ☐ Passed ☐ Failed |
| Cross-Platform Validation | ☐ Passed ☐ Failed |

---

# Issues Identified

| ID | Description | Severity | Resolution |
|----|-------------|----------|------------|
| | | Low / Medium / High | |

---

# Observations

-

---

# Recommendations

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
| Webhooks Successfully Validated | ☐ Yes ☐ No |
| Blocking Issues Remaining | ☐ Yes ☐ No |
| Environment Ready | ☐ Yes ☐ No |