# Metadata

| Property | Value |
|----------|-------|
| SOP ID | SOP-KOM-002 |
| Title | Search Contact |
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

This Standard Operating Procedure (SOP) defines the standardized process for searching existing contacts in Kommo using the REST API.

The objective is to reliably locate contact records before performing any operation that depends on an existing contact, such as updates, note creation, synchronization, ownership validation, or relationship management.

Searching for a contact before creating or updating records helps prevent duplicate data, preserves data integrity, and supports idempotent integration workflows.

---

# Scope

This procedure applies to any integration that needs to retrieve an existing contact from Kommo.

Typical use cases include:

- Synchronization workflows
- Contact validation
- Duplicate detection
- Lead association
- Contact updates
- Custom field retrieval
- External identifier lookup
- CRM enrichment
- Event processing
- Pre-validation before API operations

This SOP does not cover:

- Contact creation
- Contact updates
- Lead searches
- Note creation
- Webhook processing

---

# Prerequisites

Before starting this procedure, verify that:

- OAuth authentication has been completed successfully.
- A valid Access Token is available.
- The Kommo account is accessible.
- The integration has permission to read Contacts.
- HTTPS connectivity is available.
- Search criteria have been identified.
- Required identifiers are available whenever possible.

---

# Inputs

| Input | Required | Description |
|---------|----------|-------------|
| Access Token | Yes | OAuth access token |
| Account Domain | Yes | Kommo account domain |
| Search Value | Yes | Value used to locate the contact |
| Search Field | Yes | Contact attribute used for searching |
| Expected Contact Identifier | Optional | Existing Contact ID if known |
| External Identifier | Optional | Third-party reference stored in Kommo |
| Phone Number | Optional | Contact phone number |
| Email Address | Optional | Contact email |
| Custom Field Value | Optional | Integration-specific identifier |

---

# Procedure

## 1. Validate Authentication

Verify that:

- Access Token is valid.
- OAuth session is active.
- Required permissions are available.

If authentication fails, execute **SOP-KOM-001 OAuth Authentication** before continuing.

---

## 2. Identify the Search Strategy

Determine the most reliable search criterion.

Preferred search order:

1. Contact ID
2. External Identifier
3. Custom Field
4. Phone Number
5. Email Address
6. Contact Name

Avoid using names as the primary identifier whenever a unique identifier exists.

---

## 3. Normalize Search Data

Before executing the request:

- Remove leading and trailing spaces.
- Normalize phone number format.
- Validate email syntax.
- Remove unsupported characters.
- Ensure identifiers use the expected format.
- Apply any required business normalization rules.

Consistent normalization improves search accuracy.

---

## 4. Build the Search Request

Construct the API request using the selected search criterion.

Verify that:

- Correct API endpoint is used.
- HTTPS is enabled.
- Authorization header is included.
- Query parameters are properly encoded.
- Pagination parameters are defined when required.

---

## 5. Execute the Search

Submit the search request to Kommo.

Monitor:

- HTTP status code
- Response time
- Request completion
- Network connectivity
- Authentication status

Do not assume that a successful HTTP response indicates that a matching contact was found.

---

## 6. Validate the Response

Verify that:

- HTTP 200 OK is returned.
- Response format is valid.
- Response body is complete.
- Contact collection is present.
- No API errors are reported.

Reject incomplete or malformed responses.

---

## 7. Evaluate Search Results

Determine the outcome.

Possible outcomes include:

- Exactly one contact found
- Multiple contacts found
- No contacts found

Each outcome should be handled according to the integration business rules.

---

## 8. Resolve Duplicate Matches

If multiple contacts are returned:

- Compare Contact IDs.
- Compare phone numbers.
- Compare email addresses.
- Compare external identifiers.
- Compare custom fields.
- Apply duplicate resolution rules.

Do not arbitrarily select the first returned record.

---

## 9. Validate Contact Data

For the selected contact, verify that required information exists.

Typical validation includes:

