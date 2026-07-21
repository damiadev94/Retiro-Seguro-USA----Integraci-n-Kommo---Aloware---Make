# SOP-MAKE-003 Configure Router

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-MAKE-003 |
| Domain | Make |
| Title | Configure Router |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

# Purpose

Define the standard procedure for configuring Routers in Make scenarios.

Routers enable a workflow to branch into multiple execution paths based on business conditions. Proper router design improves scenario readability, modularity, scalability, and maintainability by separating independent business processes into clearly defined routes.

This SOP establishes a consistent approach for implementing routing logic within Make scenarios.

---

# Scope

This SOP applies whenever a Make scenario requires multiple execution paths.

Typical use cases include:

- Conditional business logic
- Multiple event types
- Platform-specific processing
- Record classification
- Parallel processing
- Error routing
- Notification workflows
- Environment-specific execution

This SOP focuses exclusively on Router configuration. Route conditions are documented separately in **SOP-MAKE-004 — Configure Filters**.

---

# Prerequisites

Before starting, verify that:

- The scenario has been created.
- The trigger has been configured.
- Business decision points have been identified.
- Routing logic has been documented.
- Required modules have been defined.

---

# Inputs

The following information may be required:

| Input | Required |
|---------|----------|
| Integration Design | Yes |
| Business Rules | Yes |
| Trigger Output | Yes |
| Route Definitions | Recommended |
| Workflow Diagram | Recommended |

---

# Procedure

## Step 1 — Identify Decision Points

Determine where the workflow must split into multiple execution paths.

Typical decision points include:

- Record status
- Object type
- Event type
- Customer category
- Environment
- Processing outcome
- Business rules

Each router should represent a single business decision.

---

## Step 2 — Determine Route Responsibilities

Define the purpose of each route.

Each route should perform one clearly defined responsibility.

Examples include:

- Create record
- Update record
- Delete record
- Send notification
- Synchronize data
- Archive information
- Execute error handling

Avoid combining unrelated business processes within the same route.

---

## Step 3 — Insert the Router Module

Add a Router immediately after the module where the business decision occurs.

The router should be placed only when the workflow genuinely branches into independent execution paths.

Do not insert routers unnecessarily.

---

## Step 4 — Create the Required Routes

Create one route for each business outcome.

Examples:

```text
Lead Created
      │
      ▼
    Router
     │
 ┌───┼─────────────┐
 │   │             │
 ▼   ▼             ▼
Create Update   Ignore
```

Each route should represent one possible workflow outcome.

---

## Step 5 — Organize the Routes

Arrange routes logically.

Recommended practices include:

- Place primary routes first.
- Group similar operations.
- Minimize crossed connections.
- Keep execution flow left to right.
- Maintain visual consistency.

Readable scenarios are easier to maintain.

---

## Step 6 — Configure Route Filters

Assign a filter to each route that determines when it should execute.

Every route should have an explicit condition.

Filter configuration is documented in **SOP-MAKE-004 — Configure Filters**.

---

## Step 7 — Validate Route Independence

Verify that each route operates independently.

Confirm that:

- One route does not depend on another.
- Shared modules are placed before the router.
- Duplicate processing cannot occur.
- Business responsibilities remain separated.

Independent routes improve maintainability.

---

## Step 8 — Execute Test Scenarios

Generate representative input data for every business case.

Verify that:

- The correct route executes.
- Unrelated routes remain inactive.
- Expected modules are executed.
- Workflow behavior matches business requirements.

Every route should be validated individually.

---

## Step 9 — Document the Router

Record:

- Router purpose
- Business decision
- Route descriptions
- Filter references
- Dependencies
- Expected execution behavior

Documentation should allow future maintainers to understand the routing strategy without inspecting the entire scenario.

---

# Validation

The procedure is considered successful when:

- Business decision points are correctly identified.
- Each route has a single responsibility.
- Every route has an associated filter.
- Only the intended route executes for each event.
- Routing behavior matches the integration design.
- Router configuration is documented.

---

# Expected Result

The scenario branches into clearly defined, independent execution paths, allowing business logic to be processed in a modular, scalable, and maintainable manner.

---

# Common Errors

| Error | Cause | Impact |
|------|------|--------|
| Router added unnecessarily | No real branching required | Increased scenario complexity |
| Multiple responsibilities in one route | Poor workflow design | Difficult maintenance |
| Missing route filters | All routes execute | Incorrect processing |
| Duplicate business logic | Logic copied across routes | Higher maintenance effort |
| Shared modules placed after the router | Incorrect architecture | Inconsistent execution |

---

# Troubleshooting

| Problem | Resolution |
|----------|------------|
| Every route executes | Verify that filters have been configured correctly for each route. |
| Incorrect route executes | Review filter conditions and business rules. |
| Duplicate processing occurs | Ensure that route conditions are mutually exclusive when appropriate. |
| Workflow becomes difficult to understand | Separate responsibilities into additional routes or scenarios. |
| Shared logic is duplicated across routes | Move common modules before the router whenever possible. |

---

# Rollback

If the router configuration introduces workflow issues:

1. Disable the affected scenario.
2. Remove or simplify the router configuration.
3. Restore the previous validated workflow.
4. Verify route logic.
5. Execute controlled testing before returning to production.

---

# Best Practices

- Use one router for one business decision.
- Keep routes independent.
- Assign a single responsibility to each route.
- Configure explicit filters for every route.
- Place shared processing before the router.
- Minimize duplicated logic across routes.
- Organize routes for readability.
- Document the purpose of every route.
- Validate every route independently.
- Refactor overly complex routing structures into multiple scenarios when appropriate.

---

# References

- SOP-MAKE-001 — Create Scenario
- SOP-MAKE-002 — Configure Trigger
- SOP-MAKE-004 — Configure Filters
- SOP-MAKE-008 — Configure Error Routes
- SOP-MAKE-009 — Test Scenario
- SOP-INF-008 — Naming Convention
- SOP Template
- Integration Documentation Framework

---

# Revision History

| Version | Date | Author | Changes |
|----------|------|--------|---------|
| 1.0 | YYYY-MM-DD | Solution Architect | Initial version |