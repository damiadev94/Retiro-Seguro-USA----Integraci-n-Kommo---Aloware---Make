# 03 Make

---

# Purpose

The **Make** domain defines the standard operating procedures for designing, building, testing, and deploying integration scenarios using the Make automation platform.

Its purpose is to establish consistent implementation practices that improve maintainability, scalability, reliability, and operational consistency across all integration projects.

These procedures are platform-independent with respect to the systems being integrated. They focus exclusively on the implementation and operation of workflows within Make.

---

# Scope

This domain applies to every integration project that uses Make as the orchestration platform.

It covers:

- Scenario creation
- Trigger configuration
- Flow routing
- Filter implementation
- Variable management
- Data Store configuration
- Scenario scheduling
- Error route configuration
- Scenario testing
- Deployment to production

This domain does **not** cover:

- Platform-specific APIs
- Business logic for individual integrations
- HTTP communication standards
- Infrastructure configuration
- Operational monitoring

These topics are documented in their respective domains.

---

# Objectives

The objectives of this domain are to:

- Standardize Make scenario implementation.
- Promote reusable implementation patterns.
- Improve workflow readability.
- Reduce implementation inconsistencies.
- Simplify maintenance activities.
- Support scalable integration architectures.
- Improve operational reliability.
- Facilitate onboarding of implementation teams.

---

# Documents

| ID | Document | Purpose |
|----|----------|---------|
| SOP-MAKE-001 | Create Scenario | Standard procedure for creating a new Make scenario. |
| SOP-MAKE-002 | Configure Trigger | Configure workflow triggers. |
| SOP-MAKE-003 | Configure Router | Create branching logic using routers. |
| SOP-MAKE-004 | Configure Filters | Control execution paths using filters. |
| SOP-MAKE-005 | Configure Data Store | Configure persistent storage within Make. |
| SOP-MAKE-006 | Configure Variables | Standardize variable usage inside scenarios. |
| SOP-MAKE-007 | Configure Scheduling | Configure scheduled scenario execution. |
| SOP-MAKE-008 | Configure Error Routes | Implement platform-specific error handling. |
| SOP-MAKE-009 | Test Scenario | Validate workflow behavior before deployment. |
| SOP-MAKE-010 | Deploy Scenario | Deploy validated scenarios to production. |

---

# Dependencies

This domain builds upon the standards defined in previous domains.

Required dependencies include:

- 00 Standards
- 01 Infrastructure
- 02 HTTP

Platform-specific implementation domains depend on this documentation, including:

- 04 Kommo
- 05 Aloware

---

# Intended Audience

This documentation is intended for:

- Solution Architects
- Integration Architects
- Technical Leads
- Integration Engineers
- Make Developers
- Operations Engineers

---

# Guiding Principles

The procedures in this domain follow these principles:

- Build reusable workflows.
- Keep scenarios modular.
- Minimize duplicated logic.
- Separate orchestration from business rules.
- Favor readability over complexity.
- Design for maintainability.
- Implement deterministic execution paths.
- Configure robust error handling.
- Validate scenarios before deployment.
- Document implementation decisions.

---

# Relationship with Other Domains

The Make domain provides implementation guidance for orchestrating integrations.

It complements:

- **Infrastructure**, which defines reusable operational foundations.
- **HTTP**, which standardizes communication with external APIs.
- **Platform domains**, which describe business-specific integrations such as Kommo and Aloware.

Together, these domains establish a layered documentation framework for designing, implementing, and operating integration projects.

---

# Status

| Property | Value |
|----------|-------|
| Domain | Make |
| Version | 1.0 |
| Status | Approved |
| Owner | Solution Architect |
| Last Updated | YYYY-MM-DD |