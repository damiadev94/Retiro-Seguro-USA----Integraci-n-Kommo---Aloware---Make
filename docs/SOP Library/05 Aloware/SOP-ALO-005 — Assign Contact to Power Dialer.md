```markdown id="alo005-power-dialer"
# Metadata

| Property | Value |
|----------|-------|
| SOP ID | SOP-ALO-005 |
| Title | Assign Contact to Power Dialer |
| Domain | 05 Aloware |
| Platform | Aloware |
| API Type | REST API |
| Authentication Method | API Token |
| Version | 1.0 |
| Status | Approved |
| Owner | Integration Documentation Framework |
| Last Updated | YYYY-MM-DD |

---

# Purpose

This Standard Operating Procedure (SOP) defines the standardized process for assigning an existing Contact to an Aloware Power Dialer campaign using the REST API.

The objective is to ensure that Contacts are consistently assigned to outbound dialing campaigns while maintaining accurate ownership, preventing duplicate assignments, and preserving synchronization with external CRM systems.

This procedure supports automated outbound communication workflows and event-driven integrations.

---

# Scope

This procedure applies to any integration that assigns Contacts to a Power Dialer campaign.

Typical use cases include:

- Sales campaign enrollment
- Outbound calling automation
- CRM pipeline synchronization
- Lead qualification workflows
- Agent workload distribution
- Follow-up campaign assignment
- Marketing campaigns
- Customer re-engagement workflows

This SOP does not cover:

- Contact creation
- Contact updates
- Campaign configuration
- Agent management
- Call execution
- SMS delivery
- Webhook processing

---

# Prerequisites

Before starting this procedure, verify that:

- API authentication has been completed successfully.
- A valid API Token is available.
- The Aloware account is accessible.
- The integration has permission to manage Power Dialer assignments.
- The Contact exists.
- The target Power Dialer campaign exists.
- Required identifiers are available.
- HTTPS connectivity is available.

It is recommended to execute **SOP-ALO-002 Search Contact** before assigning a Contact to a campaign.

---

# Inputs

| Input | Required | Description |
|---------|----------|-------------|
| API Token | Yes | Authentication credential |
| API Base URL | Yes | Aloware API endpoint |
| Contact ID | Yes | Existing Contact identifier |
| Power Dialer ID | Yes | Target Power Dialer campaign identifier |
| Assigned Agent | Optional | Agent responsible for the Contact |
| Priority | Optional | Campaign priority |
| External Identifier | Optional | External system reference |
| Assignment Timestamp | Optional | Assignment event timestamp |
| Campaign Metadata | Optional | Additional business information |

---

# Procedure

## 1. Validate Authentication

Verify that:

- API Token is valid.
- Authentication headers are correctly configured.
- Required permissions are available.

If authentication fails, execute **SOP-ALO-001 API Authentication** before continuing.

---

## 2. Verify Contact Existence

Confirm that the Contact exists.

Verify:

- Contact ID is valid.
- Contact is active.
- Contact is eligible for outbound calling.

Execute **SOP-ALO-002 Search Contact** if necessary.

---

## 3. Verify Power Dialer Availability

Confirm that the target Power Dialer campaign exists.

Verify:

- Campaign identifier is valid.
- Campaign is active.
- Campaign accepts new Contacts.
- Campaign configuration matches business requirements.

Do not continue if the campaign is unavailable.

---

## 4. Validate Assignment Rules

Verify that the Contact satisfies all assignment criteria.

Typical validation includes:

- Contact is not already assigned.
- Contact is callable.
- Required phone number exists.
- Contact status allows outbound communication.
- Campaign eligibility requirements are satisfied.
- Business rules permit enrollment.

Reject invalid assignment requests before submission.

---

## 5. Validate Contact Information

Verify that required Contact information is available.

Typical validation includes:

- Contact ID
- Primary phone number
- Assigned Agent (if required)
- External Identifier
- Contact Status

Missing required information should be corrected before continuing.

---

## 6. Build the Assignment Request

Construct the API request.

Verify that:

- Correct REST endpoint is used.
- HTTPS is enabled.
- Authentication headers are included.
- JSON payload is valid.
- Contact identifier is correct.
- Power Dialer identifier is correct.
- Optional parameters are included only when required.

---

## 7. Submit the Assignment

Send the request to the Aloware REST API.

Monitor:

- HTTP status code
- Authentication status
- Request completion
- API response
- Network connectivity

Avoid repeated submissions before evaluating the API response.

---

## 8. Validate the Response

Verify that:

- HTTP success status is returned.
- Response body is valid.
- Contact assignment completed successfully.
- Campaign identifier matches the requested campaign.
- No validation errors are reported.

Reject incomplete or malformed responses.

---

## 9. Verify Assignment

Retrieve Contact or campaign information when appropriate.

Confirm that:

- Contact appears in the target campaign.
- Assigned Agent is correct.
- Campaign status is correct.
- Contact remains active.
- Assignment metadata has been stored correctly.

---

## 10. Record Operational Information

Record the successful assignment.

Recommended information includes:

- Contact ID
- Power Dialer ID
- Assigned Agent
- Assignment timestamp
- Integration identifier
- Processing status
- Request identifier

Sensitive customer information should not be unnecessarily logged.

---

## 11. Return the Result

Return the operation outcome to the calling workflow.

Possible outcomes include:

- Contact Assigned
- Validation Failed
- Contact Not Found
- Campaign Not Found
- Authentication Failed
- Assignment Failed

Include Contact and Power Dialer identifiers whenever available.

---

# Validation

The procedure is considered successful when:

- Authentication succeeded.
- Contact exists.
- Target Power Dialer campaign exists.
- Assignment rules passed validation.
- API request completed successfully.
- HTTP success response was received.
- Contact is successfully enrolled in the Power Dialer campaign.

---

# Expected Result

Upon successful completion:

- The Contact has been assigned to the specified Power Dialer campaign.
- Assignment information has been recorded.
- Campaign enrollment is available for outbound calling.
- External systems remain synchronized.
- Downstream communication workflows can continue.

---

# Common Errors

| Error | Possible Cause | Resolution |
|---------|----------------|------------|
| Unauthorized (401) | Invalid API Token | Verify authentication credentials |
| Forbidden (403) | Missing permissions | Review API permissions |
| Contact Not Found | Invalid Contact ID | Verify Contact identifier |
| Campaign Not Found | Invalid Power Dialer ID | Verify campaign configuration |
| Contact Already Assigned | Existing enrollment | Prevent duplicate assignment |
| Invalid Phone Number | Contact is not callable | Correct Contact information |
| Validation Failed | Assignment rules not satisfied | Correct request |
| Request Timeout | Network issue | Retry according to retry policy |
| Rate Limit Reached | Excessive API requests | Retry after waiting |
| Internal Server Error | Temporary platform issue | Retry after verification |

---

# Troubleshooting

| Issue | Diagnostic Action | Resolution |
|--------|-------------------|------------|
| Assignment rejected | Review API response | Correct validation errors |
| Campaign unavailable | Verify campaign status | Activate or select another campaign |
| Contact not eligible | Review Contact information | Correct eligibility issues |
| Duplicate assignment | Inspect existing enrollments | Prevent repeated requests |
| Agent assignment incorrect | Verify Agent mapping | Correct assignment configuration |
| Authentication failure | Verify API Token | Re-authenticate |
| Unexpected response | Inspect payload | Correct request implementation |
| Slow response | Review network connectivity | Retry according to retry policy |

---

# Rollback

If the assignment procedure cannot be completed successfully:

1. Stop downstream processing.
2. Record the failure in operational logs.
3. Discard invalid assignment payloads.
4. Verify authentication status.
5. Validate Contact and campaign identifiers.
6. Correct validation issues.
7. Retry only if permitted by retry policy.

If an incorrect assignment has already been completed:

1. Record the incident.
2. Remove the Contact from the incorrect Power Dialer campaign according to operational procedures.
3. Assign the Contact to the correct campaign.
4. Verify synchronization with external systems.
5. Record the corrective action.

---

# Best Practices

- Always verify Contact existence before assignment.
- Validate campaign availability before enrollment.
- Prevent duplicate assignments through idempotent processing.
- Verify Contact eligibility before submission.
- Maintain synchronization with the CRM.
- Log assignment events without exposing sensitive customer information.
- Validate API responses before continuing workflow execution.
- Respect API rate limits.
- Monitor assignment success rates.
- Keep campaign configuration documentation up to date.
- Test assignment workflows in a non-production environment before deployment.
- Treat Power Dialer campaigns as operational resources managed by Aloware.

---

# References

- Aloware REST API Documentation
- Aloware Power Dialer Documentation
- SOP-ALO-001 API Authentication
- SOP-ALO-002 Search Contact
- SOP-ALO-003 Create Contact
- SOP-ALO-004 Update Contact
- SOP-HTTP-001 HTTP Request Standards
- SOP-HTTP-002 HTTP Response Validation
- SOP-MAKE-001 HTTP Module Configuration
- Internal Integration Standards

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | YYYY-MM-DD | Integration Documentation Framework | Initial version |
```
