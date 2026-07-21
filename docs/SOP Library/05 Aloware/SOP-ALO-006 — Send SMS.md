# Metadata

| Property | Value |
|----------|-------|
| SOP ID | SOP-ALO-006 |
| Title | Send SMS |
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

This Standard Operating Procedure (SOP) defines the standardized process for sending SMS messages through the Aloware REST API.

The objective is to ensure that SMS communications are delivered securely, consistently, and reliably while maintaining synchronization with external CRM systems, preventing duplicate message delivery, and preserving communication traceability.

This procedure applies to all outbound SMS operations initiated through system integrations.

---

# Scope

This procedure applies to any integration that sends SMS messages using Aloware.

Typical use cases include:

- Customer follow-up
- Appointment reminders
- Sales communications
- Customer support notifications
- Automated workflow notifications
- CRM-driven messaging
- Marketing campaigns
- Transactional notifications
- Event-driven messaging

This SOP does not cover:

- Contact creation
- Contact updates
- Call operations
- Power Dialer operations
- Webhook processing
- SMS reporting

---

# Prerequisites

Before starting this procedure, verify that:

- API authentication has been completed successfully.
- A valid API Token is available.
- The Aloware account is accessible.
- The integration has permission to send SMS messages.
- The recipient Contact exists.
- The recipient has a valid phone number.
- HTTPS connectivity is available.
- Business rules allow SMS delivery.

It is recommended to execute **SOP-ALO-002 Search Contact** before sending an SMS.

---

# Inputs

| Input | Required | Description |
|---------|----------|-------------|
| API Token | Yes | Authentication credential |
| API Base URL | Yes | Aloware API endpoint |
| Contact ID | Yes | Recipient Contact identifier |
| Phone Number | Yes | Destination phone number |
| SMS Message | Yes | Message content |
| Sender Line | Optional | Outbound messaging line |
| External Identifier | Optional | External system reference |
| Campaign Identifier | Optional | Associated campaign |
| Message Metadata | Optional | Additional business information |

---

# Procedure

## 1. Validate Authentication

Verify that:

- API Token is valid.
- Authentication headers are correctly configured.
- Required permissions are available.

If authentication fails, execute **SOP-ALO-001 API Authentication** before continuing.

---

## 2. Verify Contact Information

Confirm that the recipient Contact exists.

Verify:

- Contact ID is valid.
- Contact is active.
- Contact has a valid mobile phone number.
- Contact is eligible to receive SMS messages.

Execute **SOP-ALO-002 Search Contact** if necessary.

---

## 3. Validate Business Rules

Verify that SMS delivery is permitted.

Typical validation includes:

- Contact has not opted out.
- SMS is allowed by business policy.
- Required communication consent exists.
- Contact status permits messaging.
- Campaign restrictions are satisfied.

Do not continue if business rules prohibit SMS delivery.

---

## 4. Validate Message Content

Review the SMS message before submission.

Verify that:

- Message is not empty.
- Message length complies with platform limitations.
- Character encoding is supported.
- Unsupported characters have been removed.
- Business content has been approved.
- Required placeholders have been resolved.

Reject invalid messages before submission.

---

## 5. Validate Phone Number

Verify that:

- Phone number is present.
- Number is normalized.
- Country code is included when required.
- Format complies with business standards.
- Number matches the Contact information.

Do not modify phone numbers after validation unless normalization rules require it.

---

## 6. Build the SMS Request

Construct the API request.

Verify that:

- Correct REST endpoint is used.
- HTTPS is enabled.
- Authentication headers are included.
- JSON payload is valid.
- Contact identifier is correct.
- Phone number is correct.
- Message content is included.
- Optional parameters are included only when required.

---

## 7. Submit the SMS Request

Send the request to the Aloware REST API.

Monitor:

- HTTP status code
- Authentication status
- Request completion
- API response
- Network connectivity

Avoid duplicate submissions before evaluating the response.

---

## 8. Validate the Response

Verify that:

- HTTP success status is returned.
- Response body is valid.
- SMS request has been accepted.
- Message identifier has been generated.
- No validation errors are reported.

Reject incomplete or malformed responses.

---

## 9. Record Message Information

Record the successful operation.

Recommended information includes:

- Message ID
- Contact ID
- Phone Number
- Sender Line
- Timestamp
- Integration identifier
- Processing status

Do not store unnecessary message content unless required by business policy.

---

## 10. Verify Delivery Status

When supported by the integration workflow:

Verify that:

- Message has been accepted.
- Delivery status is available.
- Message lifecycle can be tracked.
- Delivery failures are reported.

Delivery confirmation may occur asynchronously.

---

## 11. Return the Result

Return the operation outcome to the calling workflow.

Possible outcomes include:

- SMS Sent
- SMS Accepted
- Validation Failed
- Contact Not Found
- Authentication Failed
- SMS Delivery Failed

Include the generated Message ID whenever available.

---

# Validation

The procedure is considered successful when:

- Authentication succeeded.
- Recipient Contact exists.
- Phone number passed validation.
- Message content passed validation.
- API request completed successfully.
- HTTP success response was received.
- Message identifier was generated.

---

# Expected Result

Upon successful completion:

- The SMS request has been accepted by Aloware.
- Message tracking information is available.
- Communication history can be synchronized with external systems.
- Downstream workflows can continue.
- Message lifecycle is traceable.

---

# Common Errors

| Error | Possible Cause | Resolution |
|---------|----------------|------------|
| Unauthorized (401) | Invalid API Token | Verify authentication credentials |
| Forbidden (403) | Missing permissions | Review API permissions |
| Contact Not Found | Invalid Contact ID | Verify Contact identifier |
| Invalid Phone Number | Incorrect number format | Normalize phone number |
| Message Too Long | Platform limitation exceeded | Reduce message length |
| Empty Message | Missing content | Provide valid SMS text |
| Consent Required | Messaging permission missing | Verify business rules |
| Request Timeout | Network issue | Retry according to retry policy |
| Rate Limit Reached | Excessive API requests | Wait before retrying |
| Internal Server Error | Temporary platform issue | Retry after verification |

---

# Troubleshooting

| Issue | Diagnostic Action | Resolution |
|--------|-------------------|------------|
| SMS rejected | Review API response | Correct validation errors |
| Invalid phone number | Verify normalization | Correct recipient information |
| Message not accepted | Review payload | Correct request structure |
| Delivery not confirmed | Verify delivery status | Monitor asynchronous events |
| Duplicate SMS | Review retry logic | Implement idempotency |
| Authentication failure | Verify API Token | Re-authenticate |
| Unexpected response | Inspect payload | Correct request implementation |
| Slow response | Review connectivity | Retry according to retry policy |

---

# Rollback

If the SMS request cannot be completed successfully:

1. Stop downstream processing.
2. Record the failure in operational logs.
3. Discard invalid request payloads.
4. Verify authentication status.
5. Correct validation issues.
6. Retry only if permitted by retry policy.

If duplicate messages are sent:

1. Record the incident.
2. Identify affected recipients.
3. Notify operational stakeholders if required.
4. Update downstream systems if necessary.
5. Implement corrective measures to prevent recurrence.

Previously delivered SMS messages cannot be recalled once accepted by the messaging platform.

---

# Best Practices

- Always verify Contact existence before sending an SMS.
- Validate communication consent before messaging.
- Normalize phone numbers before submission.
- Validate message content before sending.
- Prevent duplicate SMS delivery through idempotent processing.
- Log operational events without exposing sensitive customer information.
- Track Message IDs for reconciliation.
- Respect API rate limits.
- Monitor SMS delivery metrics.
- Test messaging workflows in non-production environments before deployment.
- Maintain synchronization with CRM communication history.
- Follow organizational messaging and compliance policies.

---

# References

- Aloware REST API Documentation
- Aloware SMS API Documentation
- SOP-ALO-001 API Authentication
- SOP-ALO-002 Search Contact
- SOP-HTTP-001 HTTP Request Standards
- SOP-HTTP-002 HTTP Response Validation
- SOP-MAKE-001 HTTP Module Configuration
- Internal Integration Standards

---

# Revision History

| Version | Date | Author | Description |
|----------|------|--------|-------------|
| 1.0 | YYYY-MM-DD | Integration Documentation Framework | Initial version |