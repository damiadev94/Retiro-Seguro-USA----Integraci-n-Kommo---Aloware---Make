# SOP-INF-001 Create Make Connection

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-INF-001 |
| Domain | Infrastructure |
| Title | Create Make Connection |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

# Purpose

Define the standard procedure for creating and validating a connection between **Make** and an external platform or service.

A properly configured connection provides authenticated access to third-party systems and serves as the foundation for all subsequent automation scenarios.

This SOP standardizes how connections are established to ensure consistency, security, and maintainability across integration projects.

---

# Scope

This procedure applies whenever a new authenticated connection must be created in Make.

Typical integrations include:

- Kommo
- Aloware
- HubSpot
- Shopify
- Stripe
- Slack
- Google Workspace
- Microsoft 365
- REST APIs
- Custom Applications

This SOP covers the creation and validation of the connection but does not include platform-specific authentication requirements.

---

# Prerequisites

Before starting, verify that:

- The Make workspace is accessible.
- The appropriate permissions have been granted.
- The target platform is available.
- Authentication credentials have been obtained.
- Required API access has been approved.
- Environment variables and secrets have been configured according to organizational standards.

---

# Inputs

The following information may be required depending on the authentication method:

| Input | Required |
|---------|----------|
| Platform Name | Yes |
| Authentication Method | Yes |
| API Base URL | If applicable |
| API Key | If applicable |
| OAuth Client ID | If applicable |
| OAuth Client Secret | If applicable |
| Access Token | If applicable |
| Refresh Token | If applicable |
| Username / Password | If applicable |

---

# Procedure

## Step 1 — Identify the Target Platform

Determine the external platform that will be connected.

Examples:

- Kommo
- Aloware
- Slack
- Shopify
- HubSpot
- Custom REST API

Document the selected platform before creating the connection.

---

## Step 2 — Verify Authentication Requirements

Review the platform documentation and identify the required authentication mechanism.

Common authentication methods include:

- OAuth 2.0
- API Key
- Bearer Token
- Basic Authentication
- Custom Headers

Ensure all required credentials are available before continuing.

---

## Step 3 — Create the Connection

Within Make:

1. Navigate to the **Connections** section.
2. Select the connector corresponding to the target platform.
3. Create a new connection.
4. Enter the required authentication information.
5. Complete the authentication process according to the platform requirements.

If OAuth is used, complete the authorization flow using the appropriate account.

---

## Step 4 — Assign a Descriptive Name

Name the connection using the organization's naming convention.

Recommended format:

```text
<Platform> <Environment>
```

Examples:

```text
Kommo Production

Kommo Sandbox

Aloware Production

Slack Development
```

The connection name should clearly identify both the platform and the environment.

---

## Step 5 — Store Credentials Securely

Verify that sensitive credentials are managed securely.

Credentials should:

- follow the organization's Secrets Management policy;
- never be documented in plain text;
- never be committed to source control;
- only be accessible to authorized personnel.

---

## Step 6 — Test the Connection

Perform a connectivity test.

Verify that:

- authentication succeeds;
- the platform accepts requests;
- no authorization errors occur;
- required permissions are available.

If supported by the connector, execute the built-in connection test.

---

## Step 7 — Document the Connection

Record the following information in the project documentation:

- Platform
- Connection name
- Authentication method
- Environment
- Owner
- Date created
- Related scenarios

Do **not** record passwords, API keys, or other secret values.

---

# Validation

The procedure is successful when:

- The connection status is **Active**.
- Authentication completes successfully.
- API requests can be executed.
- Required permissions are confirmed.
- The connection is available for use within Make scenarios.

---

# Expected Result

A secure, authenticated, and reusable connection has been created in Make and is ready to be used by implementation scenarios.

The connection follows the organization's naming, security, and documentation standards.

---

# Common Errors

| Error | Cause | Impact |
|------|------|--------|
| Authentication failed | Invalid credentials | Connection cannot be established |
| OAuth authorization denied | Insufficient permissions | Authentication fails |
| Invalid API Key | Incorrect credential | Requests rejected |
| Incorrect environment | Wrong endpoint or account | Data may be sent to the wrong system |
| Missing required permissions | Incomplete platform access | Limited functionality |

---

# Troubleshooting

| Problem | Resolution |
|----------|------------|
| Connection cannot be authenticated | Verify credentials, authentication method, and required permissions. |
| OAuth flow fails | Confirm the Client ID, Client Secret, Redirect URI, and account permissions. |
| API requests return authorization errors | Validate tokens, scopes, and user permissions. |
| Wrong environment connected | Create a new connection using the correct environment credentials and update affected scenarios. |

---

# Rollback

If the connection was created incorrectly:

1. Disable any scenarios using the connection.
2. Delete the incorrect connection if it is no longer required.
3. Create a new connection following this SOP.
4. Update all dependent scenarios.
5. Validate connectivity before re-enabling automation.

---

# Best Practices

- Create one connection per environment.
- Use service accounts whenever possible.
- Apply descriptive naming conventions.
- Test the connection before implementation.
- Avoid sharing personal credentials.
- Review connection permissions periodically.
- Remove unused connections.
- Document connection ownership.
- Follow the organization's secrets management policy.

---

# References

- SOP-INF-009 — Environment Variables
- SOP-INF-010 — Secrets Management
- SOP-INF-008 — Naming Convention
- SOP Template
- Platform Authentication Documentation

---

# Revision History

| Version | Date | Author | Changes |
|----------|------|--------|---------|
| 1.0 | YYYY-MM-DD | Solution Architect | Initial version |