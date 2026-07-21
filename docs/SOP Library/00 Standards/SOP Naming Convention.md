# SOP Naming Convention

## Purpose

This document defines the naming, identification, and numbering conventions used throughout the SOP Library.

Its objective is to ensure that every Standard Operating Procedure (SOP) has a unique, predictable, and easily identifiable name, improving navigation, traceability, cross-referencing, and long-term maintainability.

These conventions apply to all current and future SOPs, regardless of their technical domain.

---

# Scope

This standard governs:

- SOP identifiers
- File names
- Document titles
- Folder organization
- Numbering sequences
- Cross-references between documents
- Future SOP additions

---

# Naming Principles

The naming convention follows these principles:

- Every SOP must have a unique identifier.
- Identifiers are immutable once assigned.
- File names must remain human-readable.
- Prefixes represent functional domains.
- Numbering is sequential within each domain.
- The identifier is the primary reference used throughout the documentation.

---

# SOP Identifier Structure

Every SOP identifier follows the format:

```text
SOP-<DOMAIN>-<NUMBER>
```

Example:

```text
SOP-INF-001
SOP-INF-002
SOP-MAKE-004
SOP-KOM-003
SOP-HTTP-006
```

---

# Identifier Components

| Component | Description | Example |
|----------|-------------|---------|
| SOP | Standard Operating Procedure | SOP |
| DOMAIN | Functional domain | INF |
| NUMBER | Sequential identifier | 001 |

Example:

```text
SOP-INF-003
│   │     │
│   │     └── Sequential Number
│   └──────── Domain
└──────────── Document Type
```

---

# Domain Prefixes

Each functional area owns its own independent numbering sequence.

| Prefix | Domain |
|---------|--------|
| INF | Infrastructure |
| HTTP | HTTP & REST APIs |
| MAKE | Make Platform |
| KOM | Kommo CRM |
| ALO | Aloware |
| TST | Testing |
| OPS | Operations |

Future domains should introduce a new prefix without modifying existing identifiers.

---

# Numbering Rules

## Independent Sequences

Each domain starts at:

```text
001
```

Example:

```text
SOP-INF-001

SOP-INF-002

...

SOP-INF-010
```

and independently:

```text
SOP-MAKE-001

SOP-MAKE-002
```

Numbers are **never shared across domains**.

---

## Sequential Assignment

Identifiers are assigned sequentially.

Example:

```text
SOP-INF-001

SOP-INF-002

SOP-INF-003
```

Identifiers must never be reused.

If an SOP is removed, its identifier remains retired.

---

## Reserved Numbers

Numbers should not be reused, even if a document is archived or deprecated.

Example:

```text
SOP-INF-007 (Archived)

↓

Do NOT create another SOP-INF-007.
```

---

# File Naming Convention

File names combine the SOP identifier with a concise descriptive title.

Format:

```text
SOP-<DOMAIN>-<NUMBER> <Title>.md
```

Examples:

```text
SOP-INF-001 Create Make Connection.md

SOP-MAKE-004 Configure Iterator.md

SOP-KOM-003 Search Lead.md

SOP-OPS-002 Rollback.md
```

---

# Document Title Convention

The first heading inside the document must match the file identifier.

Example:

```markdown
# SOP-INF-001 Create Make Connection
```

The identifier, title, and filename must always be identical.

---

# Folder Organization

Each SOP belongs to exactly one functional domain.

Example:

```text
01 Infrastructure/

SOP-INF-001 Create Make Connection.md

SOP-INF-002 Configure Shared Variables.md
```

An SOP must never exist in multiple folders.

---

# Cross-Reference Convention

When another document references an SOP, always use its identifier.

Preferred:

```text
See SOP-INF-003.
```

Acceptable:

```text
See SOP-INF-003 — Create Webhook.
```

Avoid referencing documents only by title.

Incorrect:

```text
See Create Webhook.
```

---

# Versioning

The SOP identifier never changes.

Only the document version is updated.

Example:

```text
Identifier

SOP-INF-001

↓

Version

1.0

1.1

1.2

2.0
```

---

# Renaming Rules

The descriptive title may be updated when necessary.

Example:

Old:

```text
SOP-INF-003 Configure Incoming Webhook
```

New:

```text
SOP-INF-003 Create Webhook
```

The identifier remains unchanged.

---

# Deprecated SOPs

Deprecated procedures retain:

- Identifier
- Version history
- References

They are moved to the Archive when appropriate but continue to preserve their original identifier.

---

# Examples

## Infrastructure

```text
SOP-INF-001 Create Make Connection

SOP-INF-002 Configure Shared Variables

SOP-INF-003 Create Webhook
```

---

## HTTP

```text
SOP-HTTP-001 Create HTTP Request

SOP-HTTP-002 Configure Authentication

SOP-HTTP-003 Parse JSON Response
```

---

## Make

```text
SOP-MAKE-001 Create Scenario

SOP-MAKE-002 Configure Router

SOP-MAKE-003 Configure Filter
```

---

## Kommo

```text
SOP-KOM-001 OAuth Authentication

SOP-KOM-002 Search Contact
```

---

## Aloware

```text
SOP-ALO-001 API Authentication

SOP-ALO-002 Create Contact
```

---

## Testing

```text
SOP-TST-001 Unit Testing

SOP-TST-002 Integration Testing
```

---

## Operations

```text
SOP-OPS-001 Deployment

SOP-OPS-002 Rollback
```

---

# Best Practices

- Assign identifiers only when the SOP is created.
- Never reuse retired identifiers.
- Keep titles concise and action-oriented.
- Use verbs that clearly describe the procedure.
- Reference SOPs by identifier throughout the documentation.
- Maintain independent numbering sequences for each domain.
- Preserve identifiers across all document revisions.

---

# Compliance

Every SOP included in the SOP Library must comply with this naming convention before being approved.

Non-compliant documents should be corrected before publication.

---

# Related Documents

- README
- SOP Template
- SOP Lifecycle

---

# Status

| Property | Value |
|----------|-------|
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |