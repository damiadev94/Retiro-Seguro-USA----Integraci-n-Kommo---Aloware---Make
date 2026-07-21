```markdown id="6f0qka"
# SOP-MAKE-007 Configure Scheduling

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-MAKE-007 |
| Domain | Make |
| Title | Configure Scheduling |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

# Purpose

Define the standard procedure for configuring scheduled execution in Make scenarios.

Scheduling determines when and how often a scenario executes. A properly configured schedule ensures that workflows run at the correct frequency, meet business requirements, optimize resource consumption, and prevent unnecessary executions.

This SOP establishes a consistent approach for configuring scheduled scenarios across all integration projects.

---

# Scope

This SOP applies whenever a Make scenario is executed according to a predefined schedule.

Typical use cases include:

- Periodic data synchronization
- Batch processing
- Scheduled reporting
- Incremental imports
- Data reconciliation
- Maintenance workflows
- Cleanup processes
- Health checks
- Polling-based integrations

This SOP applies only to scheduled execution and does not cover event-driven triggers.

---

# Prerequisites

Before starting, verify that:

- The scenario has been created.
- The workflow has been implemented.
- Business execution frequency has been defined.
- Dependencies between scenarios are documented.
- Operational requirements have been approved.

---

# Inputs

The following information may be required:

| Input | Required |
|---------|----------|
| Integration Design | Yes |
| Business Requirements | Yes |
| Execution Frequency | Yes |
| Operational Window | Recommended |
| Time Zone | Recommended |

---

# Procedure

## Step 1 — Determine Scheduling Requirements

Identify when the workflow should execute.

Typical execution patterns include:

- Every few minutes
- Hourly
- Daily
- Weekly
- Monthly
- Business days only
- Custom intervals

The execution frequency should satisfy business requirements while minimizing unnecessary workload.

---

## Step 2 — Select the Scheduling Strategy

Choose the scheduling approach that best fits the workflow.

Typical strategies include:

- Fixed interval
- Specific time
- Daily schedule
- Weekly schedule
- Monthly schedule
- Business calendar schedule

The selected strategy should align with the business process.

---

## Step 3 — Configure the Time Zone

Select the appropriate time zone for execution.

Verify that:

- Business operating hours are respected.
- Daylight Saving Time requirements are understood.
- All dependent systems use compatible time references.

Scheduling should always use the agreed operational time zone.

---

## Step 4 — Define the Execution Frequency

Configure how often the scenario should execute.

Examples include:

- Every 5 minutes
- Every hour
- Every day at 02:00
- Every Monday at 08:00
- First day of each month

Avoid configuring intervals that are shorter than required by the business process.

---

## Step 5 — Prevent Overlapping Executions

Evaluate whether multiple executions could occur simultaneously.

When necessary:

- Ensure previous executions have completed.
- Prevent concurrent processing of the same records.
- Coordinate with dependent scenarios.
- Avoid race conditions.

Scheduled workflows should execute predictably without conflicting with themselves.

---

## Step 6 — Consider Platform Constraints

Review operational constraints that may affect scheduling.

Typical considerations include:

- API rate limits
- Business operating hours
- Maintenance windows
- Platform availability
- Data availability
- Expected execution duration

Scheduling should account for external system limitations.

---

## Step 7 — Configure Scenario Activation

Determine when the schedule becomes active.

Verify that:

- Testing has been completed.
- Production deployment has been approved.
- Required connections are available.
- Dependencies are operational.

Production schedules should only be enabled after successful validation.

---

## Step 8 — Validate Scheduled Execution

Execute a controlled test.

Verify that:

- The scenario starts at the expected time.
- Execution frequency is correct.
- Required modules execute successfully.
- Logs capture the execution.
- No duplicate runs occur.

The schedule should perform consistently under normal operating conditions.

---

## Step 9 — Document the Schedule

Record:

- Execution frequency
- Time zone
- Execution window
- Business purpose
- Dependencies
- Operational constraints

Documentation should allow future administrators to understand and maintain the scheduling configuration.

---

# Validation

The procedure is considered successful when:

- The scenario executes according to the defined schedule.
- The correct time zone is applied.
- Execution frequency matches business requirements.
- Concurrent executions are prevented when required.
- Operational constraints are respected.
- Scheduling configuration is documented.

---

# Expected Result

The scenario executes automatically according to the approved schedule, supporting reliable and predictable business operations while respecting operational constraints and platform limitations.

---

# Common Errors

| Error | Cause | Impact |
|------|------|--------|
| Incorrect execution frequency | Business requirements misunderstood | Missed or excessive processing |
| Wrong time zone | Time zone misconfiguration | Execution at incorrect times |
| Overlapping executions | Concurrency not considered | Duplicate processing |
| Schedule enabled before testing | Incomplete validation | Production failures |
| Excessive execution frequency | Poor scheduling design | Increased API consumption and operational cost |

---

# Troubleshooting

| Problem | Resolution |
|----------|------------|
| Scenario executes at the wrong time | Verify the configured time zone and scheduling settings. |
| Scenario executes too frequently | Review the execution interval and business requirements. |
| Scenario does not execute | Confirm that scheduling is enabled and the scenario is active. |
| Duplicate executions occur | Review concurrency controls and execution duration. |
| External systems reject requests | Adjust the schedule to comply with maintenance windows or rate limits. |

---

# Rollback

If the scheduling configuration causes operational issues:

1. Disable the scenario schedule.
2. Restore the previous validated scheduling configuration.
3. Verify operational dependencies.
4. Execute controlled testing.
5. Re-enable scheduling after successful validation.

---

# Best Practices

- Schedule workflows only as frequently as required.
- Use business operating hours whenever appropriate.
- Consider API rate limits during schedule design.
- Avoid overlapping executions.
- Coordinate schedules between dependent scenarios.
- Validate scheduling in a non-production environment before activation.
- Document every scheduling decision.
- Monitor execution frequency after deployment.
- Review schedules whenever business processes change.
- Disable unused or obsolete scheduled scenarios.

---

# References

- SOP-MAKE-001 — Create Scenario
- SOP-MAKE-002 — Configure Trigger
- SOP-MAKE-005 — Configure Data Store
- SOP-MAKE-006 — Configure Variables
- SOP-MAKE-008 — Configure Error Routes
- SOP-MAKE-009 — Test Scenario
- SOP-MAKE-010 — Deploy Scenario
- SOP-INF-005 — Configure Retry Policy
- SOP-INF-006 — Configure Logging
- SOP Template
- Integration Documentation Framework

---

# Revision History

| Version | Date | Author | Changes |
|----------|------|--------|---------|
| 1.0 | YYYY-MM-DD | Solution Architect | Initial version |
```
