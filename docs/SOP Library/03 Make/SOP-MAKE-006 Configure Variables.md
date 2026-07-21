# SOP-MAKE-006 Configure Variables

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-MAKE-006 |
| Domain | Make |
| Title | Configure Variables |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

# Purpose

Define the standard procedure for configuring and managing variables within Make scenarios.

Variables provide temporary storage for data during workflow execution, enabling information to be reused across modules, reducing duplicate operations, improving readability, and simplifying scenario maintenance.

This SOP establishes a consistent approach for using variables as part of workflow orchestration while maintaining clear separation from persistent storage and environment configuration.

---

# Scope

This SOP applies whenever temporary data must be stored and reused during the execution of a Make scenario.

Typical use cases include:

- Store intermediate calculations
- Preserve API responses
- Reuse identifiers
- Build dynamic payloads
- Assemble request bodies
- Temporary flags
- Execution context
- Correlation identifiers
- Aggregated values

This SOP applies only to variables used during scenario execution.

Persistent storage is covered in **SOP-MAKE-005 — Configure Data Store**.

Environment configuration is covered in **SOP-INF-009 — Environment Variables**.

---

# Prerequisites

Before starting, verify that:

- The scenario has been created.
- Required workflow inputs are available.
- Variable requirements have been identified.
- Business logic has been documented.
- Data mappings have been defined.

---

# Inputs

The following information may be required:

| Input | Required |
|---------|----------|
| Integration Design | Yes |
| Workflow Inputs | Yes |
| Data Mapping | Recommended |
| Business Rules | Recommended |
| Variable Naming Standard | Recommended |

---

# Procedure

## Step 1 — Identify Reusable Data

Identify information that will be referenced multiple times during workflow execution.

Typical examples include:

- Record identifiers
- Contact IDs
- Pipeline IDs
- HTTP responses
- API tokens
- Execution timestamps
- Correlation IDs
- Calculated values

Only store information that will be reused later in the workflow.

---

## Step 2 — Determine Variable Scope

Determine how long the value must remain available.

Typical scopes include:

- Current module
- Current route
- Entire scenario execution

Variables should remain available only for the duration required by the workflow.

---

## Step 3 — Apply a Naming Convention

Assign descriptive variable names.

Recommended format:

```text
camelCase
```

Examples:

```text
contactId

leadOwner

pipelineStage

requestPayload

executionTimestamp

correlationId
```

Avoid generic names such as:

```text
var1

temp

value

data

result
```

Variable names should clearly describe the stored information.

---

## Step 4 — Assign Variable Values

Populate variables using validated data.

Possible sources include:

- Trigger output
- Module output
- HTTP response
- Calculated value
- User input
- Aggregated data

Variable values should always originate from trusted and validated sources.

---

## Step 5 — Reuse Variables

Reference variables wherever the same information is required.

Typical uses include:

- HTTP requests
- Filter conditions
- Dynamic payloads
- Logging
- Notifications
- Database operations
- Data mapping

Avoid recalculating or retrieving information that has already been stored.

---

## Step 6 — Validate Variable Content

Verify that every variable contains:

- Expected value
- Correct data type
- Valid format
- Required information
- Non-null values when applicable

Validation should occur before variables are consumed by downstream modules.

---

## Step 7 — Minimize Variable Usage

Only create variables that provide measurable value.

Avoid storing:

- Static constants
- One-time values
- Data used by only one module
- Duplicate information

Excessive variables increase workflow complexity.

---

## Step 8 — Prevent Variable Confusion

Ensure that variables:

- Have unique names.
- Represent one business concept.
- Are not reassigned unnecessarily.
- Remain consistent throughout execution.

A variable should represent a single logical value.

---

## Step 9 — Document Variables

Record:

- Variable name
- Purpose
- Source
- Data type
- Scope
- Consumers

Documentation should enable future maintainers to understand why each variable exists.

---

# Validation

The procedure is considered successful when:

- Variables contain valid data.
- Variable names are descriptive.
- Duplicate variables are avoided.
- Data is reused efficiently.
- Variable scope is appropriate.
- Variable documentation is complete.

---

# Expected Result

Workflow data is stored and reused through clearly named, validated, and maintainable variables, reducing redundant processing and improving scenario readability.

---

# Common Errors

| Error | Cause | Impact |
|------|------|--------|
| Generic variable names | Poor naming convention | Difficult maintenance |
| Duplicate variables | Same data stored multiple times | Increased complexity |
| Invalid variable values | Missing validation | Workflow failures |
| Variables reused for different purposes | Poor design | Unpredictable behavior |
| Excessive variables | Overengineering | Reduced readability |

---

# Troubleshooting

| Problem | Resolution |
|----------|------------|
| Variable contains unexpected value | Verify the source module and mapping configuration. |
| Variable is empty | Confirm that the upstream module executed successfully and returned data. |
| Incorrect variable referenced | Review variable naming and ensure the correct variable is used. |
| Workflow becomes difficult to understand | Reduce the number of variables and simplify data flow. |
| Variable changes unexpectedly | Verify that the variable is not reassigned later in the workflow. |

---

# Rollback

If the variable configuration causes workflow issues:

1. Disable the affected scenario.
2. Remove or rename incorrect variables.
3. Restore the previous validated configuration.
4. Validate workflow execution.
5. Execute controlled testing before returning to production.

---

# Best Practices

- Create variables only when they improve workflow clarity.
- Use descriptive and consistent names.
- Store validated data only.
- Keep variable scope as small as possible.
- Reuse variables instead of duplicating calculations.
- Avoid reassigning variables unnecessarily.
- Remove unused variables during maintenance.
- Document every shared variable.
- Separate temporary variables from persistent storage.
- Review variables whenever workflow logic changes.

---

# References

- SOP-MAKE-001 — Create Scenario
- SOP-MAKE-004 — Configure Filters
- SOP-MAKE-005 — Configure Data Store
- SOP-MAKE-007 — Configure Scheduling
- SOP-INF-009 — Environment Variables
- SOP-INF-006 — Configure Logging
- SOP Template
- Integration Documentation Framework

---

# Revision History

| Version | Date | Author | Changes |
|----------|------|--------|---------|
| 1.0 | YYYY-MM-DD | Solution Architect | Initial version |