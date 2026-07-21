# SOP Template

## Purpose

This document defines the standard structure that every Standard Operating Procedure (SOP) within the SOP Library must follow.

Its objective is to ensure that all procedures are consistent, predictable, reusable, and easy to maintain, regardless of the technology, platform, or integration project.

This template standardizes both the organization of information and the level of detail expected in every SOP.

---

# Scope

This template applies to every SOP contained in the SOP Library, including all current and future domains.

Examples include:

- Infrastructure
- HTTP
- Make
- Kommo
- Aloware
- Testing
- Operations

No SOP should deviate from this template unless explicitly approved.

---

# Design Principles

Every SOP should follow these principles:

- One procedure per document.
- One objective per procedure.
- Sequential and deterministic execution.
- Clear prerequisites.
- Verifiable completion.
- Minimal ambiguity.
- Technology-specific when necessary.
- Reusable across projects.

The template prioritizes operational clarity over theoretical explanation.

---

# Standard Document Structure

Every SOP must use the following structure.

```markdown
# SOP-XXX-000 Title

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-XXX-000 |
| Version | 1.0 |
| Status | Draft |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

## Purpose

Describe the objective of the procedure.

---

## Scope

Define when this SOP should be used and its boundaries.

---

## Prerequisites

List all required conditions before starting.

---

## Inputs

Describe the information, credentials, tools or resources required.

---

## Procedure

Describe the procedure as an ordered sequence of steps.

---

## Validation

Explain how to verify that the procedure completed successfully.

---

## Expected Result

Describe the expected outcome after successful completion.

---

## Common Errors

List the most common implementation errors.

---

## Troubleshooting

Describe how to resolve common issues.

---

## Rollback

Describe how to safely revert the procedure if necessary.

---

## References

List related SOPs and documentation.

---

## Revision History

| Version | Date | Author | Changes |
|----------|------|--------|---------|
```

---

# Section Guidelines

## Metadata

Provides basic document information.

Required fields:

- Identifier
- Version
- Status
- Owner
- Last Updated

---

## Purpose

Clearly state what the procedure accomplishes.

The purpose should answer:

> Why does this SOP exist?

Keep this section concise.

---

## Scope

Define:

- when the SOP applies;
- when it should not be used;
- systems involved;
- implementation boundaries.

---

## Prerequisites

Describe everything that must already exist before execution.

Examples:

- Administrator access
- API credentials
- Existing Make connection
- OAuth authorization
- Customer approval

If there are no prerequisites, explicitly state:

> None.

---

## Inputs

Document everything consumed by the procedure.

Examples:

- URLs
- API Keys
- Tokens
- IDs
- Configuration values
- Environment variables
- Customer information

---

## Procedure

This is the core of the SOP.

Requirements:

- Use numbered steps.
- One action per step.
- Keep instructions imperative and explicit.
- Avoid combining multiple actions into a single step.
- Follow the actual execution order.
- Include platform navigation when relevant.

Example:

```text
1. Open the Make dashboard.

2. Navigate to Connections.

3. Click Create Connection.

4. Select HTTP.

5. Configure OAuth.

6. Save the connection.
```

---

## Validation

Describe how to confirm the procedure succeeded.

Examples:

- HTTP 200 received
- Connection status is Active
- Webhook test successful
- Scenario executes successfully
- API authentication verified

Validation must be objective.

---

## Expected Result

Describe the final expected state after successful execution.

Examples:

- Make connection is operational.
- Webhook is receiving events.
- API authentication is valid.
- Scenario is enabled.

---

## Common Errors

Document recurring operational issues.

For each error include:

- Description
- Cause
- Impact

Example:

| Error | Cause | Impact |
|------|------|--------|
| Invalid OAuth Redirect URI | Incorrect configuration | Authentication fails |

---

## Troubleshooting

Describe corrective actions for common issues.

Whenever possible, map solutions directly to the errors listed in the previous section.

Example:

```text
Problem

Authentication Failed

Solution

Verify Client ID, Client Secret and Redirect URI.
```

---

## Rollback

Describe how to safely undo the procedure.

If rollback is not applicable, explicitly state:

> No rollback procedure is required.

---

## References

Include related documentation.

Examples:

- Related SOPs
- Runbooks
- Implementation Guides
- Vendor Documentation
- Architecture Documents

Always reference documents by their identifiers whenever possible.

---

## Revision History

Track every modification.

Example:

| Version | Date | Author | Changes |
|----------|------|--------|---------|
| 1.0 | 2026-07-21 | Solution Architect | Initial version |

---

# Writing Rules

Every SOP should:

- describe one procedure only;
- use imperative language;
- avoid unnecessary explanations;
- describe actions, not concepts;
- remain implementation-oriented;
- be reproducible by another engineer.

---

# Optional Sections

When appropriate, an SOP may include:

- Warnings
- Notes
- Tips
- Screenshots
- Diagrams
- Code Examples
- API Examples
- Configuration Tables

Optional sections should appear after the relevant step rather than grouped at the end.

---

# Quality Checklist

Before approving a new SOP, verify that:

- The identifier follows the naming convention.
- The document uses the standard template.
- The purpose is clearly defined.
- All prerequisites are documented.
- Every step is actionable.
- Validation criteria are objective.
- Expected results are measurable.
- Common errors are documented.
- Rollback instructions are included or explicitly marked as not applicable.
- References are complete.
- Revision history has been initialized.

---

# Related Documents

- README
- SOP Naming Convention
- SOP Lifecycle

---

# Status

| Property | Value |
|----------|-------|
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |