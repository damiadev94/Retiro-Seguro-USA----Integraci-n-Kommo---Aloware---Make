# Metadata

| Property | Value |
|----------|-------|
| SOP ID | SOP-KOM-004 |
| Title | Create Note |
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

This Standard Operating Procedure (SOP) defines the standardized process for creating Notes in Kommo using the REST API.

The objective is to consistently record activities, synchronization events, communication summaries, and operational information within CRM entities while preserving data integrity, traceability, and auditability.

This SOP ensures that all integrations create Notes using a predictable structure and consistent operational practices.

---

# Scope

This procedure applies to any integration that needs to create Notes associated with Kommo entities.

Typical use cases include:

- Call summaries
- SMS summaries
- AI-generated conversation summaries
- Integration event logging
- Synchronization notifications
- Operational audit records
- External system activity
- Workflow completion records
- Error notifications
- Customer interaction history

This SOP does not cover:

- Updating existing Notes
- Deleting Notes
- Searching Notes
- Lead creation
- Contact creation
- Webhook configuration

---

# Prerequisites

Before starting this procedure, verify that:

- OAuth authentication has been completed successfully.
- A valid Access Token is available.
- The Kommo account is accessible.
- The integration has permission to create Notes.
- The target entity exists.
- The target entity identifier is available.
- The Note content has been prepared.
- HTTPS connectivity is available.

---

# Inputs

| Input | Required | Description |
|---------|----------|-------------|
| Access Token | Yes | OAuth access token |
| Account Domain | Yes | Kommo account domain |
| Entity Type | Yes | CRM entity receiving the Note |
| Entity ID | Yes | Identifier of the target entity |
| Note Type | Yes | Kommo Note type |
| Note Content | Yes | Text to be stored in the Note |
| Author Information | Optional | Integration or user responsible for the Note |
| Event Timestamp | Optional | Original event date and time |
| External Reference | Optional | Identifier from the originating system |
| Metadata | Optional | Additional structured information |

---

# Procedure

## 1. Validate Authentication

Verify that:

- Access Token is valid.
- OAuth session is active.
- Required permissions are available.

If authentication fails, execute **SOP-KOM-001 OAuth Authentication** before continuing.

---

## 2. Validate Target Entity

Confirm that the target entity exists.

Supported entity types commonly include:

- Lead
- Contact
- Company
- Customer

Verify:

- Entity ID is valid.
- Entity exists.
- Entity is accessible.
- Entity has not been deleted.

Do not create Notes for non-existent entities.

---

## 3. Determine the Appropriate Note Type

Select the appropriate Note type according to the business event.

Examples include:

- Common Note
- Call Activity
- SMS Activity
- Integration Event
- System Notification
- Operational Log

The selected Note type should accurately represent the event being recorded.

---

## 4. Prepare Note Content

Create clear, concise, and meaningful content.

The Note should include only relevant business information.

When applicable, include:

- Event description
- Activity summary
- Communication outcome
- External reference
- Timestamp
- Integration source

Avoid unnecessary repetition or verbose text.

---

## 5. Validate Note Content

Before submission, verify that:

- Content is complete.
- Required information is present.
- Unsupported characters are removed.
- Text encoding is valid.
- Length complies with platform limitations.
- Sensitive information is not exposed.

Do not include credentials, access tokens, or confidential system information.

---

## 6. Build the API Request

Construct the request using:

- Correct REST endpoint
- HTTPS
- Authorization header
- JSON payload
- Entity identifier
- Note type
- Prepared content

Verify that the payload conforms to the Kommo API specification.

---

## 7. Submit the Request

Send the request to the Kommo REST API.

Monitor:

- HTTP status code
- Request completion
- API response
- Network connectivity
- Authentication status

Do not retry immediately without evaluating the failure reason.

---

## 8. Validate the Response

Verify that:

- HTTP success status is returned.
- Response body is valid.
- Note identifier has been generated.
- Entity association is correct.
- No validation errors are reported.

Reject incomplete or malformed responses.

---

## 9. Confirm Note Creation

Retrieve the created Note when appropriate.

Verify:

- Note exists.
- Content matches the submitted information.
- Correct entity association.
- Timestamp is correct.
- Note type is correct.

This validation is recommended for critical integrations.

---

## 10. Record Operational Information

Record the successful operation.

Recommended operational information includes:

- Entity ID
- Note ID
- Event type
- Creation timestamp
- Integration identifier
- Execution status

Do not record confidential business information unnecessarily.

---

## 11. Return the Result

Return the operation outcome to the calling process.

Possible outcomes include:

- Note Created
- Validation Failed
- Entity Not Found
- Authentication Failed
- Request Failed

The result should include the Note identifier whenever available.

---

# Validation

The procedure is considered successful when:

- Authentication succeeded.
- Target entity exists.
- Note content passed validation.
- API request completed successfully.
- HTTP success response was received.
- Note identifier was returned.
- Note is correctly associated with the target entity.

---

# Expected Result

Upon successful completion:

- A new Note has been created.
- The Note is associated with the correct CRM entity.
- Business or operational information has been recorded.
- The creation has been confirmed by the API.
- Downstream workflows can reference the newly created Note.

---

# Common Errors

| Error | Possible Cause | Resolution |
|---------|----------------|------------|
| Unauthorized (401) | Invalid or expired Access Token | Refresh OAuth credentials |
| Forbidden (403) | Missing permissions | Review OAuth scopes |
| Entity Not Found | Invalid Entity ID | Verify target entity |
| Invalid Note Type | Unsupported Note type | Use a supported value |
| Invalid Payload | Malformed JSON | Validate request body |
| Validation Failed | Missing required fields | Complete payload |
| Request Timeout | Network issue | Retry according to retry policy |
| Rate Limit Reached | Too many requests | Wait before retrying |
| Empty Content | Missing Note text | Provide valid content |
| Internal Server Error | Temporary platform issue | Retry after verification |

---

# Troubleshooting

| Issue | Diagnostic Action | Resolution |
|--------|-------------------|------------|
| Note not created | Verify API response | Correct validation errors |
| Incorrect entity association | Validate Entity ID | Retry with correct identifier |
| Content appears truncated | Review payload size | Reduce content length |
| Formatting is incorrect | Verify text encoding | Normalize content |
| Duplicate Notes created | Inspect retry logic | Implement idempotency controls |
| Authentication failure | Validate OAuth session | Re-authenticate |
| Unexpected API response | Inspect returned payload | Retry after validation |
| Slow API response | Review network connectivity | Retry according to operational policy |

---

# Rollback

If the procedure cannot be completed successfully:

1. Stop downstream processing.
2. Discard temporary Note payloads.
3. Record the failure in operational logs.
4. Verify authentication status.
5. Validate the target entity.
6. Correct payload validation errors.
7. Retry only if permitted by retry policy.

If a duplicate or incorrect Note has been created:

1. Record the incident.
2. Follow organizational procedures for Note correction or removal.
3. Verify that downstream workflows are not affected.
4. Update operational records accordingly.

---

# Best Practices

- Always verify the target entity before creating a Note.
- Record meaningful business events only.
- Keep Note content concise and structured.
- Include external references when applicable.
- Avoid storing sensitive information.
- Standardize Note formatting across integrations.
- Validate payloads before submission.
- Prevent duplicate Note creation through idempotent workflows.
- Log successful operations without exposing confidential data.
- Respect API rate limits.
- Use consistent timestamps across integrated systems.
- Validate API responses before continuing workflow execution.

---

# References

- Kommo REST API Documentation
- Kommo Notes API Documentation
- SOP-KOM-001 OAuth Authentication
- SOP-KOM-002 Search Contact
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