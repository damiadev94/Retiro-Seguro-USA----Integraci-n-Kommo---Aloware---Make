# Metadata

| Property | Value |
|----------|-------|
| SOP ID | SOP-KOM-003 |
| Title | Search Lead |
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

This Standard Operating Procedure (SOP) defines the standardized process for searching existing Leads in Kommo using the REST API.

The objective is to reliably locate commercial opportunities before executing operations such as updates, stage transitions, ownership validation, note creation, synchronization, or business rule evaluation.

Searching for an existing Lead before performing write operations prevents duplicate records, improves data integrity, and supports deterministic and idempotent integration workflows.

---

# Scope

This procedure applies to any integration that needs to retrieve one or more Leads from Kommo.

Typical use cases include:

- Lead synchronization
- Lead validation
- Pipeline monitoring
- Stage verification
- Ownership validation
- Integration event processing
- CRM enrichment
- Duplicate detection
- Business rule evaluation
- Pre-validation before updates

This SOP does not cover:

- Lead creation
- Lead updates
- Contact searches
- Note creation
- Webhook configuration

---

# Prerequisites

Before starting this procedure, verify that:

- OAuth authentication has been completed successfully.
- A valid Access Token is available.
- The Kommo account is accessible.
- The integration has permission to read Leads.
- HTTPS connectivity is available.
- Search criteria have been identified.
- Required identifiers are available whenever possible.

---

# Inputs

| Input | Required | Description |
|---------|----------|-------------|
| Access Token | Yes | OAuth access token |
| Account Domain | Yes | Kommo account domain |
| Search Value | Yes | Value used to locate the Lead |
| Search Field | Yes | Lead attribute used for searching |
| Lead ID | Optional | Existing Lead identifier |
| Pipeline ID | Optional | Pipeline identifier |
| Stage ID | Optional | Pipeline stage identifier |
| Responsible User ID | Optional | Assigned owner identifier |
| Contact ID | Optional | Related Contact identifier |
| External Identifier | Optional | Third-party reference stored in Kommo |
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

1. Lead ID
2. External Identifier
3. Custom Field
4. Contact ID
5. Pipeline and Stage
6. Responsible User
7. Lead Name

Whenever possible, use immutable identifiers instead of descriptive attributes.

---

## 3. Normalize Search Criteria

Before executing the request:

- Remove unnecessary whitespace.
- Normalize identifier formats.
- Validate numeric identifiers.
- Verify pipeline and stage identifiers.
- Normalize custom field values.
- Ensure search values conform to expected formats.

Consistent normalization improves search reliability.

---

## 4. Build the Search Request

Construct the API request using the selected search criteria.

Verify that:

- Correct endpoint is used.
- HTTPS is enabled.
- Authorization header is included.
- Query parameters are correctly encoded.
- Pagination parameters are defined if required.
- Filters accurately represent the intended search.

---

## 5. Execute the Search

Submit the request to the Kommo REST API.

Monitor:

- HTTP status code
- API response time
- Authentication status
- Network connectivity
- Request completion

A successful HTTP response does not necessarily indicate that a matching Lead exists.

---

## 6. Validate the Response

Verify that:

- HTTP 200 OK is returned.
- Response body is valid JSON.
- Lead collection is present.
- Response is complete.
- No API errors are reported.

Reject incomplete or malformed responses.

---

## 7. Evaluate Search Results

Determine the search outcome.

Possible results include:

- Exactly one Lead found
- Multiple Leads found
- No Leads found

Each outcome should be processed according to the business rules of the integration.

---

## 8. Resolve Multiple Matches

If multiple Leads are returned:

- Compare Lead IDs.
- Compare Pipeline IDs.
- Compare Stage IDs.
- Compare Contact associations.
- Compare External Identifiers.
- Compare Custom Fields.
- Compare Responsible Users.

Do not automatically select the first returned Lead.

---

## 9. Validate Lead Information

