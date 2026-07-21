# Technical Discovery Workbook

## Kommo ↔ Aloware ↔ Make

**Project:** Bidirectional Integration (Kommo ↔ Aloware)
**Purpose:** Technical discovery and configuration inventory prior to implementation.

---

# Project Information

| Field        | Value                |
| ------------ | -------------------- |
| Client       |                      |
| Environment  | Production / Sandbox |
| Date         |                      |
| Performed by |                      |
| Version      | v1.0                 |

---

# 1. Executive Summary

## Objective

Describe the business objective of the integration.

> ---

---

## Platforms

| Platform | Access Verified |
| -------- | --------------- |
| Kommo    | ☐               |
| Aloware  | ☐               |
| Make     | ☐               |

---

# 2. Aloware Discovery

## 2.1 API

| Item                   | Value |
| ---------------------- | ----- |
| Base URL               |       |
| API Version            |       |
| Authentication         |       |
| API Token Owner        |       |
| Token Retrieved        | ☐     |
| Documentation Reviewed | ☐     |

### Notes

---

## 2.2 Authentication

| Property     | Value            |
| ------------ | ---------------- |
| Method       | API Token        |
| Parameter    | api_token        |
| OAuth        | No               |
| Bearer       | No               |
| Content-Type | application/json |
| Accept       | application/json |

### Validation

* [ ] Token tested
* [ ] Successful request
* [ ] Unauthorized request tested
* [ ] Invalid token tested

---

## 2.3 Contact Object

### Endpoint

| Property        | Value |
| --------------- | ----- |
| Endpoint        |       |
| HTTP Method     | POST  |
| Supports Create | ☐     |
| Supports Update | ☐     |
| Upsert          | ☐     |

---

### Required Fields

| Field        | Required |
| ------------ | -------- |
| api_token    | ✅        |
| phone_number | ✅        |

---

### Optional Fields

| Field        | Used | Notes |
| ------------ | ---- | ----- |
| name         |      |       |
| first_name   |      |       |
| last_name    |      |       |
| email        |      |       |
| company_name |      |       |
| notes        |      |       |
| timezone     |      |       |
| address      |      |       |
| website      |      |       |
| lead_source  |      |       |
| csf1         |      |       |
| csf2         |      |       |

---

### Relationship Fields

| Object             | ID |
| ------------------ | -- |
| User               |    |
| Ring Group         |    |
| Sequence           |    |
| Line               |    |
| Tag                |    |
| Disposition Status |    |

---

## 2.4 Lists

| List Name | List ID | API | Description |
| --------- | ------- | --- | ----------- |
|           |         |     |             |

---

## 2.5 Users

| Name | User ID | Role | Active |
| ---- | ------- | ---- | ------ |
|      |         |      |        |

---

## 2.6 Ring Groups

| Name | ID | Users |
| ---- | -- | ----- |
|      |    |       |

---

## 2.7 Sequences

| Name | ID | Description |
| ---- | -- | ----------- |
|      |    |             |

---

## 2.8 Tags

| Tag | ID |
| --- | -- |
|     |    |

---

## 2.9 Disposition Status

| Name | ID |
| ---- | -- |
|      |    |

---

## 2.10 Lines

| Name | Line ID | Phone Number |
| ---- | ------- | ------------ |
|      |         |              |

---

## 2.11 Campaigns

| Campaign | Type | Notes |
| -------- | ---- | ----- |
|          |      |       |

Questions to answer:

* How are contacts added?
* How do campaigns start?
* Are Lists required?
* Is PowerDialer mandatory?
* What triggers outbound calls?

---

## 2.12 Webhooks

| Event           | Available | Payload Reviewed | Notes |
| --------------- | --------- | ---------------- | ----- |
| Contact Created |           |                  |       |
| Contact Updated |           |                  |       |
| Call Started    |           |                  |       |
| Call Ended      |           |                  |       |
| SMS Sent        |           |                  |       |
| SMS Received    |           |                  |       |

---

## 2.13 Call Logs

| Item          | Verified |
| ------------- | -------- |
| Endpoint      |          |
| Recording URL |          |
| Duration      |          |
| Disposition   |          |
| Agent         |          |
| Timestamp     |          |

---

## 2.14 Configuration

