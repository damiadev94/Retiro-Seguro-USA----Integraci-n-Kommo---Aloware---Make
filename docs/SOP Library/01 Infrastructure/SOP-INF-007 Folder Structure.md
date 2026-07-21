# SOP-INF-007 Folder Structure

---

## Metadata

| Property | Value |
|----------|-------|
| Identifier | SOP-INF-007 |
| Domain | Infrastructure |
| Title | Folder Structure |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |

---

# Purpose

Define the standard folder structure used across all integration projects to ensure consistency, maintainability, scalability, and efficient collaboration.

A standardized project structure allows engineers to quickly locate documentation, implementation artifacts, configuration files, and operational assets regardless of the specific integration being developed.

---

# Scope

This SOP applies to every new integration project created within the Integration Framework.

It defines the high-level organization of project directories but does not prescribe the internal structure of implementation-specific files.

This procedure should be completed during the initial project setup.

---

# Prerequisites

- Project scope has been approved.
- Repository or project workspace has been created.
- Documentation framework has been selected.
- Naming conventions have been reviewed.

---

# Inputs

The following information is required before creating the project structure:

- Project name
- Repository location
- Documentation location
- Source code location (if applicable)
- Integration platform(s)
- Version control system

---

# Procedure

## Step 1 — Create the Project Root

Create the project root directory using the approved project naming convention.

Example:

```text
kommo-aloware-integration/
```

The project root becomes the single entry point for all documentation, implementation assets, and supporting resources.

---

## Step 2 — Create the Top-Level Directories

Create the standard project directories.

Recommended structure:

```text
Project Root
│
├── docs/
├── implementation/
├── assets/
├── scripts/
├── examples/
├── exports/
└── README.md
```

Each directory should have a clearly defined responsibility.

---

## Step 3 — Organize Documentation

Store all project documentation inside the `docs` directory.

Typical organization:

```text
docs/
│
├── Project State
├── Discovery
├── Functional Analysis
├── Technical Analysis
├── Architecture
├── Environment Preparation
├── Implementation
├── SOP Library
└── Appendix
```

Documentation should remain independent from implementation artifacts.

---

## Step 4 — Organize Implementation Assets

Store implementation-specific resources inside the `implementation` directory.

Examples include:

- Make scenarios
- Deployment artifacts
- Configuration exports
- Templates
- Mapping files
- Operational checklists

Implementation assets should not be mixed with documentation.

---

## Step 5 — Organize Supporting Assets

Create dedicated directories for reusable resources.

Examples:

```text
assets/
```

May contain:

- Images
- Diagrams
- Icons
- Architecture illustrations
- Screenshots

```text
examples/
```

May contain:

- Example payloads
- Sample requests
- Example responses
- Reference configurations

```text
scripts/
```

May contain:

- Helper scripts
- Migration scripts
- Validation scripts
- Utility automation

---

## Step 6 — Separate Generated Content

Create a dedicated directory for generated outputs.

Example:

```text
exports/
```

Examples:

- PDFs
- HTML documentation
- Reports
- Generated diagrams
- Build artifacts

Generated files should never replace source documentation.

---

## Step 7 — Maintain Separation of Concerns

Ensure that each directory has a single responsibility.

For example:

| Directory | Responsibility |
|-----------|----------------|
| docs | Project documentation |
| implementation | Technical implementation |
| assets | Static resources |
| scripts | Automation utilities |
| examples | Reference examples |
| exports | Generated deliverables |

Avoid mixing different artifact types within the same directory.

---

## Step 8 — Validate the Structure

Verify that:

- Every required directory exists.
- Documentation is stored under `docs`.
- Generated artifacts are isolated.
- Assets are organized by purpose.
- Empty placeholder directories include a `.gitkeep` file if required by the version control system.

---

# Validation

The procedure is considered successful when:

- The project follows the standard directory structure.
- Documentation and implementation assets are clearly separated.
- All top-level directories exist.
- Team members can easily locate project resources.
- The repository is ready for implementation activities.

---

# Expected Result

A standardized project structure is available and ready to support the complete integration lifecycle.

The repository provides a predictable organization that can be reused across future integration projects.

---

# Common Errors

| Error | Cause | Impact |
|------|------|--------|
| Documentation mixed with implementation files | No defined directory ownership | Difficult maintenance |
| Generated files committed as source documentation | Missing exports directory | Repository clutter |
| Assets stored in multiple locations | Inconsistent organization | Reduced discoverability |
| Missing top-level directories | Manual project creation | Inconsistent project layouts |

---

# Troubleshooting

| Problem | Resolution |
|----------|------------|
| Documentation scattered across folders | Consolidate all documentation under `docs`. |
| Implementation artifacts mixed with documentation | Move implementation assets to the `implementation` directory. |
| Repository structure differs from the standard | Reorganize directories according to this SOP. |
| Generated outputs committed with source files | Relocate generated artifacts to the `exports` directory. |

---

# Rollback

If the project structure was created incorrectly:

1. Backup the repository.
2. Reorganize directories according to the approved structure.
3. Update broken file references.
4. Verify documentation links.
5. Commit the corrected structure.

---

# References

- SOP-INF-008 — Naming Convention
- README — Infrastructure
- SOP Template
- Integration Documentation Framework

---

# Revision History

| Version | Date | Author | Changes |
|----------|------|--------|---------|
| 1.0 | YYYY-MM-DD | Solution Architect | Initial version |