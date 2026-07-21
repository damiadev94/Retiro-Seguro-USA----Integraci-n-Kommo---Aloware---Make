````markdown id="fcf9kd"
# SOP-MAKE-005 Configure Data Store

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-MAKE-005 |
| Domain | Make |
| Title | Configure Data Store |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

# Purpose

Define the standard procedure for configuring and using Data Stores within Make.

Data Stores provide persistent storage that remains available across multiple scenario executions. They are used to retain workflow state, prevent duplicate processing, maintain execution checkpoints, and store lightweight operational data required by integration workflows.

This SOP establishes a consistent approach for designing, configuring, and maintaining Data Stores within Make.

---

# Scope

This SOP applies whenever persistent data storage is required inside Make.

Typical use cases include:

- Deduplication records
- Execution checkpoints
- Synchronization state
- Mapping tables
- Correlation identifiers
- Retry tracking
- Processing history
- Temporary business cache
- Workflow state management

This SOP applies only to Make Data Stores.

External databases and enterprise persistence layers are outside the scope of this document.

---

# Prerequisites

Before starting, verify that:

- The scenario has been designed.
- Persistent storage requirements have been identified.
- Data retention requirements are documented.
- Business keys have been defined.
- Data ownership has been established.

---

# Inputs

The following information may be required:

| Input | Required |
|---------|----------|
| Integration Design | Yes |
| Persistent Data Requirements | Yes |
| Primary Key Definition | Yes |
| Data Retention Policy | Recommended |
| Business Rules | Recommended |

---

# Procedure

## Step 1 — Determine Whether a Data Store Is Required

Confirm that persistent storage is necessary.

Typical situations include:

- Prevent duplicate processing
- Store execution checkpoints
- Maintain synchronization state
- Preserve mapping information
- Track processed records
- Cache operational data

Do not use a Data Store when temporary variables are sufficient.

---

## Step 2 — Define the Data Model

Identify the information that will be stored.

Typical attributes include:

- Unique identifier
- External identifier
- Internal identifier
- Status
- Timestamp
- Processing state
- Retry count
- Correlation ID

Store only the data required by the business process.

---

## Step 3 — Define the Primary Key

Select a unique key that identifies each record.

Examples include:

- Contact ID
- Lead ID
- Order ID
- External Reference
- Composite Business Key
- Correlation Identifier

Primary keys should remain stable throughout the lifecycle of the stored record.

---

## Step 4 — Create the Data Store

Create a new Data Store in the appropriate Make environment.

Verify:

- Correct organization
- Correct team
- Appropriate name
- Defined data structure

The Data Store should be dedicated to a single business purpose.

---

## Step 5 — Apply the Naming Convention

Assign a descriptive name.

Recommended format:

```text
<Entity> State

<Entity> Mapping

<Entity> Cache

<Entity> History
```

Examples:

```text
Contact Mapping

Lead State

Call History

Retry Queue

Execution Checkpoints
```

The name should clearly describe the Data Store's responsibility.

---

## Step 6 — Configure Read and Write Operations

Define how scenarios interact with the Data Store.

Typical operations include:

- Create record
- Read record
- Update record
- Delete record
- Search records
- Check existence

Every operation should preserve data consistency.

---

## Step 7 — Prevent Duplicate Records

Before creating a new record:

- Verify whether the key already exists.
- Update existing records when appropriate.
- Avoid creating duplicate entries.

Deduplication should rely on business identifiers rather than execution order.

---

## Step 8 — Define Data Lifecycle

Establish how records are maintained over time.

Consider:

- Record creation
- Record updates
- Retention period
- Cleanup strategy
- Archiving requirements
- Deletion policy

Data lifecycle rules should align with operational requirements.

---

## Step 9 — Validate the Configuration

Verify that:

- Records can be created.
- Records can be retrieved.
- Updates function correctly.
- Duplicate records are prevented.
- Lookup performance is acceptable.
- Data integrity is maintained.

---

## Step 10 — Document the Data Store

Record:

- Name
- Business purpose
- Stored entities
- Primary key
- Stored attributes
- Data lifecycle
- Related scenarios

Documentation should enable future maintainers to understand why the Data Store exists and how it is used.

---

# Validation

The procedure is considered successful when:

- Persistent data is stored correctly.
- Records can be retrieved reliably.
- Duplicate records are prevented.
- Primary keys uniquely identify records.
- Data lifecycle rules are defined.
- Configuration is documented.

---

# Expected Result

A properly configured Data Store provides reliable persistent storage that supports workflow continuity, state management, and operational consistency across multiple scenario executions.

---

# Common Errors

| Error | Cause | Impact |
|------|------|--------|
| Using a Data Store for temporary values | Incorrect persistence strategy | Unnecessary complexity |
| Duplicate records | Missing uniqueness validation | Data inconsistency |
| Poor primary key selection | Unstable identifiers | Difficult synchronization |
| Excessive stored attributes | Overengineering | Reduced maintainability |
| Missing cleanup policy | Unlimited data growth | Operational inefficiency |

---

# Troubleshooting

| Problem | Resolution |
|----------|------------|
| Duplicate records appear | Verify primary key selection and existence checks before record creation. |
| Records cannot be found | Confirm lookup keys and search criteria. |
| Data becomes inconsistent | Review update logic and ensure records are modified rather than recreated. |
| Data Store grows excessively | Implement retention and cleanup procedures. |
| Scenario performance decreases | Review lookup strategy and remove unnecessary stored data. |

---

# Rollback

If the Data Store configuration causes operational issues:

1. Suspend affected scenarios.
2. Restore the previous validated Data Store configuration.
3. Verify record integrity.
4. Correct the data model or primary key if necessary.
5. Execute controlled testing before returning to production.

---

# Best Practices

- Use Data Stores only for persistent operational data.
- Assign one business responsibility to each Data Store.
- Select stable business identifiers as primary keys.
- Prevent duplicate record creation.
- Keep the stored schema as small as possible.
- Define a clear retention policy.
- Document every stored attribute.
- Validate data before writing to the Data Store.
- Separate operational persistence from business databases.
- Review Data Store contents periodically to remove obsolete records.

---

# References

- SOP-MAKE-001 — Create Scenario
- SOP-MAKE-004 — Configure Filters
- SOP-MAKE-006 — Configure Variables
- SOP-MAKE-008 — Configure Error Routes
- SOP-MAKE-009 — Test Scenario
- SOP-INF-006 — Configure Logging
- SOP Template
- Integration Documentation Framework

---

# Revision History

| Version | Date | Author | Changes |
|----------|------|--------|---------|
| 1.0 | YYYY-MM-DD | Solution Architect | Initial version |
````
