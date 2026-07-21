# SOP Lifecycle

## Purpose

This document defines the lifecycle of every Standard Operating Procedure (SOP) within the SOP Library.

Its purpose is to establish a consistent process for creating, reviewing, approving, maintaining, deprecating, and archiving SOPs throughout their operational life.

By following a standardized lifecycle, the SOP Library remains accurate, trustworthy, maintainable, and scalable as the integration framework evolves.

---

# Scope

This lifecycle applies to every SOP contained in the SOP Library, regardless of its functional domain.

This includes procedures related to:

- Infrastructure
- HTTP
- Make
- Kommo
- Aloware
- Testing
- Operations

Every SOP must follow this lifecycle from its initial creation until its retirement.

---

# Objectives

The SOP Lifecycle aims to:

- Standardize the creation of new SOPs.
- Ensure technical review before publication.
- Maintain document quality over time.
- Preserve traceability of revisions.
- Prevent obsolete procedures from remaining active.
- Support continuous improvement through controlled updates.

---

# Lifecycle Overview

Every SOP progresses through the following stages:

```text
Draft
   │
   ▼
In Review
   │
   ▼
Approved
   │
   ▼
Active
   │
   ▼
Deprecated
   │
   ▼
Archived
```

Each stage represents the maturity and operational status of the procedure.

---

# Lifecycle Stages

## Draft

### Purpose

The SOP is being created or substantially modified.

### Characteristics

- Initial implementation.
- Content may be incomplete.
- Subject to change.
- Not intended for operational use.

### Allowed Activities

- Writing
- Editing
- Internal collaboration

### Exit Criteria

- Structure completed.
- Technical content documented.
- Ready for review.

---

## In Review

### Purpose

The SOP undergoes technical validation.

### Characteristics

- Procedure reviewed by technical stakeholders.
- Accuracy verified.
- Consistency with standards confirmed.
- Improvements identified.

### Review Criteria

- Technical correctness
- Completeness
- Compliance with SOP Template
- Compliance with Naming Convention
- Operational clarity
- Validation steps defined

### Exit Criteria

- Review comments resolved.
- Reviewer approval obtained.

---

## Approved

### Purpose

The SOP has been formally accepted.

### Characteristics

- Content frozen for publication.
- Ready for operational use.
- Meets all documentation standards.

### Allowed Changes

Only editorial corrections.

Any procedural modification requires a new revision.

---

## Active

### Purpose

The SOP is the official procedure to be followed.

### Characteristics

- Operationally valid.
- Referenced by Runbooks.
- Used during implementation.
- Maintained through version control.

### Maintenance

Active SOPs should be periodically reviewed to ensure they remain aligned with:

- Platform changes
- API updates
- Product releases
- Operational improvements

---

## Deprecated

### Purpose

The procedure is no longer recommended for new implementations.

### Reasons

Examples include:

- Platform feature removed.
- API endpoint replaced.
- New implementation method available.
- Security concerns.
- Architectural redesign.

### Rules

A deprecated SOP:

- remains available for historical reference;
- keeps its identifier;
- is not used in new projects;
- references the replacement SOP when applicable.

Example:

```text
Status

Deprecated

Replacement

SOP-MAKE-012
```

---

## Archived

### Purpose

The SOP is permanently retired.

### Characteristics

- No longer maintained.
- Preserved for historical traceability.
- Stored in the Archive section.
- Identifier permanently reserved.

Archived SOPs must never be deleted.

---

# Status Definitions

| Status | Operational Use | Editable |
|---------|-----------------|----------|
| Draft | No | Yes |
| In Review | No | Limited |
| Approved | Not Yet | Editorial Only |
| Active | Yes | Controlled |
| Deprecated | Historical Only | No |
| Archived | Historical Only | No |

---

# Versioning

Every SOP maintains an independent version history.

The SOP identifier never changes.

Only the version number evolves.

Example:

```text
SOP-INF-003

Version 1.0

↓

Version 1.1

↓

Version 1.2

↓

Version 2.0
```

---

# Version Numbering

The library follows Semantic Versioning principles.

| Version | Meaning |
|----------|---------|
| 1.0 | Initial approved release |
| 1.1 | Minor improvements or clarifications |
| 1.2 | Documentation updates without procedural changes |
| 2.0 | Major procedural redesign |

General rules:

- Major versions represent significant changes to the procedure.
- Minor versions represent improvements or clarifications.
- Editorial corrections may increment the minor version according to project governance.

---

# Change Management

Whenever an SOP changes:

1. Update the document version.
2. Update the Last Updated field.
3. Record the modification in the Revision History.
4. Review affected Runbooks.
5. Review related SOP references.
6. Validate that the procedure remains accurate.

---

# Revision History

Every SOP must maintain its own revision history.

Example:

| Version | Date | Author | Changes |
|----------|------|--------|---------|
| 1.0 | 2026-07-21 | Solution Architect | Initial publication |
| 1.1 | 2026-08-03 | Solution Architect | Updated validation steps |

Revision history must never be removed.

---

# Retirement Process

An SOP should be retired when:

- The underlying technology is no longer supported.
- The documented procedure becomes obsolete.
- A replacement SOP exists.
- The integration architecture changes significantly.

Retirement process:

```text
Active

↓

Deprecated

↓

Archived
```

Direct deletion is not permitted.

---

# Governance Rules

Every SOP must:

- Have a unique identifier.
- Follow the standard template.
- Maintain revision history.
- Have a defined lifecycle status.
- Be reviewed before becoming Active.
- Preserve traceability throughout its lifetime.

No SOP may bypass the review and approval process.

---

# Responsibilities

| Role | Responsibility |
|------|----------------|
| Author | Create and maintain SOP content |
| Reviewer | Validate technical accuracy and compliance |
| Solution Architect | Approve publication and major revisions |
| Implementation Engineer | Execute procedures and provide operational feedback |

---

# Lifecycle Compliance Checklist

Before changing an SOP status, verify that:

- The document follows the standard template.
- The identifier complies with the naming convention.
- Technical accuracy has been validated.
- Validation steps are complete.
- Revision history has been updated.
- Related references have been reviewed.
- The status transition is appropriate.

---

# Related Documents

- README
- SOP Naming Convention
- SOP Template

---

# Status

| Property | Value |
|----------|-------|
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |