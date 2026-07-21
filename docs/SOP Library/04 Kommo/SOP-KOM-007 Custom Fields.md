# Metadata

| Property | Value |
|----------|-------|
| SOP ID | SOP-KOM-007 |
| Title | Custom Fields |
| Domain | 04 Kommo |
| Platform | Kommo CRM |
| API Version | REST API v4 |
| Authentication Method | OAuth 2.0 |
| Version | 1.0 |
| Status | Approved |
| Owner | Integration Documentation Framework |
| Last Updated | YYYY-MM-DD |

---

# Purpose

This Standard Operating Procedure (SOP) defines the standardized process for working with Custom Fields in Kommo using the REST API.

The objective is to ensure that custom data is consistently identified, validated, mapped, and maintained across integrations while preserving data integrity, preventing mapping errors, and supporting long-term maintainability.

Custom Fields should be treated as stable integration interfaces between Kommo and external systems.

---

# Scope

This procedure applies to any integration that reads, writes, validates, or synchronizes Custom Fields within Kommo.

Typical use cases include:

- External system identifiers
- Synchronization metadata
- Business-specific attributes
- Integration status
- AI-generated information
- Communication metadata
- Mapping external references
- Workflow state tracking
- Data enrichment
- Operational flags

This SOP does not cover:

- Standard Kommo fields
- Lead creation
- Contact creation
- OAuth authentication
- Webhook configuration

---

# Prerequisites

Before starting this procedure, verify that:

- OAuth authentication has been completed successfully.
- A valid Access Token is available.
- The Kommo account is accessible.
- The integration has permission to read Custom Fields.
- Required entities exist.
- Required Custom Fields have been created.
- Field identifiers are documented.
- HTTPS connectivity is available.

---

# Inputs

| Input | Required | Description |
|---------|----------|-------------|
| Access Token | Yes | OAuth access token |
| Account Domain | Yes | Kommo account domain |
| Entity Type | Yes | Lead, Contact, Company, Customer, etc. |
| Entity ID | Optional | Target entity identifier |
| Custom Field ID | Optional | Kommo Custom Field identifier |
| Custom Field Code | Optional | System field code if available |
| Custom Field Name | Optional | Display name |
| Custom Field Value | Optional | Value to read or write |
| External Identifier | Optional | Identifier from another system |

---

# Procedure

## 1. Validate Authentication

Verify that:

- Access Token is valid.
- OAuth session is active.
- Required permissions are available.

If authentication fails, execute **SOP-KOM-001 OAuth Authentication** before continuing.

---

## 2. Identify the Target Entity

Determine the entity containing the Custom Field.

Supported entities commonly include:

- Leads
- Contacts
- Companies
- Customers

Confirm that the entity exists before attempting to read or update Custom Fields.

---

## 3. Discover Available Custom Fields

Retrieve the available Custom Fields for the target entity.

Verify:

- Field ID
- Field Name
- Field Code
- Field Type
- Allowed Values
- Required Status

Always use the API as the authoritative source for field definitions.

---

## 4. Identify the Required Custom Field

Locate the required field using one of the following identifiers, in order of preference:

1. Field ID
2. Field Code
3. Field Name

Avoid relying solely on display names, as they may change over time.

---

## 5. Validate Field Configuration

Verify that:

- The field exists.
- The field belongs to the expected entity.
- The field type matches the expected value.
- The field is active.
- Required permissions are available.

Do not continue if field configuration does not match integration requirements.

---

## 6. Validate Field Value

Before writing data, verify that:

- Data type is correct.
- Enumerated values exist.
- Numeric values are valid.
- Date formats are supported.
- Boolean values are correctly represented.
- Multi-select values are valid.
- Required values are present.

Reject invalid values before submitting the request.

---

## 7. Build the API Request

Construct the request using:

- Correct REST endpoint
- HTTPS
- Authorization header
- Entity identifier
- Custom Field identifier
- Validated field value

Verify that the payload follows the Kommo API specification.

---

## 8. Submit the Request

Execute the API request.

Monitor:

- HTTP status code
- Authentication status
- Request completion
- API response
- Network connectivity

Avoid retrying immediately without analyzing the failure.

---

## 9. Validate the Response

Verify that:

- HTTP success status is returned.
- Response body is valid.
- Updated value matches the requested value.
- No validation errors are reported.
- Field identifier is correct.

