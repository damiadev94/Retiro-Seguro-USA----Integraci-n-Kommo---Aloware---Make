# Metadata

| Property | Value |
|----------|-------|
| SOP ID | SOP-KOM-005 |
| Title | Update Lead |
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

This Standard Operating Procedure (SOP) defines the standardized process for updating existing Leads in Kommo using the REST API.

The objective is to ensure that Lead information is modified in a controlled, consistent, and auditable manner while preserving data integrity, preventing unintended data loss, and supporting reliable synchronization across integrated systems.

This procedure applies to partial updates of existing Lead records and follows the principle of modifying only the fields required by the triggering business event.

---

# Scope

This procedure applies to any integration that needs to update existing Lead records in Kommo.

Typical use cases include:

- Pipeline stage updates
- Responsible user assignment
- Lead status synchronization
- Custom field updates
- Tag management
- Integration metadata updates
- External identifier synchronization
- Communication status updates
- Business attribute synchronization

This SOP does not cover:

- Lead creation
- Lead deletion
- Contact updates
- Note creation
- Bulk data migration
- Pipeline configuration

---

# Prerequisites

Before starting this procedure, verify that:

- OAuth authentication has been completed successfully.
- A valid Access Token is available.
- The Kommo account is accessible.
- The integration has permission to update Leads.
- The target Lead exists.
- The Lead ID is available.
- The fields requiring modification have been identified.
- HTTPS connectivity is available.

---

# Inputs

| Input | Required | Description |
|---------|----------|-------------|
| Access Token | Yes | OAuth access token |
| Account Domain | Yes | Kommo account domain |
| Lead ID | Yes | Identifier of the Lead to update |
| Fields to Update | Yes | One or more Lead attributes to modify |
| Custom Field Values | Optional | Updated custom field values |
| Pipeline ID | Optional | Target pipeline |
| Stage ID | Optional | Target stage |
| Responsible User ID | Optional | Assigned owner |
| Tags | Optional | Updated tag collection |
| External Identifier | Optional | Third-party identifier |
| Update Timestamp | Optional | Event timestamp |

---

# Procedure

## 1. Validate Authentication

Verify that:

- Access Token is valid.
- OAuth session is active.
- Required permissions are available.

If authentication fails, execute **SOP-KOM-001 OAuth Authentication** before continuing.

---

## 2. Verify Lead Existence

Confirm that the Lead exists before attempting any modification.

Recommended validation includes:

- Search by Lead ID.
- Verify ownership.
- Confirm accessibility.
- Confirm the Lead has not been deleted.

If necessary, execute **SOP-KOM-003 Search Lead**.

---

## 3. Identify Required Changes

Determine exactly which fields require modification.

Typical fields include:

- Pipeline
- Stage
- Responsible User
- Price
- Tags
- Custom Fields
- Name
- External Identifiers

Only update fields affected by the triggering business event.

---

## 4. Validate Update Data

Verify that:

- Required fields are present.
- Field values are valid.
- Enumerated values exist.
- Pipeline and Stage relationship is valid.
- Responsible User exists.
- Custom Field values comply with expected formats.

Reject invalid update requests before sending them to Kommo.

---

## 5. Preserve Existing Data

Review the current Lead data before applying updates.

Ensure that:

- Unchanged fields remain untouched.
- Existing values are not overwritten unintentionally.
- Integration-specific metadata is preserved.
- Required relationships remain intact.

Avoid replacing entire objects when only partial updates are required.

---

## 6. Build the Update Request

Construct the API request.

Verify that:

- Correct REST endpoint is used.
- HTTPS is enabled.
- Authorization header is included.
- JSON payload is valid.
- Only required fields are included.
- Lead ID is correct.

---

## 7. Submit the Update

Send the request to the Kommo REST API.

Monitor:

- HTTP status code
- Request completion
- Authentication status
- API response
- Network connectivity

Avoid repeated submissions before evaluating the API response.

---

## 8. Validate the Response

Verify that:

- HTTP success status is returned.
- Response body is valid.
- Updated Lead identifier matches the requested Lead.
- Returned values reflect the requested modifications.
- No validation errors are reported.

Reject incomplete or malformed responses.

---

## 9. Verify Updated Information

