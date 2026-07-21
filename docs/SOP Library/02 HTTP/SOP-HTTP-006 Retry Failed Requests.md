# SOP-HTTP-006 Retry Failed Requests

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-HTTP-006 |
| Domain | HTTP |
| Title | Retry Failed Requests |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

# Purpose

Define the standard procedure for retrying failed HTTP requests caused by temporary or recoverable conditions.

Retrying transient failures improves integration reliability by automatically recovering from temporary network issues, service interruptions, and infrastructure instability while preventing unnecessary duplicate requests and excessive load on external systems.

This SOP establishes a consistent strategy for retrying failed HTTP requests independently of any specific API provider or integration platform.

---

# Scope

This SOP applies whenever an HTTP request fails due to a temporary condition that may succeed if executed again.

Typical scenarios include:

- Network interruptions
- Connection timeouts
- Temporary API outages
- HTTP 429 (Too Many Requests)
- HTTP 500 (Internal Server Error)
- HTTP 502 (Bad Gateway)
- HTTP 503 (Service Unavailable)
- HTTP 504 (Gateway Timeout)

This SOP applies to both synchronous and asynchronous integrations.

Permanent failures are handled according to **SOP-HTTP-007 — Error Response Handling**.

---

# Prerequisites

Before starting, verify that:

- The HTTP request has been implemented.
- Error handling has been configured.
- Retry policies have been approved.
- Logging is enabled.
- The API documentation has been reviewed for retry recommendations.

---

# Inputs

The following information may be required:

| Input | Required |
|---------|----------|
| HTTP Request | Yes |
| API Documentation | Yes |
| Retry Policy | Yes |
| Rate Limit Policy | Recommended |
| Business SLA | Recommended |

---

# Procedure

## Step 1 — Detect Request Failure

Identify that the HTTP request did not complete successfully.

Common failure indicators include:

- HTTP timeout
- Connection failure
- Temporary DNS failure
- Network interruption
- Recoverable HTTP status code

The failure should be captured before any retry attempt is initiated.

---

## Step 2 — Determine Retry Eligibility

Evaluate whether the failed request is eligible for retry.

Typical retryable conditions include:

- HTTP 408 (Request Timeout)
- HTTP 429 (Too Many Requests)
- HTTP 500 (Internal Server Error)
- HTTP 502 (Bad Gateway)
- HTTP 503 (Service Unavailable)
- HTTP 504 (Gateway Timeout)
- Temporary connection failures

Non-retryable conditions include:

- HTTP 400 (Bad Request)
- HTTP 401 (Unauthorized)
- HTTP 403 (Forbidden)
- HTTP 404 (Not Found)
- HTTP 422 (Validation Error)

Only transient failures should trigger automatic retries.

---

## Step 3 — Verify Idempotency

Before retrying, determine whether the request can be safely executed again.

Typical idempotent operations include:

- GET
- PUT
- DELETE

Operations such as POST may require additional safeguards, including:

- Idempotency keys
- Request identifiers
- Duplicate detection
- Business transaction identifiers

Retrying non-idempotent requests without safeguards may create duplicate records.

---

## Step 4 — Apply the Retry Strategy

Execute the retry according to the approved retry policy.

Typical strategies include:

### Fixed Delay

```text
Attempt 1 → Wait 5 seconds

Attempt 2 → Wait 5 seconds

Attempt 3 → Wait 5 seconds
```

### Incremental Delay

```text
5 seconds

10 seconds

20 seconds
```

### Exponential Backoff

```text
5 seconds

10 seconds

20 seconds

40 seconds
```

Exponential backoff is recommended for most public APIs.

---

## Step 5 — Respect Rate Limits

If the failure is caused by rate limiting:

- Honor the `Retry-After` header when available.
- Wait until the reset period expires.
- Resume processing only after the permitted interval.

Rate limit handling should follow **SOP-HTTP-005 — Handle Rate Limits**.

---

## Step 6 — Retry the Request

Resend the original request without modifying:

- Endpoint
- HTTP method
- Headers
- Authentication
- Payload

Only retry after completing the configured waiting period.

---

## Step 7 — Monitor Retry Attempts

Track every retry attempt.

Recommended information includes:

- Attempt number
- Timestamp
- HTTP status code
- Error message
- Delay applied
- Final outcome
- Correlation ID

Operational monitoring should clearly distinguish original requests from retry attempts.

---

## Step 8 — Handle Retry Exhaustion

If all retry attempts fail:

- Stop retrying.
- Route the request to the Error Handler.
- Record the failure.
- Notify operations if required.
- Preserve diagnostic information.

Retry exhaustion should produce a deterministic outcome.

---

## Step 9 — Validate Retry Behavior

Execute controlled testing and verify that:

- Retryable failures trigger retries.
- Permanent failures do not retry.
- Retry delays are correctly applied.
- Duplicate requests are prevented.
- Logging records every retry attempt.
- Exhausted retries invoke the appropriate error handling process.

---

# Validation

The procedure is considered successful when:

- Recoverable failures trigger retries.
- Permanent failures fail immediately.
- Retry limits are respected.
- Waiting periods are correctly applied.
- Duplicate processing is prevented.
- Retry attempts are fully logged.
- Failed retries are escalated appropriately.

---

# Expected Result

Recoverable HTTP request failures are automatically retried according to the approved retry strategy, allowing temporary service interruptions to be resolved without manual intervention while maintaining data integrity and preventing duplicate operations.

---

# Common Errors

| Error | Cause | Impact |
|------|------|--------|
| Retrying permanent failures | Incorrect error classification | Unnecessary requests |
| Infinite retry loop | Missing retry limit | Resource exhaustion |
| Duplicate resource creation | Retrying non-idempotent requests | Data inconsistency |
| Ignoring Retry-After header | Rate limit not respected | Additional throttling |
| Missing retry logs | Insufficient observability | Difficult troubleshooting |

---

# Troubleshooting

| Problem | Resolution |
|----------|------------|
| Retries never occur | Verify retry conditions and HTTP status handling. |
| Requests retry indefinitely | Configure a maximum retry limit. |
| Duplicate records are created | Implement idempotency controls before retrying POST operations. |
| API continues returning HTTP 429 | Increase retry delay and honor the Retry-After header. |
| Retry attempts are difficult to trace | Ensure correlation IDs and retry metadata are included in logs. |

---

# Rollback

If the retry implementation causes operational issues:

1. Disable automatic retries.
2. Restore the previous validated retry configuration.
3. Verify workflow stability.
4. Review retry conditions and idempotency controls.
5. Re-enable retries after successful validation.

---

# Best Practices

- Retry only transient failures.
- Never retry validation or authorization errors.
- Use exponential backoff whenever possible.
- Respect provider-specific retry recommendations.
- Honor the `Retry-After` header.
- Limit the maximum number of retry attempts.
- Ensure idempotency before retrying write operations.
- Log every retry attempt.
- Monitor retry frequency to identify recurring issues.
- Keep retry behavior consistent across all integrations.

---

# References

- SOP-HTTP-001 — Create HTTP Request
- SOP-HTTP-005 — Handle Rate Limits
- SOP-HTTP-007 — Error Response Handling
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