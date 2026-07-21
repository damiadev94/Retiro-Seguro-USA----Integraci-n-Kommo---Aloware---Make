# SOP-HTTP-003 Parse JSON Response

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-HTTP-003 |
| Domain | HTTP |
| Title | Parse JSON Response |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

# Purpose

Define the standard procedure for parsing and validating JSON responses received from HTTP-based services.

A consistent approach to processing JSON responses improves data quality, reduces implementation errors, simplifies maintenance, and ensures reliable data exchange between integrated systems.

This SOP establishes platform-independent best practices for extracting, validating, and transforming JSON data returned by HTTP APIs.

---

# Scope

This SOP applies whenever an integration receives a JSON response from an HTTP endpoint.

Typical use cases include:

- REST API responses
- Webhook payloads
- Search results
- Resource retrieval
- Authentication responses
- Batch processing results
- Status endpoints

This SOP assumes that the HTTP request has been successfully executed according to **SOP-HTTP-001 — Create HTTP Request**.

---

# Prerequisites

Before starting, verify that:

- The HTTP request completed successfully.
- The expected response structure is documented.
- Required business fields have been identified.
- Error handling has been configured.
- Data transformation requirements are known.

---

# Inputs

The following information may be required:

| Input | Required |
|---------|----------|
| HTTP Response | Yes |
| API Documentation | Yes |
| Expected JSON Schema | Recommended |
| Business Requirements | Recommended |
| Data Mapping Specification | Recommended |

---

# Procedure

## Step 1 — Verify the HTTP Status Code

Before processing the response body, verify that the HTTP request completed successfully.

Typical successful status codes include:

- 200 OK
- 201 Created
- 202 Accepted
- 204 No Content

Unexpected status codes should be handled according to **SOP-HTTP-007 — Error Response Handling**.

---

## Step 2 — Validate the Content Type

Confirm that the response contains JSON data.

Typical header:

```text
Content-Type: application/json
```

If another format is returned (XML, HTML, plain text, etc.), follow the appropriate processing procedure.

---

## Step 3 — Parse the JSON Document

Convert the response body into a structured object supported by the integration platform.

The parser should validate that:

- the document is valid JSON;
- the structure is complete;
- the syntax is correct.

Malformed JSON should be treated as an unexpected response.

---

## Step 4 — Validate the Response Structure

Compare the parsed response with the expected schema.

Verify:

- required objects exist;
- required fields are present;
- nested objects are available;
- arrays have the expected structure.

Do not assume that optional fields are always present.

---

## Step 5 — Validate Data Types

Verify that each required field contains the expected data type.

Common data types include:

- String
- Number
- Boolean
- Object
- Array
- Date/Time
- Null

Unexpected data types should be treated as validation failures.

---

## Step 6 — Extract Required Fields

Retrieve only the fields required by the business process.

Typical examples include:

- Identifier
- Name
- Status
- Timestamp
- Email
- Phone Number
- Created Date
- Updated Date

Avoid extracting unnecessary information.

---

## Step 7 — Handle Optional and Missing Fields

Determine how optional fields should be processed.

Possible strategies include:

- Use a default value.
- Skip the field.
- Continue processing.
- Trigger a validation warning.
- Stop processing if the field is business-critical.

The handling strategy should be defined by the business requirements.

---

## Step 8 — Validate Business Rules

Verify that the extracted data satisfies the business logic.

Examples include:

- Status is valid.
- Required identifiers exist.
- Numeric values are within acceptable ranges.
- Dates are valid.
- Mandatory business conditions are satisfied.

Technical validation alone is not sufficient.

---

## Step 9 — Pass Data to the Next Process

After validation, expose the processed data to downstream workflow components.

Typical destinations include:

- Data transformation
- Database operations
- CRM synchronization
- API requests
- Business workflow execution

Only validated data should continue through the integration.

---

# Validation

The procedure is considered successful when:

- The response is valid JSON.
- Required fields are present.
- Data types are correct.
- Business rules are satisfied.
- Invalid responses are detected.
- Only validated data proceeds through the workflow.

---

# Expected Result

The JSON response is successfully parsed, validated, and transformed into a structured dataset suitable for subsequent integration processes.

---

# Common Errors

| Error | Cause | Impact |
|------|------|--------|
| Invalid JSON | Malformed response | Parsing failure |
| Missing required field | Incomplete API response | Business process failure |
| Incorrect data type | API response differs from specification | Validation failure |
| Unexpected response structure | API version changes | Workflow interruption |
| Processing optional fields as mandatory | Incorrect assumptions | Unnecessary failures |

---

# Troubleshooting

| Problem | Resolution |
|----------|------------|
| JSON cannot be parsed | Verify that the response body is valid JSON and the Content-Type is correct. |
| Required fields are missing | Compare the response with the API documentation and validate the endpoint. |
| Data type validation fails | Review the API specification and update the parsing logic if necessary. |
| Unexpected nested objects | Inspect the latest response structure and adjust the extraction logic. |
| Business validation fails | Verify that the returned data satisfies the business requirements before continuing. |

---

# Rollback

If JSON parsing causes workflow failures:

1. Stop processing the affected response.
2. Restore the previous validated parsing configuration.
3. Review the API response structure.
4. Update the parsing rules if the API has changed.
5. Execute validation tests before resuming production.

---

# Best Practices

- Always validate the HTTP status code before parsing.
- Confirm the response content type.
- Validate JSON syntax before accessing fields.
- Validate required fields before processing.
- Treat optional fields appropriately.
- Validate data types explicitly.
- Separate technical validation from business validation.
- Parse only the data required by the workflow.
- Protect sensitive information throughout processing.
- Keep parsing logic resilient to minor API changes.

---

# References

- SOP-HTTP-001 — Create HTTP Request
- SOP-HTTP-007 — Error Response Handling
- SOP-HTTP-008 — Data Transformation
- SOP-INF-004 — Configure Error Handler
- SOP-INF-006 — Configure Logging
- SOP Template
- Integration Documentation Framework

---

# Revision History

| Version | Date | Author | Changes |
|----------|------|--------|---------|
| 1.0 | YYYY-MM-DD | Solution Architect | Initial version |