S00 Infrastructure — SOP mapping

This file documents the automatic mappings applied to the S00 runbook (04-runbook.md). Mappings link scenario runbook task codes to SOP Library files (relative paths from the runbook).

Mapping applied:

- PRE-001 Verify Organization -> SOP-MAKE-001 — Create Scenario (..\..\..\SOP Library\03 Make\SOP-MAKE-001 Create Scenario.md)
- PRE-002 Verify Team -> SOP-MAKE-001 — Create Scenario (..\..\..\SOP Library\03 Make\SOP-MAKE-001 Create Scenario.md)
- PRE-003 Verify Workspace -> SOP-MAKE-001 — Create Scenario (..\..\..\SOP Library\03 Make\SOP-MAKE-001 Create Scenario.md)
- PRE-004 Verify Permissions -> SOP-HTTP-002 — Configure Authentication (..\..\..\SOP Library\02 HTTP\SOP-HTTP-002 Configure Authentication.md)

- CFG-001 Workspace Organization -> SOP-INF-007 — Folder Structure (..\..\..\SOP Library\01 Infrastructure\SOP-INF-007 Folder Structure.md)
- CFG-002 Naming Convention -> SOP-INF-008 — Naming Convention (..\..\..\SOP Library\01 Infrastructure\SOP-INF-008 Naming Convention.md)
- CFG-003 Create Scenario -> SOP-MAKE-001 — Create Scenario (..\..\..\SOP Library\03 Make\SOP-MAKE-001 Create Scenario.md)

- CFG-101 Kommo Connection -> SOP-KOM-001 — OAuth Authentication (..\..\..\SOP Library\04 Kommo\SOP-KOM-001 OAuth Authentication.md)
- CFG-102 OAuth -> SOP-KOM-001 — OAuth Authentication (..\..\..\SOP Library\04 Kommo\SOP-KOM-001 OAuth Authentication.md)
- CFG-103 Connection Test -> SOP-INF-001 — Create Make Connection (..\..\..\SOP Library\01 Infrastructure\SOP-INF-001 Create Make Connection.md)
- CFG-106 Aloware Connection -> SOP-ALO-001 — API Authentication (..\..\..\SOP Library\05 Aloware\SOP-ALO-001 API Authentication.md)

- CFG-201 Register Kommo Webhook -> SOP-KOM-008 — Webhooks (..\..\..\SOP Library\04 Kommo\SOP-KOM-008 Webhooks.md)
- CFG-205 Register Aloware Webhook -> SOP-ALO-006 — Webhooks (..\..\..\SOP Library\05 Aloware\SOP-ALO-006 Webhooks.md)

- CFG-301 Variables -> SOP-MAKE-006 — Configure Variables (..\..\..\SOP Library\03 Make\SOP-MAKE-006 Configure Variables.md)
- CFG-304 Shared IDs -> SOP-INF-002 — Configure Shared Variables (..\..\..\SOP Library\01 Infrastructure\SOP-INF-002 Configure Shared Variables.md)
- CFG-309 Constants -> SOP-INF-009 — Environment Variables (..\..\..\SOP Library\01 Infrastructure\SOP-INF-009 Environment Variables.md)

- CFG-401 Logging -> SOP-INF-006 — Configure Logging (..\..\..\SOP Library\01 Infrastructure\SOP-INF-006 Configure Logging.md)
- CFG-404 Error Handling -> SOP-INF-004 — Configure Error Handler (..\..\..\SOP Library\01 Infrastructure\SOP-INF-004 Configure Error Handler.md)
- CFG-409 Retry Strategy -> SOP-INF-005 — Configure Retry Policy (..\..\..\SOP Library\01 Infrastructure\SOP-INF-005 Configure Retry Policy.md)

- VAL-001 Workspace Validation -> SOP-TST-006 — Validation Checklist (..\..\..\SOP Library\06 Testing\SOP-TST-006 Validation Checklist.md)
- VAL-003 Connection Validation -> SOP-INF-001 — Create Make Connection (..\..\..\SOP Library\01 Infrastructure\SOP-INF-001 Create Make Connection.md)
- VAL-005 Webhook Validation -> SOP-TST-003 — Webhook Testing (..\..\..\SOP Library\06 Testing\SOP-TST-003 Webhook Testing.md)
- VAL-010 Operational Validation -> SOP-TST-006 — Validation Checklist (..\..\..\SOP Library\06 Testing\SOP-TST-006 Validation Checklist.md)

- DOC-001 Update Documentation -> SOP Template (..\..\..\SOP Library\00 Standards\SOP Template.md)
- APP-001 Final Review -> SOP-OPS-001 — Deployment (..\..\..\SOP Library\07 Operations\SOP-OPS-001 Deployment.md)
- APP-002 Infrastructure Approval -> SOP Lifecycle (..\..\..\SOP Library\00 Standards\SOP Lifecycle.md)

Notes:
- Mappings were chosen using the task descriptions and the best-matching SOPs found in the SOP Library. Some scenario SOP codes (SOP-0xx) in the runbook were generic placeholders; they are now linked to domain-prefixed SOP IDs in the library.
- If any mapping should be changed (for example to a more specific SOP), update the mapping file and the runbook accordingly.
