````markdown
# SOP-INF-002 Configure Shared Variables

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-INF-002 |
| Domain | Infrastructure |
| Title | Configure Shared Variables |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

# Purpose

Define the standard procedure for creating, organizing, and maintaining shared variables used across integration scenarios.

Shared variables centralize reusable configuration values, reducing duplication, simplifying maintenance, and ensuring consistency across multiple workflows and environments.

This SOP establishes best practices for managing variables that are referenced by multiple scenarios within the integration platform.

---

# Scope

This SOP applies whenever configuration values are reused across two or more integration scenarios.

Typical shared variables include:

- Environment identifiers
- API endpoints
- Default IDs
- Configuration flags
- Timeout values
- Retry limits
- Business constants
- Feature flags
- Default pipeline identifiers
- Default owner identifiers

Sensitive values such as API Keys, Client Secrets, and Access Tokens are **not** covered by this SOP and must be managed according to **SOP-INF-010 — Secrets Management**.

---

# Prerequisites

Before starting, verify that:

- The project structure has been established.
- Naming conventions have been defined.
- Required environments have been identified.
- Configuration requirements have been documented.
- Shared values have been distinguished from secrets.

---

# Inputs

The following information may be required:

| Input | Required |
|---------|----------|
| Environment Name | Yes |
| Platform Configuration | Yes |
| Shared Configuration Values | Yes |
| Variable Naming Convention | Yes |
| Business Requirements | Recommended |

---

# Procedure

## Step 1 — Identify Shared Configuration

Review the integration design and identify configuration values that are reused across multiple scenarios.

Examples include:

- Base API URLs
- Pipeline IDs
- Stage IDs
- Default owners
- Business constants
- Retry limits
- Timeout values

Only values used by multiple scenarios should be considered shared variables.

---

## Step 2 — Separate Variables from Secrets

Determine whether each value is a configuration variable or a secret.

Examples of shared variables:

```text
DEFAULT_PIPELINE_ID

DEFAULT_STAGE_ID

REQUEST_TIMEOUT

MAX_RETRY_ATTEMPTS

LOG_LEVEL
```

Examples of secrets:

```text
API_KEY

CLIENT_SECRET

ACCESS_TOKEN
```

Secrets must never be stored as shared configuration variables.

---

## Step 3 — Apply the Naming Convention

Assign descriptive names following the organization's naming standard.

General rules:

- Use uppercase letters.
- Separate words with underscores.
- Use meaningful names.
- Avoid abbreviations unless universally recognized.

Examples:

```text
DEFAULT_PIPELINE_ID

DEFAULT_OWNER_ID

REQUEST_TIMEOUT

MAX_RETRY_ATTEMPTS

LOG_LEVEL
```

Avoid names such as:

```text
VALUE1

CONFIG

DATA

TEST
```

---

## Step 4 — Group Variables Logically

Organize variables according to their functional domain.

Example:

```text
KOMMO_*

ALOWARE_*

MAKE_*

HTTP_*

LOGGING_*

SYSTEM_*
```

Grouping improves readability and simplifies maintenance.

---

## Step 5 — Define Default Values

Assign default values whenever appropriate.

Examples:

```text
REQUEST_TIMEOUT = 30

MAX_RETRY_ATTEMPTS = 3

LOG_LEVEL = INFO
```

Default values should be reviewed before deployment to production.

---

## Step 6 — Reference Variables Consistently

Configure scenarios to reference shared variables instead of hardcoded values.

Benefits include:

- centralized configuration;
- simplified updates;
- improved consistency;
- reduced maintenance effort.

Changes should require updating the variable only once.

---

## Step 7 — Document Shared Variables

Maintain documentation for every shared variable.

Recommended attributes:

| Attribute | Description |
|-----------|-------------|
| Name | Variable identifier |
| Purpose | Business or technical purpose |
| Data Type | String, Number, Boolean, etc. |
| Default Value | If applicable |
| Used By | Related scenarios or services |
| Environment | Development, Testing, Production |

Document variable usage without exposing sensitive information.

---

## Step 8 — Validate Configuration

Verify that:

- Variable names follow the naming convention.
- Variables are referenced consistently.
- No duplicate variables exist.
- No secrets are stored as shared variables.
- Every shared variable is documented.

---

# Validation

The procedure is considered successful when:

- Shared configuration values are centralized.
- Variable names comply with the naming convention.
- Multiple scenarios reference the same variables.
- Hardcoded configuration values have been eliminated where appropriate.
- Documentation accurately describes all shared variables.

---

# Expected Result

A centralized and standardized collection of shared variables is available for use across integration scenarios, improving consistency, maintainability, and configuration management.

---

# Common Errors

| Error | Cause | Impact |
|------|------|--------|
| Hardcoded configuration values | Shared variables not used | Increased maintenance effort |
| Duplicate variables | Poor governance | Configuration inconsistency |
| Ambiguous variable names | Naming convention ignored | Reduced readability |
| Secrets stored as variables | Incorrect classification | Security risk |
| Unused variables accumulate | Lack of periodic review | Configuration clutter |

---

# Troubleshooting

| Problem | Resolution |
|----------|------------|
| Multiple variables represent the same value | Consolidate them into a single shared variable and update all references. |
| Configuration changes require editing multiple scenarios | Replace duplicated values with shared variables. |
| Variable purpose is unclear | Rename the variable following the naming convention and update its documentation. |
| Sensitive information found in shared variables | Remove the value immediately and migrate it to the approved secrets management solution. |

---

# Rollback

If shared variables were configured incorrectly:

1. Restore the previous validated configuration.
2. Remove duplicate or obsolete variables.
3. Reconfigure affected scenarios.
4. Validate all references.
5. Confirm that integrations execute successfully after the update.

---

# Best Practices

- Centralize reusable configuration values.
- Use descriptive variable names.
- Keep configuration independent of implementation logic.
- Avoid duplicate variables.
- Document every shared variable.
- Review shared variables periodically.
- Remove obsolete configuration values.
- Never store secrets as shared variables.
- Keep environment-specific values isolated.

---

# References

- SOP-INF-009 — Environment Variables
- SOP-INF-010 — Secrets Management
- SOP-INF-008 — Naming Convention
- SOP-INF-007 — Folder Structure
- SOP Template
- Integration Documentation Framework

---

# Revision History

| Version | Date | Author | Changes |
|----------|------|--------|---------|
| 1.0 | YYYY-MM-DD | Solution Architect | Initial version |
````
