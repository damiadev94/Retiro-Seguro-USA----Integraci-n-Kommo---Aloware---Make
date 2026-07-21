# Metadata

| Property | Value |
|----------|-------|
| SOP ID | SOP-KOM-006 |
| Title | Update Contact |
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

This Standard Operating Procedure (SOP) defines the standardized process for updating existing Contacts in Kommo using the REST API.

The objective is to ensure that Contact information is updated consistently, accurately, and securely while preserving existing customer data, maintaining synchronization between systems, and preventing unintended modifications.

This procedure supports incremental updates and follows the principle of modifying only the attributes affected by the triggering business event.

---

# Scope

This procedure applies to any integration that updates Contact records in Kommo.

Typical use cases include:

- Contact information synchronization
- Phone number updates
- Email address updates
- Responsible user reassignment
- Custom Field synchronization
- Tag management
- External identifier synchronization
- Customer profile enrichment
- Communication preference updates
- Integration metadata updates

This SOP does not cover:

- Contact creation
- Contact deletion
- Lead updates
- Note creation
- Bulk data migration
- Contact searches

---

# Prerequisites

Before starting this procedure, verify that:

- OAuth authentication has been completed successfully.
- A valid Access Token is available.
- The Kommo account is accessible.
- The integration has permission to update Contacts.
- The target Contact exists.
- The Contact ID is available.
- The fields requiring modification have been identified.
- HTTPS connectivity is available.

---

# Inputs

| Input | Required | Description |
|---------|----------|-------------|
| Access Token | Yes | OAuth access token |
| Account Domain | Yes | Kommo account domain |
| Contact ID | Yes | Identifier of the Contact to update |
| Fields to Update | Yes | One or more Contact attributes to modify |
| Name | Optional | Updated Contact name |
| Phone Numbers | Optional | Updated phone numbers |
| Email Addresses | Optional | Updated email addresses |
| Responsible User ID | Optional | Assigned owner |
| Custom Field Values | Optional | Updated custom field values |
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

## 2. Verify Contact Existence

Confirm that the Contact exists before applying any modifications.

Recommended validation includes:

- Search by Contact ID.
- Verify ownership.
- Confirm accessibility.
- Confirm the Contact has not been deleted.

If necessary, execute **SOP-KOM-002 Search Contact**.

---

## 3. Identify Required Changes

Determine which Contact attributes require modification.

Typical fields include:

- Name
- Phone Numbers
- Email Addresses
- Responsible User
- Tags
- Custom Fields
- External Identifiers

Only modify fields affected by the triggering business event.

---

## 4. Validate Update Data

Verify that:

- Required fields are present.
- Phone numbers follow the expected format.
- Email addresses are syntactically valid.
- Responsible User exists.
- Custom Field values are valid.
- Required identifiers are available.
- Enumerated values are supported.

Reject invalid update requests before submitting them to the API.

---

## 5. Preserve Existing Data

Review the current Contact information before updating.

Ensure that:

- Existing values are preserved unless intentionally modified.
- Integration metadata is retained.
- Related business information is not overwritten.
- Partial updates do not remove existing information unintentionally.

Avoid replacing complete objects when only a subset of attributes has changed.

---

## 6. Build the Update Request

Construct the API request.

Verify that:

- Correct REST endpoint is used.
- HTTPS is enabled.
- Authorization header is included.
- JSON payload is valid.
- Only intended fields are included.
- Contact ID is correct.

---

## 7. Submit the Update

Send the request to the Kommo REST API.

Monitor:

- HTTP status code
- Request completion
- Authentication status
- API response
- Network connectivity

Avoid duplicate submissions before evaluating the response.

---

## 8. Validate the Response

Verify that:

- HTTP success status is returned.
- Response body is valid.
- Returned Contact ID matches the requested Contact.
- Updated values reflect the requested modifications.
- No validation errors are reported.

Reject incomplete or malformed responses.

---

## 9. Verify Updated Information

When appropriate, retrieve the Contact after the update.

Confirm that:

