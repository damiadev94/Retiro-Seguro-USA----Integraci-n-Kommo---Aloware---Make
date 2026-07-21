# 04 Kommo

The **Kommo** domain contains the Standard Operating Procedures (SOPs) required to interact with the Kommo CRM platform as part of reusable integration solutions.

These procedures standardize how integrations authenticate, retrieve information, update CRM entities, manage custom fields, and configure event-driven communication through webhooks.

The SOPs contained in this domain are platform-oriented and intentionally independent of any specific customer implementation. They provide repeatable operational procedures that can be reused across projects involving Kommo REST API integrations.

---

# Domain Scope

This domain covers operational procedures related to:

- OAuth 2.0 authentication
- Contact retrieval
- Lead retrieval
- Lead updates
- Contact updates
- Note creation
- Custom field management
- Webhook configuration and validation

The domain assumes that HTTP communication, API fundamentals, and Make platform operations are already covered by the corresponding SOP libraries.

---

# Dependencies

The Kommo SOPs depend on knowledge documented in the following domains:

| Domain | Purpose |
|----------|---------|
| 00 Standards | Documentation standards, naming conventions, error handling, and SOP methodology |
| 01 Infrastructure | Environment preparation, credentials, networking, and access validation |
| 02 HTTP | HTTP methods, headers, authentication concepts, status codes, retries, and request validation |
| 03 Make | HTTP module configuration, connections, variables, routing, logging, and error handling |

---

# Supported Platform

Platform:

- Kommo CRM

Primary Interface:

- REST API v4

Authentication:

- OAuth 2.0

Primary Data Format:

- JSON

Communication Model:

- HTTPS REST API
- Outbound Webhooks

---

# Supported Operations

The SOP library currently standardizes the following platform operations.

| SOP | Description |
|------|-------------|
| SOP-KOM-001 | OAuth Authentication |
| SOP-KOM-002 | Search Contact |
| SOP-KOM-003 | Search Lead |
| SOP-KOM-004 | Create Note |
| SOP-KOM-005 | Update Lead |
| SOP-KOM-006 | Update Contact |
| SOP-KOM-007 | Custom Fields |
| SOP-KOM-008 | Webhooks |

---

# Typical Integration Responsibilities

Within a typical integration architecture, Kommo commonly acts as the commercial System of Record.

Typical responsibilities include:

- Managing contacts
- Managing leads
- Managing companies
- Managing pipelines
- Managing pipeline stages
- Managing responsible users
- Storing customer information
- Recording CRM activities
- Receiving operational notes from external systems
- Triggering business events through webhooks

Business communication systems (telephony, messaging, AI assistants, etc.) should synchronize with Kommo through an integration platform rather than communicating directly with external systems, following an event-driven architecture. This responsibility separation aligns with the architectural principles established for the integration framework. :contentReference[oaicite:0]{index=0}

---

# Platform Concepts

Understanding the following Kommo entities is essential before using the procedures in this domain.

## Contact

Represents an individual person or organization.

Typical attributes include:

- Name
- Phone numbers
- Email addresses
- Custom Fields
- Tags

---

## Lead

Represents a commercial opportunity progressing through a sales pipeline.

Typical attributes include:

- Pipeline
- Stage (Status)
- Responsible User
- Value
- Associated Contacts
- Notes
- Tags
- Custom Fields

---

## Note

Represents an activity recorded on a CRM entity.

Notes are commonly used to record:

- Call summaries
- Integration events
- System notifications
- External activities
- Synchronization logs

---

## Custom Field

A customer-defined field extending the standard Kommo data model.

Custom fields are frequently used for:

- External identifiers
- Synchronization state
- Integration metadata
- Third-party references

---

## Responsible User

The CRM user responsible for managing a lead or contact.

Responsible users are commonly mapped to users or agents in external platforms during integrations.

---

## Pipeline

Represents a commercial workflow.

A pipeline contains multiple stages that model the progression of a sales opportunity.

---

## Stage (Status)

Represents the current state of a Lead within a Pipeline.

Stage changes frequently serve as business events that trigger integration workflows.

---

## Webhook

An outbound HTTP notification automatically sent by Kommo when configured events occur.

Typical webhook events include:

- Lead created
- Lead updated
- Contact updated
- Pipeline stage changed

---

# Operational Principles

All procedures within this domain follow these principles.

- OAuth credentials shall never be exposed in implementation artifacts.
- All API requests shall use HTTPS.
- Authentication shall be validated before executing business operations.
- Requests shall use least-privilege credentials whenever possible.
- API responses shall always be validated before processing.
- Entity identifiers shall be treated as immutable references.
- Update operations shall modify only the required fields.
- Integration logic shall preserve Kommo as the authoritative source for commercial data unless explicitly defined otherwise by the solution architecture.
- Webhook processing shall be designed to tolerate duplicate event delivery.
- All operational errors should be logged using the logging standards defined in the Operations domain.

---

# Recommended Workflow

For new implementations, the SOPs should normally be executed in the following sequence.

1. Complete OAuth Authentication.
2. Validate API connectivity.
3. Search for the required Contact.
4. Search for the required Lead.
5. Retrieve required Custom Fields.
6. Update Contact or Lead when necessary.
7. Create operational Notes.
8. Configure and validate Webhooks.
9. Execute integration testing.

Some implementations may omit specific procedures depending on business requirements.

---

# Out of Scope

This domain does not cover:

- HTTP protocol fundamentals
- OAuth theory
- Make scenario construction
- Business process design
- Customer-specific field mappings
- Pipeline design
- Sales methodology
- Integration architecture
- Platform administration
- User permission management

These topics are documented in other domains of the Integration Documentation Framework.

---

# Related Domains

- 00 Standards
- 01 Infrastructure
- 02 HTTP
- 03 Make
- 05 Aloware
- 06 Testing
- 07 Operations

---

# References

- Kommo REST API Documentation
- Kommo OAuth Documentation
- Kommo Webhooks Documentation
- Internal Integration Standards
- Internal Error Handling Standards
- Internal Logging Standards

---

# Version

| Property | Value |
|----------|-------|
| Domain | 04 Kommo |
| Version | 1.0 |
| Status | Approved |
| Owner | Integration Documentation Framework |
| Last Updated | YYYY-MM-DD |