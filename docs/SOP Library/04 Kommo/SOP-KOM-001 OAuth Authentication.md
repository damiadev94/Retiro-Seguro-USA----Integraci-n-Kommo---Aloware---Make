# Metadata

| Property | Value |
|----------|-------|
| SOP ID | SOP-KOM-001 |
| Title | OAuth Authentication |
| Domain | 04 Kommo |
| Platform | Kommo CRM |
| API Version | REST API v4 |
| Authentication Method | OAuth 2.0 Authorization Code Grant |
| Version | 1.0 |
| Status | Approved |
| Owner | Integration Documentation Framework |
| Last Updated | YYYY-MM-DD |

---

# Purpose

This Standard Operating Procedure (SOP) defines the standardized process for authenticating against the Kommo REST API using OAuth 2.0.

The objective is to establish a secure, reusable, and maintainable authentication process that allows integration platforms to access Kommo resources while following security best practices and the principle of least privilege.

This SOP applies to initial authorization, access token acquisition, access token renewal, authentication validation, and operational troubleshooting.

---

# Scope

This procedure applies to any integration that accesses the Kommo REST API.

Typical scenarios include:

- New integrations
- API-based automations
- Make scenarios
- Middleware platforms
- Internal integration services
- Periodic synchronization jobs
- Event-driven integrations

This SOP does not cover:

- API operations
- HTTP request construction
- Business logic implementation
- Webhook configuration
- User permission administration

---

# Prerequisites

Before starting this procedure, verify that:

- A Kommo account is available.
- A Kommo integration has been registered.
- Client ID is available.
- Client Secret is available.
- Redirect URI has been configured.
- Required API scopes have been identified.
- HTTPS connectivity is available.
- OAuth callback endpoint is operational.
- Secure credential storage has been prepared.
- The integration platform supports OAuth 2.0.

---

# Inputs

The following information is required.

| Input | Required | Description |
|---------|----------|-------------|
| Kommo Account Domain | Yes | Account subdomain used for authentication |
| Client ID | Yes | OAuth application identifier |
| Client Secret | Yes | OAuth application secret |
| Redirect URI | Yes | OAuth callback URL |
| Authorization Code | Yes | Temporary authorization code returned by Kommo |
| Access Token | Generated | OAuth access token |
| Refresh Token | Generated | OAuth refresh token |
| Requested Scopes | Yes | Permissions required by the integration |

---

# Procedure

## 1. Verify Integration Registration

Confirm that the integration has been created in the Kommo developer portal.

Verify:

- Client ID exists.
- Client Secret exists.
- Redirect URI matches the implementation.
- Required scopes have been granted.
- Integration status is active.

---

## 2. Validate Redirect URI

Confirm that the configured Redirect URI exactly matches the URI used during authorization.

Verify:

- HTTPS is used.
- No trailing slash differences exist.
- Domain matches.
- Path matches.
- Port matches if applicable.

Any mismatch will cause authorization failure.

---

## 3. Generate Authorization Request

Build the OAuth Authorization URL using the required parameters.

The request shall include:

- Client ID
- Redirect URI
- Response Type
- State parameter
- Requested scopes

The State parameter should contain a cryptographically secure random value to protect against CSRF attacks.

---

## 4. Authorize the Integration

Open the authorization URL in a browser.

The authorized Kommo user shall:

- Authenticate if required.
- Review requested permissions.
- Approve the integration.

Upon successful authorization, Kommo redirects the browser to the configured Redirect URI.

---

## 5. Capture the Authorization Code

Extract the Authorization Code from the callback request.

Verify that:

- The code exists.
- The State parameter matches the original request.
- The authorization was not cancelled.

Authorization Codes are short-lived and should be exchanged immediately.

---

## 6. Exchange Authorization Code for Tokens

Send a secure HTTPS POST request to the OAuth token endpoint.

The request shall include:

- Client ID
- Client Secret
- Authorization Code
- Redirect URI
- Grant Type

Upon success, Kommo returns:

- Access Token
- Refresh Token
- Token Type
- Expiration Information

---

## 7. Securely Store Tokens

Immediately store the generated tokens using a secure credential storage mechanism.

Do not store tokens:

- Inside Make scenarios
- Inside source code
- Inside configuration files
- Inside logs
- Inside documentation

Only authorized systems should have access to stored credentials.

---

## 8. Validate Authentication