- Requested fields have been updated.
- Existing values remain intact.
- Phone numbers are correct.
- Email addresses are correct.
- Responsible User assignment is correct.
- Custom Fields contain expected values.
- Integration metadata has been preserved.

---

## 10. Record Operational Information

Record the successful update.

Recommended information includes:

- Contact ID
- Updated fields
- Execution timestamp
- Integration identifier
- Processing status
- Response identifier

Sensitive customer information should not be unnecessarily logged.

---

## 11. Return the Result

Return the operation outcome to the calling workflow.

Possible outcomes include:

- Contact Updated
- Validation Failed
- Contact Not Found
- Authentication Failed
- Update Failed

Include the Contact identifier and processing status whenever possible.

---

# Validation

The procedure is considered successful when:

- Authentication succeeded.
- Target Contact exists.
- Update payload passed validation.
- API request completed successfully.
- HTTP success response was received.
- Requested fields were updated correctly.
- Existing Contact information remained intact.

---

# Expected Result

Upon successful completion:

- The Contact contains the updated information.
- Only intended fields have been modified.
- Existing customer information has been preserved.
- Integration metadata remains consistent.
- Downstream workflows can continue using the updated Contact.

---

# Common Errors

| Error | Possible Cause | Resolution |
|---------|----------------|------------|
| Unauthorized (401) | Invalid or expired Access Token | Refresh OAuth credentials |
| Forbidden (403) | Missing update permissions | Review OAuth scopes |
| Contact Not Found | Invalid Contact ID | Verify Contact identifier |
| Invalid Phone Number | Incorrect phone format | Normalize phone number |
| Invalid Email Address | Invalid email syntax | Correct email format |
| Invalid Responsible User | User does not exist | Verify User ID |
| Invalid Custom Field | Incorrect field identifier or value | Validate Custom Field configuration |
| Validation Failed | Invalid payload | Correct request data |
| Rate Limit Reached | Excessive API requests | Retry after waiting |
| Request Timeout | Network issue | Retry according to retry policy |

---

# Troubleshooting

| Issue | Diagnostic Action | Resolution |
|--------|-------------------|------------|
| Contact not updated | Verify API response | Correct validation errors |
| Phone number not updated | Review normalization rules | Correct phone format |
| Email update rejected | Validate email syntax | Correct input value |
| Responsible User not assigned | Verify User ID | Update mapping configuration |
| Custom Field update fails | Validate field identifier and value | Correct payload |
| Duplicate update execution | Inspect retry logic | Implement idempotency controls |
| Authentication failures | Validate OAuth session | Re-authenticate |
| Unexpected API response | Inspect response payload | Retry after validation |

---

# Rollback

If the update procedure cannot be completed successfully:

1. Stop downstream processing.
2. Record the failure in operational logs.
3. Discard invalid update payloads.
4. Verify authentication status.
5. Validate Contact existence.
6. Correct payload validation issues.
7. Retry only if permitted by retry policy.

If an incorrect update has already been applied:

1. Retrieve the previous Contact state if available.
2. Determine the affected fields.
3. Restore the correct values through a controlled update.
4. Record the corrective action.
5. Verify downstream system consistency.

---

# Best Practices

- Always verify that the Contact exists before updating it.
- Use Contact ID as the primary identifier.
- Prefer partial updates over full object replacement.
- Normalize phone numbers before submission.
- Validate email addresses before updating.
- Modify only the fields affected by the business event.
- Preserve existing customer information whenever possible.
- Validate Custom Field values before submission.
- Prevent duplicate updates through idempotent workflows.
- Validate API responses before continuing execution.
- Respect API rate limits.
- Test update workflows in a non-production environment before deployment.

---

# References

- Kommo REST API Documentation
- Kommo Contacts API Documentation
- SOP-KOM-001 OAuth Authentication
- SOP-KOM-002 Search Contact
- SOP-HTTP-001 HTTP Request Standards
- SOP-HTTP-002 HTTP Response Validation
- SOP-MAKE-001 HTTP Module Configuration
- Internal Integration Standards

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | YYYY-MM-DD | Integration Documentation Framework | Initial version |