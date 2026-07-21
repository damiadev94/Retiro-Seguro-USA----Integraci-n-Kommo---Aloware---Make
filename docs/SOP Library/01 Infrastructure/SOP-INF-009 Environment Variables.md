# SOP-INF-009 Environment Variables

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-INF-009 |
| Domain | Infrastructure |
| Title | Environment Variables |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

# Purpose

Define the standard process for creating, organizing, documenting, and maintaining environment variables used by integration projects.

Environment variables provide a centralized mechanism for storing configuration values that differ between environments or contain information that should not be hardcoded into implementation logic.

Proper management of environment variables improves portability, security, maintainability, and deployment consistency across Development, Testing, Staging, and Production environments.

---

# Scope

This SOP applies to all integration projects that require configurable runtime values.

Typical environment variables include:

- API endpoints
- OAuth credentials
- API tokens
- Client IDs
- Client Secrets
- Environment identifiers
- Feature flags
- Timeout values
- Retry configuration
- Logging configuration
- Database connection parameters

Sensitive values such as passwords and secrets are governed by **SOP-INF-010 — Secrets Management**.

---

# Prerequisites

- Project infrastructure has been created.
- Naming conventions have been established.
- Required platforms have been identified.
- Required configuration parameters have been documented.

---

# Inputs

Before defining environment variables, collect:

- Platform configuration
- API documentation
- Authentication requirements
- Environment definitions
- Runtime configuration requirements

---

# Procedure

## Step 1 — Identify Configuration Values

Identify every value that may vary between environments or deployments.

Examples include:

- Base URLs
- API versions
- Authentication parameters
- Feature flags
- Operational limits
- Timeout values

Avoid embedding configurable values directly into implementation logic.

---

## Step 2 — Separate Configuration from Secrets

Classify each configuration value.

### Environment Variables

Examples:

```text
API_BASE_URL
API_VERSION
DEFAULT_PIPELINE_ID
LOG_LEVEL
REQUEST_TIMEOUT
```

### Secrets

Examples:

```text
CLIENT_SECRET
API_KEY
ACCESS_TOKEN
PRIVATE_KEY
```

Sensitive values should be managed according to the Secrets Management SOP.

---

## Step 3 — Apply Standard Naming

Environment variable names should:

- use uppercase letters;
- separate words with underscores;
- be descriptive;
- remain platform-independent whenever possible.

Examples:

```text
KOMMO_BASE_URL

KOMMO_CLIENT_ID

ALOWARE_API_URL

DEFAULT_OWNER_ID

REQUEST_TIMEOUT

MAX_RETRY_ATTEMPTS
```

Avoid abbreviated or ambiguous names.

---

## Step 4 — Group Variables by Platform

Organize variables logically.

Example:

```text
KOMMO_*

ALOWARE_*

MAKE_*

SMTP_*

LOGGING_*
```

Logical grouping improves discoverability and maintenance.

---

## Step 5 — Define Default Values

When appropriate, define safe default values.

Example:

```text
REQUEST_TIMEOUT = 30

MAX_RETRY_ATTEMPTS = 3

LOG_LEVEL = INFO
```

Defaults should be documented and reviewed before production deployment.

---

## Step 6 — Document Every Variable

Each environment variable should be documented.

Recommended attributes include:

| Attribute | Description |
|-----------|-------------|
| Name | Variable identifier |
| Purpose | Business or technical purpose |
| Required | Yes / No |
| Default Value | If applicable |
| Example | Non-sensitive example |
| Used By | Systems or scenarios |

Example:

| Property | Value |
|----------|-------|
| Name | KOMMO_BASE_URL |
| Purpose | Kommo API endpoint |
| Required | Yes |
| Default | None |
| Used By | Kommo HTTP Requests |

---

## Step 7 — Create Environment-Specific Configurations

Maintain independent configuration sets for each environment.

Example:

```text
Development

Testing

Staging

Production
```

Each environment should contain only the values required for its operation.

---

## Step 8 — Validate Configuration

Before deployment, verify that:

- every required variable exists;
- values are correctly formatted;
- references are valid;
- required variables are populated;
- unused variables have been removed.

---

# Validation

The procedure is considered successful when:

- All required configuration values are externalized.
- Variable names follow the standard naming convention.
- Environment-specific values are separated correctly.
- No configurable values remain hardcoded.
- Documentation accurately reflects the runtime configuration.

---

# Expected Result

The project contains a complete, organized, and documented set of environment variables that enables consistent deployments across all supported environments without requiring code or scenario modifications.

---

# Common Errors

| Error | Cause | Impact |
|------|------|--------|
| Hardcoded configuration values | Variables not externalized | Difficult maintenance |
| Inconsistent variable names | Naming convention not followed | Configuration confusion |
| Missing required variables | Incomplete configuration | Runtime failures |
| Shared configuration across environments | Poor environment separation | Deployment risks |
| Undocumented variables | Missing documentation | Operational uncertainty |

---

# Troubleshooting

| Problem | Resolution |
|----------|------------|
| Configuration differs between environments | Compare environment variable sets and synchronize required values. |
| Variable not recognized | Verify spelling, naming convention, and platform configuration. |
| Runtime configuration failure | Confirm all required variables are defined before deployment. |
| Duplicate configuration values | Consolidate duplicated variables into a single authoritative definition. |

---

# Rollback

If incorrect environment variables were introduced:

1. Restore the previous validated configuration.
2. Remove invalid or obsolete variables.
3. Reapply the approved configuration set.
4. Validate all dependent integrations.
5. Perform a deployment verification before resuming operations.

---

# Best Practices

- Externalize all configurable values.
- Keep environment configurations independent.
- Document every variable.
- Use meaningful and descriptive names.
- Remove unused variables regularly.
- Minimize the number of required variables.
- Review configuration during every release.
- Never hardcode values that may change between environments.

---

# References

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