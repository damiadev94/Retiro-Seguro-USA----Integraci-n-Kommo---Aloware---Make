# SOP-HTTP-001 Create HTTP Request

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-HTTP-001 |
| Domain | HTTP |
| Title | Create HTTP Request |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

# Purpose

Define the standard procedure for creating HTTP requests within integration workflows.

A consistent approach to constructing HTTP requests improves interoperability, reduces implementation errors, simplifies troubleshooting, and ensures compatibility across different APIs and integration platforms.

This SOP establishes best practices for building HTTP requests independently of any specific provider or integration platform.

---

# Scope

This SOP applies to any workflow that communicates with an external service using the HTTP protocol.

Typical use cases include:

- REST API integrations
- Webhook callbacks
- Internal microservices
- Third-party SaaS platforms
- Custom APIs
- Serverless endpoints

Supported HTTP methods include:

- GET
- POST
- PUT
- PATCH
- DELETE
- HEAD
- OPTIONS

This SOP is platform-agnostic and applies regardless of the integration technology (Make, n8n, custom code, middleware, etc.).

---

# Prerequisites

Before starting, verify that:

- The target API endpoint has been identified.
- Authentication requirements are documented.
- Required request parameters are known.
- Required headers have been identified.
- Request payload specifications are available.
- Error handling has been defined.

---

# Inputs

The following information may be required:

| Input | Required |
|---------|----------|
| Base URL | Yes |
| Endpoint | Yes |
| HTTP Method | Yes |
| Authentication Method | Yes |
| Headers | If applicable |
| Query Parameters | If applicable |
| Request Body | If applicable |
| API Documentation | Recommended |

---

# Procedure

## Step 1 — Identify the Endpoint

Determine the target endpoint that will receive the request.

Example:

```text
https://api.example.com/v1/contacts
```

Verify that:

- the endpoint exists;
- the API version is correct;
- the endpoint matches the intended business operation.

---

## Step 2 — Select the HTTP Method

Choose the appropriate HTTP method based on the intended operation.

| Method | Typical Purpose |
|---------|-----------------|
| GET | Retrieve information |
| POST | Create a new resource |
| PUT | Replace an existing resource |
| PATCH | Partially update a resource |
| DELETE | Remove a resource |
| HEAD | Retrieve headers only |
| OPTIONS | Discover supported operations |

The selected method should align with the API specification.

---

## Step 3 — Configure Authentication

Configure the authentication mechanism required by the API.

Common methods include:

- API Key
- Bearer Token
- OAuth 2.0
- Basic Authentication
- Custom Headers

Authentication configuration is defined in **SOP-HTTP-002 — Configure Authentication**.

---

## Step 4 — Configure Request Headers

Include all required HTTP headers.

Common headers include:

```text
Content-Type

Accept

Authorization

User-Agent

X-Correlation-ID
```

Only include headers required by the target API.

---

## Step 5 — Configure Query Parameters

When supported by the API, define query parameters.

Example:

```text
GET /contacts?page=2&limit=100
```

Typical query parameters include:

- page
- limit
- offset
- filter
- search
- sort
- include

Query parameters should be URL encoded when necessary.

---

## Step 6 — Configure the Request Body

For methods such as POST, PUT, or PATCH, construct the request payload according to the API specification.

Common body formats include:

- JSON
- Form Data
- URL Encoded Form
- XML
- Multipart Form Data

Validate that:

- required fields are present;
- field names match the specification;
- data types are correct;
- optional fields are included only when necessary.

---

## Step 7 — Validate the Request

Before execution, verify:

- URL
- HTTP method
- Authentication
- Headers
- Query parameters
- Payload structure
- Required fields
- Data types

Correct validation reduces unnecessary API failures.

---

## Step 8 — Send the Request

Execute the HTTP request using the selected integration platform.

Monitor:

- request duration;
- response status;
- timeout behavior;
- connectivity issues.

---

## Step 9 — Validate the Response

After execution, verify:

- HTTP status code
- Response headers
- Response body
- Expected resource
- Business outcome

Successful responses should be processed according to **SOP-HTTP-003 — Parse JSON Response**.

Unexpected responses should follow **SOP-HTTP-007 — Error Response Handling**.

---

# Validation

The procedure is considered successful when:

- The request reaches the intended endpoint.
- Authentication succeeds.
- Required headers are included.
- Parameters are transmitted correctly.
- The payload matches the API specification.
- The API returns the expected response.
- No unexpected HTTP errors occur.

---

# Expected Result

A valid HTTP request is successfully executed against the target API, producing the expected response while complying with the API specification and organizational integration standards.

---

# Common Errors

| Error | Cause | Impact |
|------|------|--------|
| Invalid endpoint | Incorrect URL | Request fails |
| Incorrect HTTP method | Wrong operation selected | Unexpected API behavior |
| Missing authentication | Authentication not configured | Unauthorized request |
| Missing headers | Required headers omitted | Request rejected |
| Invalid payload | Incorrect JSON or field names | Validation errors |
| Incorrect query parameters | Invalid parameter values | Unexpected results |

---

# Troubleshooting

| Problem | Resolution |
|----------|------------|
| Request returns 404 | Verify the endpoint URL and API version. |
| Request returns 401 or 403 | Review the authentication configuration and permissions. |
| Request returns 400 | Validate the request body, query parameters, and required fields. |
| Request times out | Verify network connectivity, timeout settings, and API availability. |
| Unexpected response data | Confirm the endpoint, HTTP method, and request parameters. |

---

# Rollback

If the request configuration causes operational issues:

1. Stop executing the affected workflow.
2. Restore the previous validated request configuration.
3. Verify endpoint availability.
4. Revalidate authentication and request parameters.
5. Execute controlled testing before returning to production.

---

# Best Practices

- Follow the API documentation exactly.
- Use the correct HTTP method for each operation.
- Keep request payloads as small as possible.
- Validate data before sending requests.
- Use descriptive headers where appropriate.
- Generate a correlation ID for traceability.
- Avoid hardcoded configuration values.
- Reuse shared variables whenever possible.
- Protect confidential information.
- Test requests before production deployment.

---

# References

- SOP-HTTP-002 — Configure Authentication
- SOP-HTTP-003 — Parse JSON Response
- SOP-HTTP-007 — Error Response Handling
- SOP-INF-004 — Configure Error Handler
- SOP-INF-005 — Configure Retry Policy
- SOP-INF-006 — Configure Logging
- SOP-INF-010 — Secrets Management
- SOP Template
- Integration Documentation Framework

---

# Revision History

| Version | Date | Author | Changes |
|----------|------|--------|---------|
| 1.0 | YYYY-MM-DD | Solution Architect | Initial version |