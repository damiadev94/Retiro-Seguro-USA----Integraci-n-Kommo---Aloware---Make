# SOP-MAKE-001 Create Scenario

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-MAKE-001 |
| Domain | Make |
| Title | Create Scenario |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

# Purpose

Define the standard procedure for creating a new scenario in Make.

A consistent scenario creation process establishes a solid foundation for workflow implementation, promotes maintainability, improves readability, and ensures that all integration projects follow the same architectural standards.

This SOP standardizes the initial configuration of Make scenarios before any business logic is implemented.

---

# Scope

This SOP applies whenever a new integration workflow is created in Make.

Typical use cases include:

- New API integrations
- Webhook-based workflows
- Scheduled synchronizations
- Event-driven automations
- Data synchronization processes
- Batch processing workflows
- Internal automation scenarios

This SOP applies only to scenario creation and initial configuration.

---

# Prerequisites

Before starting, verify that:

- Access to the Make organization has been granted.
- The appropriate team has been selected.
- Required platform connections are available.
- Environment variables have been defined.
- Project documentation has been approved.

---

# Inputs

The following information may be required:

| Input | Required |
|---------|----------|
| Integration Design | Yes |
| Scenario Name | Yes |
| Environment | Yes |
| Required Connections | Recommended |
| Business Requirements | Recommended |

---

# Procedure

## Step 1 — Review the Integration Design

Review the implementation documentation before creating the scenario.

Confirm:

- Workflow objectives
- Trigger type
- Target systems
- Required integrations
- Expected outputs

The scenario should only be created after the implementation design has been approved.

---

## Step 2 — Create the Scenario

Create a new scenario within the appropriate Make team and workspace.

Verify that:

- The correct organization is selected.
- The correct team is selected.
- The scenario is created in the intended environment.

---

## Step 3 — Apply the Naming Convention

Assign a descriptive and standardized name.

Recommended format:

```text
<Source System> → <Destination System> | <Business Process>
```

Examples:

```text
Kommo → Aloware | Assign Contact

Aloware → Kommo | Synchronize Call

Shopify → ERP | Create Order
```

Scenario names should clearly describe their primary responsibility.

---

## Step 4 — Configure the Scenario Description

Add a description summarizing:

- Business purpose
- Trigger source
- Target systems
- High-level workflow
- Related documentation

The description should provide sufficient context for future maintenance.

---

## Step 5 — Configure Basic Scenario Settings

Review the default scenario configuration.

Typical settings include:

- Execution mode
- Scheduling state
- Error handling behavior
- Sequential execution requirements
- Data retention settings

Configuration should align with project standards.

---

## Step 6 — Add the Initial Trigger

Insert the first module representing the workflow trigger.

Examples include:

- Webhook
- Scheduler
- HTTP request
- Email trigger
- CRM event
- Queue listener

Trigger configuration is documented in **SOP-MAKE-002 — Configure Trigger**.

---

## Step 7 — Organize the Workspace

Arrange the scenario canvas for readability.

Recommended practices include:

- Maintain left-to-right execution flow.
- Group related modules.
- Leave sufficient spacing.
- Minimize connector crossings.
- Preserve logical sequence.

A well-organized canvas improves maintainability.

---

## Step 8 — Save the Scenario

Save the scenario after completing the initial configuration.

Verify that:

- Naming is correct.
- Description has been completed.
- Initial trigger has been added.
- Configuration has been preserved.

---

## Step 9 — Validate the Scenario

Verify that:

- The scenario appears in the correct workspace.
- Naming follows the established convention.
- No configuration errors are present.
- Required connections are available.
- The initial trigger is correctly configured.

The scenario is now ready for implementation.

---

# Validation

The procedure is considered successful when:

- The scenario exists in the correct environment.
- Naming follows organizational standards.
- The description is complete.
- Initial configuration is correct.
- The trigger has been added.
- The scenario is ready for workflow implementation.

---

# Expected Result

A properly configured Make scenario is created, documented, and prepared for implementation according to organizational standards.

---

# Common Errors

| Error | Cause | Impact |
|------|------|--------|
| Incorrect scenario name | Naming convention not followed | Difficult maintenance |
| Wrong environment | Scenario created in incorrect workspace | Deployment risk |
| Missing description | Poor documentation | Reduced maintainability |
| Incorrect trigger selection | Implementation misunderstanding | Workflow redesign required |
| Poor canvas organization | Lack of structure | Difficult future maintenance |

---

# Troubleshooting

| Problem | Resolution |
|----------|------------|
| Scenario created in the wrong team | Move or recreate the scenario in the correct workspace. |
| Naming does not follow standards | Rename the scenario according to the approved naming convention. |
| Required connection is unavailable | Create or verify the connection before continuing implementation. |
| Trigger type is incorrect | Replace the trigger before adding additional modules. |
| Scenario layout becomes difficult to read | Reorganize modules before implementation progresses. |

---

# Rollback

If the scenario was created incorrectly:

1. Stop implementation activities.
2. Delete the incorrectly configured scenario if it has not been used.
3. Create a new scenario following this SOP.
4. Verify naming and configuration.
5. Resume implementation only after validation.

---

# Best Practices

- Create one scenario for one business responsibility.
- Keep scenarios focused and modular.
- Follow the standard naming convention.
- Document the business purpose immediately.
- Configure the trigger before adding additional modules.
- Organize the canvas from the beginning.
- Avoid implementing business logic before validating the scenario structure.
- Review scenario configuration before development starts.
- Keep scenarios easy to understand for future maintainers.
- Align every scenario with the approved implementation design.

---

# References

- SOP-MAKE-002 — Configure Trigger
- SOP-MAKE-003 — Configure Router
- SOP-MAKE-004 — Configure Filters
- SOP-MAKE-008 — Configure Error Routes
- SOP-MAKE-009 — Test Scenario
- SOP-MAKE-010 — Deploy Scenario
- SOP-INF-008 — Naming Convention
- SOP Template
- Integration Documentation Framework

---

# Revision History

| Version | Date | Author | Changes |
|----------|------|--------|---------|
| 1.0 | YYYY-MM-DD | Solution Architect | Initial version |