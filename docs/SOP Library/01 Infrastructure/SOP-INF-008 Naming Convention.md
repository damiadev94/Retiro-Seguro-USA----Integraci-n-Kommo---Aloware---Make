````markdown
# SOP-INF-008 Naming Convention

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-INF-008 |
| Domain | Infrastructure |
| Title | Naming Convention |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

# Purpose

Define the standard naming conventions for technical resources used throughout integration projects.

Consistent naming improves readability, maintainability, troubleshooting, monitoring, collaboration, and long-term scalability by ensuring that every technical artifact can be easily identified and understood without additional context.

This SOP establishes naming standards for integration resources, independent of the implementation platform.

---

# Scope

This SOP applies to all technical resources created during an integration project, including:

- Projects
- Repositories
- Make Scenarios
- Webhooks
- Variables
- Connections
- Data Stores
- API Credentials
- Environment Variables
- Configuration Files
- Documentation Assets

The convention should be followed from project initialization through production maintenance.

---

# Prerequisites

- The project has been approved.
- The project identifier has been defined.
- The standard folder structure has been created.
- Team naming standards have been reviewed.

---

# Inputs

Before applying this convention, the following information should be available:

- Project name
- Integration platforms
- Environment
- Business domain
- Scenario purpose
- Repository name

---

# Procedure

## Step 1 — Use Descriptive Names

Names should clearly describe the purpose of the resource.

Prefer:

```text
Assign Contact to Dialer
```

Avoid:

```text
Scenario 1

Test

Flow

Automation
```

Every resource should be understandable without additional documentation.

---

## Step 2 — Use Consistent Case

Use **Title Case** for user-facing resources whenever supported.

Examples:

```text
Assign Contact to Dialer

Receive Incoming Calls

Sync Call Activity
```

Use **UPPER_SNAKE_CASE** for environment variables.

Example:

```text
KOMMO_CLIENT_ID

KOMMO_CLIENT_SECRET

ALOWARE_API_KEY
```

Use **lowercase-with-hyphens** for folders and repositories.

Example:

```text
kommo-aloware-integration

integration-framework
```

---

## Step 3 — Prefix Environment-Specific Resources

When resources differ by environment, include the environment prefix.

Examples:

```text
DEV - Assign Contact

QA - Assign Contact

PROD - Assign Contact
```

or

```text
DEV_WEBHOOK

PROD_WEBHOOK
```

The environment should be immediately identifiable.

---

## Step 4 — Name Make Scenarios

Use the following structure:

```text
<System> → <System> | <Business Action>
```

Examples:

```text
Kommo → Aloware | Assign Contact

Aloware → Kommo | Sync Call Activity

Kommo → Aloware | Create Lead
```

This format immediately communicates:

- Source
- Destination
- Business purpose

---

## Step 5 — Name Webhooks

Webhook names should describe the triggering event.

Examples:

```text
Lead Created

Lead Updated

Call Finished

SMS Received
```

Avoid generic names such as:

```text
Webhook

Incoming

Receiver
```

---

## Step 6 — Name Variables

Variable names should be concise, descriptive, and consistent.

Examples:

```text
Lead ID

Contact ID

Agent ID

Pipeline ID
```

Environment variables should use uppercase.

Examples:

```text
MAKE_API_TOKEN

KOMMO_CLIENT_ID

KOMMO_CLIENT_SECRET

ALOWARE_API_KEY
```

Avoid abbreviations unless universally recognized.

---

## Step 7 — Name Connections

Connection names should identify both the platform and the environment.

Examples:

```text
Kommo Production

Kommo Sandbox

Aloware Production

Slack Production
```

Avoid:

```text
Connection 1

CRM

Main
```

---

## Step 8 — Name Documentation Files

Documentation files should use descriptive names.

Examples:

```text
Technical Design.md

Project State.md

Environment Readiness Report.md

Implementation Design.md
```

Avoid:

```text
Document.md

Notes.md

Final.md

Version2.md
```

---

## Step 9 — Maintain Consistency

Once a naming convention has been adopted:

- do not rename resources unnecessarily;
- use identical terminology across documentation and implementation;
- avoid multiple names for the same business concept.

For example:

If the project uses **Lead**, do not alternate between:

```text
Lead

Opportunity

Deal
```

unless the platform explicitly distinguishes them.

---

# Validation

The naming convention has been correctly applied when:

- Resource names are descriptive.
- Naming patterns are consistent.
- Environment is identifiable where applicable.
- Business actions are immediately understandable.
- Documentation and implementation use identical terminology.
- No ambiguous or generic names exist.

---

# Expected Result

All technical resources follow a predictable naming convention, enabling engineers to quickly understand the purpose and ownership of each artifact without consulting additional documentation.

---

# Common Errors

| Error | Cause | Impact |
|------|------|--------|
| Generic resource names | Lack of naming standards | Difficult maintenance |
| Mixed naming styles | Inconsistent implementation | Reduced readability |
| Missing environment identifiers | Environment not included | Risk of configuration mistakes |
| Multiple names for the same concept | Terminology inconsistency | Documentation confusion |

---

# Troubleshooting

| Problem | Resolution |
|----------|------------|
| Resource names are inconsistent | Rename resources according to this SOP. |
| Documentation uses different terminology than implementation | Standardize terminology across both. |
| Environment cannot be identified | Add the appropriate environment prefix or suffix. |
| Generic names exist | Replace with descriptive business-oriented names. |

---

# Rollback

If resources were created using incorrect naming:

1. Identify all affected resources.
2. Rename according to this SOP.
3. Update references in documentation.
4. Update references in implementation.
5. Validate that integrations continue to function correctly after renaming.

---

# References

- SOP-INF-007 — Folder Structure
- SOP Naming Convention
- SOP Template
- Integration Documentation Framework

---

# Revision History

| Version | Date | Author | Changes |
|----------|------|--------|---------|
| 1.0 | YYYY-MM-DD | Solution Architect | Initial version |
````
