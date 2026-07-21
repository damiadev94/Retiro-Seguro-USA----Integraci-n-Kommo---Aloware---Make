```markdown id="p8k7nq"
# SOP-MAKE-010 Deploy Scenario

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-MAKE-010 |
| Domain | Make |
| Title | Deploy Scenario |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

# Purpose

Define the standard procedure for deploying Make scenarios into a production environment.

Deployment is the controlled process of promoting a validated scenario from development or testing into production. A structured deployment process minimizes operational risk, preserves system stability, ensures configuration consistency, and provides traceability throughout the release lifecycle.

This SOP establishes a standardized deployment methodology for all Make scenarios.

---

# Scope

This SOP applies to every production deployment of a Make scenario.

Typical deployment activities include:

- Initial production deployment
- Scenario updates
- Configuration changes
- New integrations
- Scheduled releases
- Hotfix deployments
- Rollback preparation
- Post-deployment validation

This SOP applies only after successful completion of scenario testing.

---

# Prerequisites

Before starting, verify that:

- Scenario testing has been completed successfully.
- All critical defects have been resolved.
- Production connections are available.
- Required credentials have been validated.
- Deployment has been approved.
- Rollback procedures have been documented.

---

# Inputs

| Input | Required |
|---------|----------|
| Approved Scenario | Yes |
| Test Results | Yes |
| Deployment Approval | Yes |
| Production Configuration | Yes |
| Rollback Plan | Yes |
| Release Notes | Recommended |

---

# Procedure

## Step 1 — Review Deployment Readiness

Verify that deployment prerequisites have been satisfied.

Confirm:

- Functional testing completed
- Integration testing completed
- Error handling validated
- Documentation updated
- Configuration approved
- Stakeholder approval obtained

Deployment should only proceed after formal readiness verification.

---

## Step 2 — Verify Production Configuration

Review the production environment.

Confirm:

- Connections are active.
- Authentication credentials are valid.
- Webhooks are configured.
- Environment variables are correct.
- Data Stores are available.
- Required permissions have been granted.

Production configuration should match the approved implementation design.

---

## Step 3 — Verify External Dependencies

Ensure that all dependent systems are operational.

Typical dependencies include:

- APIs
- CRM platforms
- Telephony platforms
- Email services
- Webhook endpoints
- Authentication providers
- Databases

Deployment should not proceed while critical dependencies are unavailable.

---

## Step 4 — Prepare Rollback Strategy

Confirm that rollback procedures are available.

Document:

- Previous scenario version
- Previous configuration
- Rollback owner
- Recovery procedure
- Recovery validation

Rollback procedures should be executable without additional development.

---

## Step 5 — Deploy the Scenario

Deploy the approved scenario to the production environment.

Verify that:

- The correct scenario version is deployed.
- Production connections are selected.
- Scheduling configuration is correct.
- Error Routes remain enabled.
- Logging configuration is active.

No functional changes should be introduced during deployment.

---

## Step 6 — Activate the Scenario

Enable the scenario according to the approved deployment plan.

Verify:

- Scheduling is enabled where applicable.
- Webhooks are active.
- Connections authenticate successfully.
- Trigger conditions are operational.

Scenario activation should occur only after deployment verification.

---

## Step 7 — Perform Smoke Testing

Execute a limited production validation.

Verify:

- Scenario starts correctly.
- Trigger executes.
- Modules complete successfully.
- External systems respond correctly.
- Expected output is produced.
- No unexpected errors occur.

Smoke testing should validate the critical business flow without affecting normal operations.

---

## Step 8 — Monitor Initial Execution

Observe the first production executions.

Review:

- Execution history
- Processing duration
- Error logs
- API responses
- Retry attempts
- Notifications
- Data consistency

Any unexpected behavior should be investigated immediately.

---

## Step 9 — Validate Business Outcomes

Confirm that production results meet business expectations.

Verify:

- Records are synchronized correctly.
- Business rules are enforced.
- Data mappings are correct.
- Duplicate processing does not occur.
- Stakeholders confirm expected behavior.

Business validation should be completed before considering the deployment successful.

---

## Step 10 — Complete Deployment Documentation

Record:

- Deployment date
- Scenario version
- Environment
- Deployed by
- Approval reference
- Validation results
- Known issues
- Rollback status
- Post-deployment observations

Deployment documentation should provide complete operational traceability.

---

# Validation

The procedure is considered successful when:

- The scenario is deployed successfully.
- Production configuration is correct.
- Initial executions complete successfully.
- Business functionality is validated.
- No critical issues remain.
- Deployment documentation is complete.

---

# Expected Result

The Make scenario is successfully deployed to production, operates according to the approved design, integrates correctly with all dependent systems, and is fully documented for ongoing operations and support.

---

# Common Errors

| Error | Cause | Impact |
|------|------|--------|
| Deploying an untested scenario | Incomplete validation | Production failures |
| Incorrect production configuration | Environment mismatch | Integration errors |
| Invalid production credentials | Authentication failure | Scenario cannot execute |
| Missing rollback plan | Poor release preparation | Extended outage during failures |
| Deployment without monitoring | Operational issues go undetected | Increased business risk |

---

# Troubleshooting

| Problem | Resolution |
|----------|------------|
| Scenario fails immediately after deployment | Verify production connections, authentication, and environment configuration. |
| External systems reject requests | Confirm endpoint configuration, credentials, and API availability. |
| Unexpected production behavior | Compare deployed configuration with the approved implementation design. |
| Duplicate or missing records | Review scheduling, trigger configuration, filters, and Data Store state. |
| Critical production issue detected | Execute the documented rollback procedure and investigate before redeployment. |

---

# Rollback

If deployment introduces critical issues:

1. Disable the production scenario.
2. Stop scheduled executions and incoming triggers if necessary.
3. Restore the previously validated scenario version.
4. Reconfigure production settings if required.
5. Validate that normal operation has been restored.
6. Document the rollback and root cause before scheduling a new deployment.

---

# Best Practices

- Deploy only scenarios that have successfully completed all required testing.
- Use the same deployment process for every release.
- Verify production configuration before activation.
- Prepare rollback procedures before deployment begins.
- Perform smoke testing immediately after activation.
- Monitor the first production executions closely.
- Deploy during approved maintenance windows when appropriate.
- Document every deployment and configuration change.
- Obtain formal approval before enabling production execution.
- Conduct a post-deployment review to capture lessons learned and improvement opportunities.

---

# References

- SOP-MAKE-001 — Create Scenario
- SOP-MAKE-007 — Configure Scheduling
- SOP-MAKE-008 — Configure Error Routes
- SOP-MAKE-009 — Test Scenario
- SOP-INF-004 — Configure Error Handler
- SOP-INF-005 — Configure Retry Policy
- SOP-INF-006 — Configure Logging
- SOP-INF-009 — Environment Variables
- SOP-INF-010 — Secrets Management
- SOP Template
- Integration Documentation Framework

---

# Revision History

| Version | Date | Author | Changes |
|----------|------|--------|---------|
| 1.0 | YYYY-MM-DD | Solution Architect | Initial version |
```
