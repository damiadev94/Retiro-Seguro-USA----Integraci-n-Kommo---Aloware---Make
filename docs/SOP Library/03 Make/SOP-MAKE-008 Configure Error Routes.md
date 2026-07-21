# SOP-MAKE-008 Configure Error Routes

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-MAKE-008 |
| Domain | Make |
| Title | Configure Error Routes |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

# Purpose

Define the standard procedure for configuring Error Routes in Make scenarios.

Error Routes provide an alternative execution path when a module fails, allowing the workflow to recover gracefully, preserve operational continuity, and capture diagnostic information without unnecessarily terminating the entire scenario.

This SOP establishes a consistent approach for implementing platform-specific error handling within Make.

---

# Scope

This SOP applies whenever a Make scenario requires custom handling of module execution failures.

Typical use cases include:

- HTTP request failures
- Temporary API outages
- Authentication errors
- Data validation failures
- Rate limiting
- Retry logic
- Logging
- Notifications
- Recovery workflows
- Dead-letter processing

This SOP focuses exclusively on Error Routes within Make.

Business-specific error recovery strategies are documented in the corresponding platform domains.

---

# Prerequisites

Before starting, verify that:

- The scenario has been implemented.
- Business recovery requirements have been documented.
- Retry policies have been approved.
- Logging has been configured.
- Failure scenarios have been identified.

---

# Inputs

The following information may be required:

| Input | Required |
|---------|----------|
| Integration Design | Yes |
| Error Handling Strategy | Yes |
| Retry Policy | Recommended |
| Business Rules | Recommended |
| Notification Requirements | Recommended |

---

# Procedure

## Step 1 — Identify Failure Points

Review the workflow and identify modules that may fail.

Typical examples include:

- HTTP requests
- API operations
- Database access
- Data Store operations
- File operations
- Authentication modules
- External platform modules

Focus Error Routes on modules where recovery is possible or operational visibility is required.

---

## Step 2 — Classify Expected Errors

Determine which failures should be handled.

Typical categories include:

### Recoverable Errors

Examples:

- Temporary network failures
- HTTP 429
- HTTP 500
- HTTP 502
- HTTP 503
- HTTP 504

These errors may trigger retries.

---

### Non-Recoverable Errors

Examples:

- Invalid credentials
- Validation errors
- Missing required data
- Configuration errors
- Unsupported operations

These errors should normally terminate processing and generate operational visibility.

---

## Step 3 — Create the Error Route

Attach an Error Route to the module requiring custom error handling.

The Error Route should only handle failures relevant to that module.

Avoid routing unrelated errors through the same recovery path.

---

## Step 4 — Define the Recovery Action

Determine the action performed after a failure.

Typical recovery actions include:

- Retry the operation
- Log the failure
- Store the failed record
- Skip the current record
- Continue processing
- Notify operations
- Create an incident
- Stop the workflow

The recovery action should match the business recovery strategy.

---

## Step 5 — Capture Diagnostic Information

Collect information required for troubleshooting.

Recommended fields include:

- Scenario name
- Module name
- Execution ID
- Correlation ID
- Timestamp
- Error message
- Error code
- HTTP status code
- Input payload
- Retry attempt

Diagnostic information should be sufficient to reproduce and investigate the failure.

---

## Step 6 — Preserve Workflow Integrity

Ensure that failure handling does not compromise workflow consistency.

Verify that:

- Completed operations are not repeated.
- Duplicate records are avoided.
- Partial transactions are not propagated.
- Failed records remain traceable.

Error recovery should never compromise data integrity.

---

## Step 7 — Configure Notifications

Define when operational notifications should be generated.

Typical notification scenarios include:

- Retry exhaustion
- Authentication failures
- External service outages
- Repeated processing failures
- Critical business operations

Avoid generating notifications for expected transient failures that are automatically recovered.

---

## Step 8 — Validate Error Recovery

Simulate representative failure scenarios.

Verify that:

- The Error Route executes.
- Recovery actions are performed.
- Logs are generated.
- Notifications are sent when required.
- The workflow behaves as expected.

Every configured Error Route should be validated before deployment.

---

## Step 9 — Document the Error Route

Record:

- Protected module
- Failure conditions
- Recovery strategy
- Retry behavior
- Logging actions
- Notification rules
- Dependencies

Documentation should clearly explain the purpose of the Error Route and its expected behavior.

---

# Validation

The procedure is considered successful when:

- Expected failures trigger the Error Route.
- Recovery actions execute correctly.
- Diagnostic information is captured.
- Workflow integrity is maintained.
- Notifications are generated when required.
- Error Route behavior is documented.

---

# Expected Result

Scenario failures are handled through controlled recovery paths that preserve workflow stability, improve observability, and support operational troubleshooting without compromising business data.

---

# Common Errors

| Error | Cause | Impact |
|------|------|--------|
| No Error Route configured | Default failure behavior only | Scenario terminates unexpectedly |
| Every error routed identically | No error classification | Inefficient recovery |
| Missing diagnostic information | Incomplete logging | Difficult troubleshooting |
| Retry configured for permanent failures | Incorrect recovery strategy | Unnecessary processing |
| Notifications generated for every failure | Excessive alerting | Alert fatigue |

---

# Troubleshooting

| Problem | Resolution |
|----------|------------|
| Error Route never executes | Verify that it is attached to the correct module and that the failure is reproducible. |
| Scenario stops despite Error Route | Review module configuration and confirm that the Error Route handles the expected error type. |
| Recovery repeats indefinitely | Verify retry limits and termination conditions. |
| Failed records cannot be investigated | Ensure sufficient diagnostic information is logged before recovery actions execute. |
| Operations receive excessive alerts | Review notification rules and restrict alerts to actionable failures. |

---

# Rollback

If the Error Route configuration introduces operational issues:

1. Disable the affected Error Route.
2. Restore the previous validated configuration.
3. Review recovery logic.
4. Validate failure handling.
5. Execute controlled testing before returning to production.

---

# Best Practices

- Configure Error Routes only where recovery adds value.
- Separate recoverable and non-recoverable failures.
- Keep recovery logic simple and deterministic.
- Capture sufficient diagnostic information.
- Prevent duplicate processing after failures.
- Limit automatic retries according to the approved retry policy.
- Notify operations only for actionable incidents.
- Test every recovery path before deployment.
- Document every Error Route and its recovery strategy.
- Periodically review recurring failures to improve workflow reliability.

---

# References

- SOP-MAKE-001 — Create Scenario
- SOP-MAKE-005 — Configure Data Store
- SOP-MAKE-007 — Configure Scheduling
- SOP-MAKE-009 — Test Scenario
- SOP-HTTP-005 — Handle Rate Limits
- SOP-HTTP-006 — Retry Failed Requests
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