For the selected Lead, verify that required information is available.

Typical validation includes:

- Lead ID
- Lead Name
- Pipeline
- Stage
- Responsible User
- Associated Contacts
- Tags
- Custom Fields
- Creation Date
- Last Updated Date

Additional validation may be required depending on the integration workflow.

---

## 10. Store Required Information

Store only the information required by downstream processes.

Commonly retained values include:

- Lead ID
- Pipeline ID
- Stage ID
- Responsible User ID
- Contact IDs
- External Identifier
- Required Custom Field values

Avoid persisting unnecessary customer information.

---

## 11. Return the Result

Return the outcome to the calling process.

Possible results include:

- Lead Found
- Multiple Leads Found
- Lead Not Found
- Search Failed

Include sufficient metadata to support subsequent workflow decisions.

---

# Validation

The procedure is considered successful when:

- Authentication succeeded.
- Search request completed successfully.
- Response structure is valid.
- Matching Lead has been correctly identified.
- Required Lead information has been validated.
- Search outcome has been returned to the calling workflow.

---

# Expected Result

Upon successful completion:

- The requested Lead has been located or confirmed as absent.
- Duplicate matches have been evaluated when necessary.
- Required Lead identifiers have been collected.
- Downstream processes have reliable information to continue execution.
- No duplicate Lead has been created.

---

# Common Errors

| Error | Possible Cause | Resolution |
|---------|----------------|------------|
| Unauthorized (401) | Invalid or expired Access Token | Refresh OAuth credentials |
| Forbidden (403) | Missing permissions | Review OAuth scopes |
| Lead Not Found | Search criteria do not match any Lead | Verify search parameters |
| Multiple Leads Returned | Duplicate business records exist | Apply duplicate resolution rules |
| Invalid Pipeline ID | Incorrect identifier | Validate Pipeline ID |
| Invalid Stage ID | Stage does not belong to the specified Pipeline | Verify stage mapping |
| Invalid Search Parameter | Unsupported query | Correct request parameters |
| Empty Response | No matching Leads | Confirm search criteria |
| Timeout | Network latency | Retry according to retry policy |
| Rate Limit Reached | Too many requests | Respect API limits before retrying |

---

# Troubleshooting

| Issue | Diagnostic Action | Resolution |
|--------|-------------------|------------|
| No Leads returned | Verify search criteria | Retry using a unique identifier |
| Incorrect Lead selected | Review matching logic | Strengthen filtering criteria |
| Duplicate Leads detected | Inspect Lead identifiers and custom fields | Apply duplicate management policy |
| Pipeline filter produces no results | Validate Pipeline ID | Update configuration |
| Stage filter produces incorrect results | Verify Stage mapping | Correct Stage identifier |
| Authentication failures | Validate OAuth session | Re-authenticate |
| Slow searches | Review filters and pagination | Optimize query strategy |
| Unexpected API response | Inspect response payload | Retry and validate response structure |

---

# Rollback

If the search procedure cannot be completed successfully:

1. Discard incomplete search results.
2. Do not cache invalid responses.
3. Clear temporary search variables.
4. Record the failure in operational logs.
5. Verify authentication status.
6. Validate search parameters.
7. Retry the request if permitted by retry policy.
8. Escalate persistent failures according to operational procedures.

Since this procedure performs read-only operations, no changes are made to Kommo data and no platform rollback is required.

---

# Best Practices

- Always search before updating a Lead.
- Prefer immutable identifiers over descriptive attributes.
- Use Lead ID whenever available.
- Validate Pipeline and Stage relationships.
- Normalize search values before execution.
- Handle duplicate results explicitly.
- Validate API responses before processing.
- Store only required identifiers.
- Respect API rate limits.
- Avoid unnecessary repeated searches.
- Design search operations to be idempotent.
- Log search outcomes without exposing sensitive business information.

---

# References

- Kommo REST API Documentation
- Kommo Leads API Documentation
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