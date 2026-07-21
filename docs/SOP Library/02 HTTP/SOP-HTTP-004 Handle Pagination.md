````markdown
# SOP-HTTP-004 Handle Pagination

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-HTTP-004 |
| Domain | HTTP |
| Title | Handle Pagination |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

# Purpose

Define the standard procedure for retrieving paginated data from HTTP-based APIs.

Many APIs divide large datasets into multiple pages to improve performance and reduce payload size. A standardized pagination strategy ensures that all available records are retrieved reliably, efficiently, and without duplication or omission.

This SOP establishes platform-independent best practices for implementing pagination across integration workflows.

---

# Scope

This SOP applies whenever an HTTP API returns paginated results.

Typical use cases include:

- Contact synchronization
- Lead synchronization
- Customer imports
- Product catalogs
- Order history
- Activity logs
- Audit records
- Search results
- Reporting APIs

This SOP applies regardless of the pagination mechanism implemented by the API provider.

---

# Prerequisites

Before starting, verify that:

- The API documentation defines its pagination model.
- Authentication has been configured.
- The expected dataset has been identified.
- Rate limit requirements are understood.
- Error handling has been implemented.

---

# Inputs

The following information may be required:

| Input | Required |
|---------|----------|
| API Documentation | Yes |
| Endpoint | Yes |
| Pagination Method | Yes |
| Maximum Page Size | Recommended |
| Rate Limit Information | Recommended |

---

# Procedure

## Step 1 — Identify the Pagination Strategy

Review the API documentation to determine how pagination is implemented.

Common pagination methods include:

- Page Number
- Offset / Limit
- Cursor-Based Pagination
- Token-Based Pagination
- Next Page URL
- Continuation Token

The integration should implement the strategy defined by the API provider.

---

## Step 2 — Determine the Page Size

Configure the number of records requested per page.

Consider:

- API limitations
- Performance requirements
- Response size
- Memory usage
- Rate limits

When supported, use the largest practical page size without exceeding provider limits.

---

## Step 3 — Execute the Initial Request

Send the first HTTP request using the configured pagination parameters.

Examples:

```text
GET /contacts?page=1

GET /contacts?offset=0&limit=100

GET /contacts?cursor=<cursor>
```

Record the pagination information returned by the API.

---

## Step 4 — Process the Current Page

For each response:

- Validate the HTTP status code.
- Parse the JSON response.
- Process each record.
- Validate business rules.
- Record execution metrics if required.

Only continue after successfully processing the current page.

---

## Step 5 — Determine Whether Additional Pages Exist

Inspect the response for pagination indicators.

Common indicators include:

- Total Pages
- Total Records
- Next Page Number
- Next Cursor
- Continuation Token
- Next URL
- hasNext flag

Do not assume that another page exists without confirmation.

---

## Step 6 — Request the Next Page

If additional data is available:

- Update the pagination parameter.
- Execute the next request.
- Repeat the processing sequence.

Continue until no further pages remain.

---

## Step 7 — Prevent Duplicate Processing

Ensure that records are processed only once.

Recommended techniques include:

- Unique identifiers
- Record tracking
- Idempotent processing
- Deduplication logic

Pagination should never produce duplicate business operations.

---

## Step 8 — Handle Pagination Interruptions

If pagination is interrupted:

- Record the last successfully processed page.
- Preserve the current cursor or continuation token.
- Log the interruption.
- Resume from the last successful position whenever supported.

Avoid restarting from the beginning unless required.

---

## Step 9 — Validate Completion

After processing all pages, verify that:

- Every page was retrieved.
- No records were skipped.
- No duplicates were processed.
- Pagination completed successfully.
- The total number of processed records is reasonable.

---

# Validation

The procedure is considered successful when:

- All available pages are retrieved.
- Every record is processed exactly once.
- Pagination terminates correctly.
- No duplicate records are generated.
- No records are omitted.
- Interruptions can be safely resumed when supported.

---

# Expected Result

All available records exposed by the paginated API are retrieved, validated, and processed completely, efficiently, and without duplication.

---

# Common Errors

| Error | Cause | Impact |
|------|------|--------|
| Infinite pagination loop | Incorrect termination condition | Excessive API calls |
| Missing records | Incorrect page increment | Incomplete synchronization |
| Duplicate processing | Pagination state not maintained | Duplicate business operations |
| Large page size | Exceeds provider limits | Request failures or timeouts |
| Restarting from page one after interruption | Missing checkpoint mechanism | Unnecessary processing |

---

# Troubleshooting

| Problem | Resolution |
|----------|------------|
| Records appear to be missing | Verify the pagination parameters and ensure every page is processed. |
| Duplicate records are created | Implement record deduplication and verify pagination state management. |
| Pagination never finishes | Review the termination condition and ensure the next-page indicator is correctly interpreted. |
| Requests fail on large datasets | Reduce the page size and review API limits. |
| Workflow restarts after interruption | Store the last processed page or cursor and resume from that point when supported. |

---

# Rollback

If the pagination implementation causes operational issues:

1. Stop the synchronization process.
2. Restore the previous validated pagination configuration.
3. Verify pagination parameters.
4. Confirm record integrity.
5. Execute controlled testing before resuming production.

---

# Best Practices

- Follow the pagination model defined by the API.
- Use the maximum safe page size.
- Process each page independently.
- Validate every response before requesting the next page.
- Prevent duplicate processing through idempotency.
- Store pagination state for long-running synchronizations.
- Respect API rate limits during pagination.
- Monitor execution time and processed record counts.
- Log pagination progress for troubleshooting.
- Design pagination workflows to resume safely after interruptions.

---

# References

- SOP-HTTP-001 — Create HTTP Request
- SOP-HTTP-003 — Parse JSON Response
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
````