When required, retrieve the Lead after the update.

Confirm that:

- Requested fields were updated.
- Unmodified fields remain unchanged.
- Pipeline and Stage are correct.
- Responsible User is correct.
- Custom Fields contain expected values.
- Integration metadata is preserved.

---

## 10. Record Operational Information

Record the update operation.

Recommended information includes:

- Lead ID
- Updated fields
- Execution timestamp
- Integration identifier
- Processing status
- Response identifier

Sensitive business information should not be unnecessarily logged.

---

## 11. Return the Result

Return the outcome to the calling workflow.

Possible outcomes include:

- Lead Updated
- Validation Failed
- Lead Not Found
- Authentication Failed
- Update Failed

Include the Lead identifier and update status whenever possible.

---

# Validation

The procedure is considered successful when:

- Authentication succeeded.
- Target Lead exists.
- Update payload passed validation.
- API request completed successfully.
- HTTP success response was received.
- Requested fields were updated correctly.
- No unintended data modifications occurred.

---

# Expected Result

Upon successful completion:

- The Lead contains the updated information.
- Only intended fields have been modified.
- Existing business data has been preserved.
- Integration metadata remains consistent.
- Downstream workflows can continue using the updated Lead.

---

# Common Errors

| Error | Possible Cause | Resolution |
|---------|----------------|------------|
| Unauthorized (401) | Invalid or expired Access Token | Refresh OAuth credentials |
| Forbidden (403) | Missing update permissions | Review OAuth scopes |
| Lead Not Found | Invalid Lead ID | Verify Lead identifier |
| Invalid Stage | Stage does not belong to Pipeline | Validate Stage mapping |
| Invalid Responsible User | User does not exist | Verify User ID |
| Invalid Custom Field | Incorrect field identifier or value | Validate Custom Field configuration |
| Validation Failed | Invalid payload | Correct request data |
| Rate Limit Reached | Excessive API requests | Retry after waiting |
| Request Timeout | Network issue | Retry according to retry policy |
| Internal Server Error | Temporary platform issue | Retry after verification |

---

# Troubleshooting

| Issue | Diagnostic Action | Resolution |
|--------|-------------------|------------|
| Lead not updated | Verify API response | Correct validation errors |
| Incorrect fields modified | Compare payload with expected changes | Send only required fields |
| Stage update rejected | Verify Pipeline and Stage relationship | Correct mapping |
| Responsible User not assigned | Validate User ID | Update mapping configuration |
| Custom Field update fails | Verify field identifier and format | Correct payload |
| Duplicate update execution | Review retry logic | Implement idempotent processing |
| Authentication errors | Validate OAuth session | Re-authenticate |
| Unexpected API response | Inspect response payload | Retry after validation |

---

# Rollback

If the update procedure cannot be completed successfully:

1. Stop downstream processing.
2. Record the failure in operational logs.
3. Discard invalid update payloads.
4. Verify authentication status.
5. Validate Lead existence.
6. Correct payload validation issues.
7. Retry only if permitted by retry policy.

If an incorrect update has already been applied:

1. Retrieve the previous Lead state if available.
2. Determine the affected fields.
3. Restore the correct values through a controlled update.
4. Record the corrective action.
5. Verify that downstream integrations remain consistent.

---

# Best Practices

- Always verify that the Lead exists before updating it.
- Prefer partial updates over full object replacement.
- Modify only fields affected by the business event.
- Validate all identifiers before submission.
- Verify Pipeline and Stage consistency.
- Preserve existing Custom Field values whenever possible.
- Prevent duplicate updates using idempotent workflows.
- Validate API responses before continuing execution.
- Log operational events without exposing sensitive business data.
- Respect API rate limits.
- Maintain synchronization with the authoritative source system.
- Test update workflows in a non-production environment before deployment.

---

# References

- Kommo REST API Documentation
- Kommo Leads API Documentation
- SOP-KOM-001 OAuth Authentication
- SOP-KOM-003 Search Lead
- SOP-HTTP-001 HTTP Request Standards
- SOP-HTTP-002 HTTP Response Validation
- SOP-MAKE-001 HTTP Module Configuration
- Internal Integration Standards

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | YYYY-MM-DD | Integration Documentation Framework | Initial version |