- Contact ID
- Name
- Phone numbers
- Email addresses
- Responsible User
- Tags
- Custom Fields
- Creation date
- Last updated date

Additional validation may be required by the business process.

---

## 10. Store Required Information

Record only the information required by downstream processes.

Commonly stored values include:

- Contact ID
- External Identifier
- Responsible User ID
- Custom Field values
- Phone number
- Email address

Avoid persisting unnecessary personal information.

---

## 11. Return the Result

Provide the search result to the calling process.

Possible outcomes:

- Contact Found
- Multiple Contacts Found
- Contact Not Found
- Search Failed

The returned result should include sufficient metadata for subsequent workflow decisions.

---

# Validation

The procedure is considered successful when:

- Authentication succeeded.
- Search request completed successfully.
- Response was received.
- Response structure is valid.
- Matching contact was correctly identified.
- Required contact information has been validated.
- Search outcome has been returned to the calling process.

---

# Expected Result

Upon successful completion:

- The requested contact has been identified or confirmed as absent.
- Duplicate detection has been performed when applicable.
- Required identifiers have been collected.
- Downstream processes have the information necessary to continue safely.
- No duplicate contact has been created as part of the search process.

---

# Common Errors

| Error | Possible Cause | Resolution |
|---------|----------------|------------|
| Unauthorized (401) | Invalid or expired Access Token | Refresh or regenerate OAuth credentials |
| Forbidden (403) | Missing API permissions | Review granted OAuth scopes |
| Contact Not Found | Search value does not exist | Verify search criteria |
| Multiple Results Returned | Duplicate records exist | Apply duplicate resolution rules |
| Invalid Search Parameter | Unsupported query format | Validate request construction |
| Empty Response | No matching records | Confirm input values |
| Malformed Response | API communication problem | Retry request and validate response |
| Timeout | Network issue or slow API | Retry according to retry policy |
| Rate Limit Reached | Excessive API requests | Respect rate limits and retry later |
| Invalid Phone Format | Search value not normalized | Normalize phone number before searching |

---

# Troubleshooting

| Issue | Diagnostic Action | Resolution |
|--------|-------------------|------------|
| Search returns no results | Verify search value | Retry with normalized input |
| Duplicate contacts returned | Inspect identifiers and custom fields | Apply duplicate handling policy |
| Incorrect contact selected | Review matching rules | Strengthen search criteria |
| Search by phone fails | Verify international format | Normalize phone number |
| Search by email fails | Validate email syntax | Retry using normalized email |
| Authentication errors occur | Verify OAuth session | Execute authentication procedure |
| API response is incomplete | Inspect response payload | Retry request if appropriate |
| Slow searches | Review filters and pagination | Optimize search strategy |

---

# Rollback

If the search procedure cannot be completed successfully:

1. Discard incomplete search results.
2. Do not cache invalid responses.
3. Clear temporary search variables.
4. Record the failure in integration logs.
5. Verify authentication status.
6. Validate search parameters.
7. Retry the search if permitted by the retry policy.
8. Escalate persistent failures according to operational procedures.

Since this procedure is read-only, no changes are made to Kommo data and no platform rollback is required.

---

# Best Practices

- Search before creating contacts.
- Prefer immutable identifiers over names.
- Use Contact ID whenever available.
- Normalize search values before querying.
- Validate API responses before processing.
- Handle duplicate results explicitly.
- Avoid assumptions when multiple matches exist.
- Cache identifiers only when appropriate.
- Log search outcomes without exposing sensitive data.
- Respect API rate limits.
- Minimize unnecessary search requests.
- Design workflows to be idempotent.

---

# References

- Kommo REST API Documentation
- Kommo Contacts API Documentation
- SOP-KOM-001 OAuth Authentication
- SOP-HTTP-001 HTTP Request Standards
- SOP-HTTP-002 HTTP Response Validation
- SOP-MAKE-001 HTTP Module Configuration
- Internal Integration Standards

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | YYYY-MM-DD | Integration Documentation Framework | Initial version |