Perform a simple authenticated API request.

Recommended validation:

- Retrieve account information.
- Retrieve current user.
- Retrieve a small list of contacts.

Verify that:

- Authentication succeeds.
- HTTP 200 is returned.
- Returned data is correct.

---

## 9. Monitor Token Lifetime

Track Access Token expiration.

The integration should never wait until requests begin failing before refreshing credentials.

Implement proactive monitoring of token validity.

---

## 10. Refresh the Access Token

Before the Access Token expires, use the Refresh Token to request a new Access Token.

Verify that:

- Refresh Token is valid.
- New Access Token is returned.
- New expiration information is received.
- Stored credentials are updated.

If the Refresh Token has expired or been revoked, the complete authorization process must be repeated.

---

## 11. Record Authentication Status

Record the successful authentication event.

Recommended information:

- Date
- Environment
- Account
- Integration Name
- Authentication Status
- Token Expiration
- Operator (if manual)

Sensitive credential values must never be logged.

---

# Validation

Authentication is considered successful when all of the following conditions are met.

- OAuth authorization completed successfully.
- Authorization Code received.
- Access Token received.
- Refresh Token received.
- Tokens securely stored.
- Authenticated API request succeeds.
- Required permissions are available.
- Token expiration has been recorded.

---

# Expected Result

Upon successful completion:

- The integration is authorized.
- OAuth credentials are securely stored.
- API requests can be authenticated.
- Token lifecycle management is established.
- The integration is ready to perform authenticated API operations.

---

# Common Errors

| Error | Possible Cause | Resolution |
|---------|----------------|------------|
| Invalid Client ID | Incorrect integration configuration | Verify Client ID |
| Invalid Client Secret | Incorrect secret | Update stored credentials |
| Redirect URI Mismatch | Callback URL differs from registered URI | Use the exact registered Redirect URI |
| Invalid Authorization Code | Authorization code expired or reused | Restart authorization process |
| Invalid Refresh Token | Token revoked or expired | Perform full OAuth authorization again |
| Unauthorized (401) | Expired Access Token | Refresh Access Token |
| Forbidden (403) | Missing permissions | Review granted scopes |
| Invalid State | CSRF validation failed | Restart authentication flow |
| SSL Validation Error | Invalid HTTPS configuration | Correct TLS configuration |
| Token Not Stored | Credential storage failure | Verify secure storage configuration |

---

# Troubleshooting

| Issue | Diagnostic Action | Resolution |
|--------|-------------------|------------|
| OAuth callback not received | Verify Redirect URI configuration | Correct callback URL |
| Authorization page unavailable | Verify account domain and connectivity | Check network access |
| API returns 401 | Inspect token validity | Refresh or regenerate tokens |
| API returns 403 | Verify OAuth scopes | Reauthorize with required permissions |
| Authorization loop | Inspect Redirect URI and State parameter | Correct OAuth configuration |
| Refresh process fails | Validate Refresh Token | Perform full authorization |
| Credentials lost | Verify credential storage | Reauthorize integration |
| Authentication intermittently fails | Check token expiration handling | Refresh tokens proactively |

---

# Rollback

If authentication cannot be completed successfully:

1. Revoke any partially authorized integration if applicable.
2. Remove invalid Access Tokens.
3. Remove invalid Refresh Tokens.
4. Delete incomplete credential records.
5. Verify integration registration.
6. Restart the complete OAuth authorization process.
7. Validate authentication before resuming API operations.

---

# Best Practices

- Always use HTTPS.
- Store credentials in a secure secret manager.
- Never expose Client Secrets.
- Never expose Access Tokens.
- Never expose Refresh Tokens.
- Never log OAuth credentials.
- Use cryptographically secure State parameters.
- Validate every OAuth callback.
- Refresh tokens before expiration.
- Implement least-privilege access.
- Rotate credentials when required by organizational policy.
- Periodically validate OAuth permissions.
- Monitor authentication failures.
- Audit authentication events regularly.

---

# References

- Kommo REST API Documentation
- Kommo OAuth 2.0 Documentation
- OAuth 2.0 Authorization Framework (RFC 6749)
- OAuth 2.0 Threat Model (RFC 6819)
- Internal HTTP SOP Library
- Internal Infrastructure SOP Library
- Internal Make SOP Library

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | YYYY-MM-DD | Integration Documentation Framework | Initial version |