| Property       | Value |
| -------------- | ----- |
| Timezone       |       |
| Caller IDs     |       |
| Phone Numbers  |       |
| Business Hours |       |

---

# 3. Kommo Discovery

## 3.1 Pipelines

| Pipeline | ID |
| -------- | -- |
|          |    |

---

## 3.2 Stages

| Stage | ID |
| ----- | -- |
|       |    |

---

## 3.3 Custom Fields

| Name | ID | Type | Entity |
| ---- | -- | ---- | ------ |
|      |    |      |        |

---

## 3.4 Users

| Name | User ID | Role |
| ---- | ------- | ---- |
|      |         |      |

---

## 3.5 Tags

| Name | ID |
| ---- | -- |
|      |    |

---

## 3.6 Webhooks

| Event | Destination | Active |
| ----- | ----------- | ------ |
|       |             |        |

---

## 3.7 Installed Integrations

| Integration | Active | Notes |
| ----------- | ------ | ----- |
|             |        |       |

---

## 3.8 Business Process

Describe the real sales flow.

```text
Lead Created

↓

Stage 1

↓

Stage 2

↓

Stage 3

↓

Won / Lost
```

---

# 4. Make Discovery

## Workspace

| Property     | Value |
| ------------ | ----- |
| Organization |       |
| Team         |       |
| Owner        |       |

---

## Connections

| Connection | Status |
| ---------- | ------ |
| Kommo      |        |
| Aloware    |        |
| HTTP       |        |
| Other      |        |

---

## Scenarios

| Scenario | Trigger | Status | Notes |
| -------- | ------- | ------ | ----- |
|          |         |        |       |

---

## Webhooks

| Name | URL | Used By |
| ---- | --- | ------- |
|      |     |         |

---

## Variables

| Variable | Description |
| -------- | ----------- |
|          |             |

---

## Data Stores

| Name | Purpose |
| ---- | ------- |
|      |         |

---

# 5. Integration Mapping

## Kommo → Aloware

| Kommo Field | Aloware Field | Notes |
| ----------- | ------------- | ----- |
|             |               |       |

---

## Aloware → Kommo

| Aloware Field | Kommo Field | Notes |
| ------------- | ----------- | ----- |
|               |             |       |

---

# 6. Functional Validation

| Test                      | Result | Notes |
| ------------------------- | ------ | ----- |
| Create Lead in Kommo      | ☐      |       |
| Move Stage                | ☐      |       |
| Create Contact in Aloware | ☐      |       |
| Assign User               | ☐      |       |
| Add to List               | ☐      |       |
| Add to PowerDialer        | ☐      |       |
| Make Call                 | ☐      |       |
| Change Disposition        | ☐      |       |
| Receive Webhook           | ☐      |       |
| Update Kommo              | ☐      |       |

---

# 7. Risks & Findings

## Risks

| Risk | Impact | Mitigation |
| ---- | ------ | ---------- |
|      |        |            |

---

## Missing Information

* ☐
* ☐
* ☐

---

## Questions for Client

* ☐
* ☐
* ☐

---

# 8. Final Inventory

## Credentials

| System      | Status |
| ----------- | ------ |
| Kommo API   | ☐      |
| Aloware API | ☐      |
| Make        | ☐      |

---

## IDs Collected

| Entity             | Status |
| ------------------ | ------ |
| Pipeline           | ☐      |
| Stages             | ☐      |
| Users              | ☐      |
| Tags               | ☐      |
| Lists              | ☐      |
| Ring Groups        | ☐      |
| Sequences          | ☐      |
| Disposition Status | ☐      |
| Lines              | ☐      |

---

## Documentation Completed

* [ ] APIs
* [ ] Authentication
* [ ] Webhooks
* [ ] API Objects
* [ ] API Endpoints
* [ ] Data Mapping
* [ ] Business Rules
* [ ] Functional Analysis
* [ ] Technical Analysis
* [ ] Technical Constraints
* [ ] Technical Risks
* [ ] Test Plan
* [ ] Deployment Checklist

---

# 9. Sign-off

| Item                         | Completed |
| ---------------------------- | --------- |
| Technical Discovery Finished | ☐         |
| All IDs Collected            | ☐         |
| APIs Validated               | ☐         |
| Mapping Completed            | ☐         |
| Ready for Implementation     | ☐         |
