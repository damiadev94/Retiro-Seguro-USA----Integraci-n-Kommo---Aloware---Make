# SOP-HTTP-007 Error Response Handling

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-HTTP-007 |
| Domain | HTTP |
| Title | Error Response Handling |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

# Purpose

Define the standard procedure for handling HTTP error responses returned by external services.

A consistent error response strategy ensures that failures are correctly identified, classified, logged, and managed without compromising data integrity or workflow stability. Proper error handling improves reliability, simplifies troubleshooting, and enables predictable recovery across integration projects.

This SOP establishes a platform-independent approach for processing HTTP error responses.

---

# Scope

This SOP applies whenever an HTTP request returns an unsuccessful response.

Typical scenarios include:

- Client errors (4xx)
- Server errors (5xx)
- Authentication failures
- Authorization failures
- Validation errors
- Rate limiting
- Resource conflicts
- Service outages
- Unexpected HTTP responses

This SOP applies to every HTTP-based integration regardless of the target platform.

---

# Prerequisites

Before starting, verify that:

- HTTP requests have been implemented.
- Retry policies have been defined.
- Error handlers are configured.
- Logging is enabled.
- Business recovery requirements are documented.

---

# Inputs

The following information may be required:

| Input | Required |
|---------|----------|
| HTTP Response | Yes |
| HTTP Status Code | Yes |
| Response Body | If available |
| API Documentation | Recommended |
| Business Rules | Recommended |

---

# Procedure

## Step 1 — Detect the Error Response

Determine whether the response indicates a failure.

Typical unsuccessful status codes include:

- 400 Bad Request
- 401 Unauthorized
- 403 Forbidden
- 404 Not Found
- 409 Conflict
- 422 Unprocessable Entity
- 429 Too Many Requests
- 500 Internal Server Error
- 502 Bad Gateway
- 503 Service Unavailable
- 504 Gateway Timeout

Any unexpected HTTP status should be treated as an error until validated.

---

## Step 2 — Classify the Error

Categorize the response according to its origin.

### Client Errors (4xx)

Examples:

- Invalid request
- Authentication failure
- Authorization failure
- Validation failure
- Resource not found

These errors generally require correcting the request before retrying.

---

### Server Errors (5xx)

Examples:

- Internal server error
- Service unavailable
- Gateway timeout
- Temporary platform outage

These errors are often recoverable and may trigger retries.

---

### Unexpected Responses

Examples:

- Unknown HTTP status code
- Invalid response format
- Missing response body
- Unsupported media type

Unexpected responses should be investigated before continuing workflow execution.

---

## Step 3 — Extract Error Details

Capture diagnostic information from the response.

Typical fields include:

- HTTP status code
- Error code
- Error message
- Error description
- Request ID
- Correlation ID
- Timestamp
- Endpoint
- Response body

Capture as much information as possible without exposing sensitive data.

---

## Step 4 — Determine Recoverability

Evaluate whether the error can be resolved automatically.

Typical recoverable errors include:

- HTTP 429
- HTTP 500
- HTTP 502
- HTTP 503
- HTTP 504
- Temporary network failures

Typical non-recoverable errors include:

- HTTP 400
- HTTP 401
- HTTP 403
- HTTP 404
- HTTP 409
- HTTP 422

The recovery strategy should be consistent with the approved retry policy.

---

## Step 5 — Execute the Appropriate Response

Select the appropriate action based on the error category.

Possible actions include:

- Retry the request.
- Stop processing.
- Skip the affected record.
- Route the workflow to the Error Handler.
- Notify operations.
- Create an incident.
- Escalate for manual review.

Business requirements determine the appropriate response.

---

## Step 6 — Log the Error

Record sufficient information for operational analysis.

Recommended log information includes:

- Timestamp
- Workflow
- Scenario
- Endpoint
- HTTP method
- HTTP status code
- Error category
- Error message
- Correlation ID
- Retry attempt
- Final action

Logs should support troubleshooting without exposing confidential information.

---

## Step 7 — Preserve Workflow Integrity

Prevent partial or inconsistent processing.

Ensure that:

- Completed operations are not repeated.
- Duplicate records are avoided.
- Business transactions remain consistent.
- Failed operations are isolated.

Error handling should never compromise data integrity.

---

## Step 8 — Notify When Required

Generate operational notifications for critical failures.

Typical notification scenarios include:

- Authentication failures
- Repeated retry exhaustion
- Service outages
- Critical synchronization failures
- Persistent API errors

Notification channels depend on organizational standards.

---

## Step 9 — Validate the Error Handling Process

Perform controlled testing to verify that:

- Errors are correctly classified.
- Recovery actions execute as expected.
- Logs are complete.
- Notifications are generated when required.
- Workflow integrity is maintained.

---

# Validation

The procedure is considered successful when:

- HTTP errors are correctly detected.
- Errors are properly classified.
- Recoverable failures invoke retries.
- Non-recoverable failures stop safely.
- Diagnostic information is captured.
- Workflow integrity is preserved.
- Operational notifications function correctly.

---

# Expected Result

HTTP error responses are processed consistently, allowing recoverable failures to be resolved automatically while ensuring permanent failures are safely managed, documented, and escalated when necessary.

---

# Common Errors

| Error | Cause | Impact |
|------|------|--------|
| Treating every error as retryable | Incorrect classification | Unnecessary API requests |
| Ignoring response details | Poor diagnostics | Difficult troubleshooting |
| Missing workflow rollback | Partial processing | Data inconsistency |
| Sensitive information written to logs | Poor logging practices | Security risk |
| Missing operational notifications | Incomplete monitoring | Delayed incident response |

---

# Troubleshooting

| Problem | Resolution |
|----------|------------|
| Error responses cannot be diagnosed | Capture additional diagnostic information from the response body and headers. |
| Requests continue failing after retries | Verify whether the error is recoverable and review the retry policy. |
| Workflow stops unexpectedly | Confirm that all error responses are routed through the configured Error Handler. |
| Duplicate records appear after failures | Review idempotency controls and transaction management. |
| Critical failures are not reported | Validate notification rules and monitoring integrations. |

---

# Rollback

If the error handling implementation causes operational issues:

1. Disable the affected workflow.
2. Restore the previous validated error handling configuration.
3. Verify request processing.
4. Reconfigure error classification if necessary.
5. Execute controlled testing before returning to production.

---

# Best Practices

- Evaluate every HTTP status code explicitly.
- Separate recoverable and non-recoverable errors.
- Capture complete diagnostic information.
- Never expose confidential information in logs.
- Maintain workflow consistency during failures.
- Avoid retrying permanent errors.
- Notify operations only for actionable incidents.
- Keep error handling independent of business logic.
- Regularly review recurring error patterns.
- Align recovery actions with business requirements.

---

# References

- SOP-HTTP-001 — Create HTTP Request
- SOP-HTTP-003 — Parse JSON Response
- SOP-HTTP-005 — Handle Rate Limits
- SOP-HTTP-006 — Retry Failed Requests
- SOP-INF-004 — Configure Error Handler
- SOP-INF-005 — Configure Retry Policy
- SOP-INF-006 — Configure Logging
- SOP Template
- Integration Documentation Framework

---

# Revision History

| Version | Date | Author | Changes |
|----------|------|--------|---------|
| 1.0 | YYYY-MM-DD | Solution Architect | Initial version |