Reject incomplete or malformed responses.

---

## 10. Verify Data Persistence

Retrieve the entity when appropriate.

Confirm that:

- The Custom Field contains the expected value.
- Existing fields remain unchanged.
- No unintended modifications occurred.
- Related integration metadata remains intact.

---

## 11. Record Operational Information

Record the successful operation.

Recommended information includes:

- Entity ID
- Custom Field ID
- Field Name
- Operation performed
- Execution timestamp
- Integration identifier
- Processing status

Sensitive business information should not be unnecessarily logged.

---

## 12. Return the Result

Return the outcome to the calling workflow.

Possible outcomes include:

- Custom Field Read Successfully
- Custom Field Updated Successfully
- Field Not Found
- Validation Failed
- Authentication Failed
- Request Failed

Include entity and field identifiers whenever possible.

---

# Validation

The procedure is considered successful when:

- Authentication succeeded.
- Target entity exists.
- Required Custom Field was identified.
- Field configuration is valid.
- Field value passed validation.
- API request completed successfully.
- Expected value is stored or retrieved correctly.

---

# Expected Result

Upon successful completion:

- The required Custom Field has been correctly identified.
- Field values have been validated.
- Data has been successfully read or updated.
- Integration mappings remain consistent.
- Business data integrity has been preserved.

---

# Common Errors

| Error | Possible Cause | Resolution |
|---------|----------------|------------|
| Unauthorized (401) | Invalid or expired Access Token | Refresh OAuth credentials |
| Forbidden (403) | Missing permissions | Review OAuth scopes |
| Custom Field Not Found | Incorrect Field ID | Verify field configuration |
| Invalid Field Type | Incorrect value type | Validate payload |
| Invalid Enumeration Value | Unsupported option | Use allowed values only |
| Entity Not Found | Invalid entity identifier | Verify entity exists |
| Validation Failed | Invalid payload | Correct request data |
| Rate Limit Reached | Too many requests | Retry later |
| Request Timeout | Network issue | Retry according to retry policy |
| Internal Server Error | Temporary platform issue | Retry after verification |

---

# Troubleshooting

| Issue | Diagnostic Action | Resolution |
|--------|-------------------|------------|
| Field cannot be located | Retrieve available Custom Fields | Update mapping configuration |
| Field value rejected | Verify data type | Correct value format |
| Enumeration update fails | Compare against allowed values | Use valid option |
| Incorrect field updated | Verify Field ID | Update field mapping |
| Value not persisted | Retrieve entity again | Retry after validation |
| Authentication failure | Validate OAuth session | Re-authenticate |
| Unexpected API response | Inspect payload | Correct request |
| Duplicate updates | Review retry logic | Implement idempotency |

---

# Rollback

If the procedure cannot be completed successfully:

1. Stop downstream processing.
2. Record the failure in operational logs.
3. Discard invalid payloads.
4. Verify authentication status.
5. Validate field configuration.
6. Correct validation errors.
7. Retry only if permitted by retry policy.

If an incorrect Custom Field value has already been stored:

1. Retrieve the previous entity state if available.
2. Identify affected fields.
3. Restore the previous value through a controlled update.
4. Record the corrective action.
5. Verify downstream synchronization.

---

# Best Practices

- Use Custom Field IDs whenever possible.
- Avoid relying on display names.
- Document every integration field mapping.
- Validate field types before writing data.
- Normalize values before submission.
- Use immutable external identifiers.
- Minimize unnecessary Custom Fields.
- Preserve existing values during partial updates.
- Validate API responses before continuing workflow execution.
- Prevent duplicate updates through idempotent workflows.
- Respect API rate limits.
- Periodically review Custom Field definitions to ensure compatibility with integration requirements.

---

# References

- Kommo REST API Documentation
- Kommo Custom Fields API Documentation
- SOP-KOM-001 OAuth Authentication
- SOP-KOM-002 Search Contact
- SOP-KOM-003 Search Lead
- SOP-KOM-005 Update Lead
- SOP-KOM-006 Update Contact
- SOP-HTTP-001 HTTP Request Standards
- SOP-HTTP-002 HTTP Response Validation
- SOP-MAKE-001 HTTP Module Configuration
- Internal Integration Standards

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | YYYY-MM-DD | Integration Documentation Framework | Initial version |