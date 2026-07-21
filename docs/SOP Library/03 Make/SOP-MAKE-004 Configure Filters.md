# SOP-MAKE-004 Configure Filters

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-MAKE-004 |
| Domain | Make |
| Title | Configure Filters |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

# Purpose

Define the standard procedure for configuring Filters in Make scenarios.

Filters control whether a workflow continues through a specific execution path based on defined conditions. Proper filter implementation ensures that only relevant data is processed, reduces unnecessary executions, improves performance, and preserves business logic integrity.

This SOP establishes a consistent approach for implementing conditional logic within Make scenarios.

---

# Scope

This SOP applies whenever a Make scenario requires conditional execution.

Typical use cases include:

- Event filtering
- Business rule evaluation
- Record classification
- Pipeline stage validation
- Status verification
- Environment selection
- Data quality validation
- Duplicate prevention
- Conditional synchronization

This SOP applies to filters attached to Routers as well as filters placed between individual modules.

---

# Prerequisites

Before starting, verify that:

- The scenario has been created.
- The trigger has been configured.
- Required input data is available.
- Business rules have been documented.
- Routing logic has been defined.

---

# Inputs

The following information may be required:

| Input | Required |
|---------|----------|
| Integration Design | Yes |
| Business Rules | Yes |
| Input Payload | Yes |
| Data Mapping | Recommended |
| Workflow Diagram | Recommended |

---

# Procedure

## Step 1 — Identify the Business Condition

Determine the condition that controls workflow execution.

Typical conditions include:

- Status equals a specific value
- Field exists
- Field is empty
- Numeric comparison
- Date comparison
- Boolean value
- Text comparison
- Record type
- Custom business rule

Each filter should evaluate a single business decision.

---

## Step 2 — Identify the Required Data

Verify that all fields required by the filter are available.

Review:

- Input payload
- Mapped fields
- Variables
- Module outputs
- Data types

Filtering should only use validated and available data.

---

## Step 3 — Define the Filter Logic

Translate the business rule into a logical expression.

Typical operators include:

- Equals
- Does not equal
- Greater than
- Less than
- Contains
- Does not contain
- Exists
- Does not exist
- Is empty
- Is not empty

The filter should directly reflect the documented business rule.

---

## Step 4 — Configure the Filter

Attach the filter to the appropriate connection.

Typical locations include:

- Between modules
- Router routes
- Conditional processing branches

Filters should be positioned immediately before the modules they control.

---

## Step 5 — Apply Clear Naming

Assign a descriptive name that explains the business condition.

Recommended examples:

```text
Lead is Qualified

Call Completed

Stage Changed

Contact Exists

Valid Phone Number

Production Environment
```

Avoid generic names such as:

```text
Filter 1

Condition

Test

Validation
```

The filter name should describe **why** the route executes.

---

## Step 6 — Keep Conditions Simple

Configure concise and readable conditions.

If the business logic becomes complex:

- Separate conditions into multiple filters.
- Introduce additional routers when appropriate.
- Move complex decision logic into dedicated workflow sections.

Simple filters are easier to understand and maintain.

---

## Step 7 — Validate Every Possible Outcome

Test both execution paths.

Verify that:

- Matching records continue.
- Non-matching records stop.
- Unexpected data is handled correctly.
- No unintended modules execute.

Both positive and negative conditions should be validated.

---

## Step 8 — Prevent Overlapping Conditions

Review all filters connected to the same router.

Verify that:

- Conditions are mutually exclusive when required.
- No record unintentionally matches multiple routes.
- Business priorities are respected.

Overlapping filters may produce duplicate processing.

---

## Step 9 — Document the Filter

Record:

- Filter name
- Business purpose
- Evaluated fields
- Operators
- Expected outcome
- Related business rule

Documentation should clearly explain why the filter exists.

---

# Validation

The procedure is considered successful when:

- Filter logic matches the documented business rule.
- Only intended records continue.
- Invalid records are excluded.
- No duplicate processing occurs.
- Filter names are descriptive.
- Configuration is documented.

---

# Expected Result

Workflow execution is controlled through clear, maintainable, and predictable filtering rules that accurately implement the required business logic.

---

# Common Errors

| Error | Cause | Impact |
|------|------|--------|
| Incorrect comparison operator | Misconfigured condition | Wrong execution path |
| Generic filter names | Poor documentation | Difficult maintenance |
| Overlapping filters | Inconsistent routing | Duplicate processing |
| Filtering on unavailable fields | Incorrect module order | Runtime errors |
| Complex filter expressions | Poor workflow design | Difficult troubleshooting |

---

# Troubleshooting

| Problem | Resolution |
|----------|------------|
| Filter never matches | Verify field mapping, operators, and expected values. |
| Multiple routes execute unexpectedly | Review filter overlap and ensure conditions are mutually exclusive where appropriate. |
| Records are incorrectly excluded | Validate the business rule and inspect the incoming payload. |
| Filter references missing fields | Ensure the required data is available before the filter executes. |
| Filter logic is difficult to understand | Split the condition into smaller filters or redesign the routing strategy. |

---

# Rollback

If the filter configuration causes workflow issues:

1. Disable the affected scenario.
2. Remove the incorrect filter.
3. Restore the previous validated condition.
4. Verify workflow execution.
5. Perform controlled testing before returning to production.

---

# Best Practices

- One filter should evaluate one business decision.
- Use descriptive filter names.
- Keep conditions simple and readable.
- Avoid deeply nested logical expressions.
- Filter as early as possible to reduce unnecessary processing.
- Ensure filters evaluate validated data.
- Prevent overlapping route conditions whenever possible.
- Test both matching and non-matching scenarios.
- Document every business condition.
- Review filters whenever business rules change.

---

# References

- SOP-MAKE-002 — Configure Trigger
- SOP-MAKE-003 — Configure Router
- SOP-MAKE-005 — Configure Data Store
- SOP-MAKE-006 — Configure Variables
- SOP-MAKE-009 — Test Scenario
- SOP-INF-006 — Configure Logging
- SOP Template
- Integration Documentation Framework

---

# Revision History

| Version | Date | Author | Changes |
|----------|------|--------|---------|
| 1.0 | YYYY-MM-DD | Solution Architect | Initial version |