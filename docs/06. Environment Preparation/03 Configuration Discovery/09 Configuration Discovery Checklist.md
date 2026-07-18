# Configuration Discovery Checklist

**Version:** 1.0

**Status:** Pending

**Phase:** 3.3 — Configuration Discovery

---

# Purpose

This checklist verifies that all customer-specific configuration required for the Kommo ↔ Aloware integration has been collected, documented, and validated.

All items should be completed before proceeding to the implementation phase.

---

# 1. Kommo Configuration Inventory

## Account

- [ ] Account information documented
- [ ] API version verified
- [ ] Time zone documented
- [ ] Domain documented

---

## Pipelines

- [ ] All pipelines inventoried
- [ ] Integration pipeline identified
- [ ] Pipeline IDs documented

---

## Pipeline Stages

- [ ] All stages documented
- [ ] Integration trigger stages identified
- [ ] Stage IDs documented
- [ ] Stage names verified

---

## Users

- [ ] All users inventoried
- [ ] Responsible users identified
- [ ] User IDs documented

---

## Contacts

- [ ] Standard fields documented
- [ ] Required fields identified

---

## Leads

- [ ] Lead configuration documented
- [ ] Lead ownership rules documented

---

## Custom Fields

- [ ] Existing custom fields inventoried
- [ ] Required custom fields identified
- [ ] Missing fields identified

---

## Tags

- [ ] Existing tags inventoried
- [ ] Integration tags identified

---

## Webhooks

- [ ] Existing webhooks documented
- [ ] Required webhook events verified

---

# 2. Aloware Configuration Inventory

## Account

- [ ] Account information documented
- [ ] API version verified
- [ ] Authentication method verified

---

## Agents

- [ ] All agents inventoried
- [ ] Active agents identified
- [ ] Agent IDs documented

---

## Teams

- [ ] Teams documented
- [ ] Team assignments verified

---

## Phone Numbers

- [ ] Phone numbers inventoried
- [ ] Numbers used by the integration identified

---

## Campaigns

- [ ] Campaigns documented
- [ ] Integration campaigns identified

---

## Power Dialer Lists

- [ ] Lists documented
- [ ] Target lists identified

---

## Contact Configuration

- [ ] Contact fields documented
- [ ] Required fields identified

---

## AI Features

- [ ] Enabled AI features documented
- [ ] AI Summary availability verified

---

## Webhooks

- [ ] Existing webhooks documented
- [ ] Required webhook events verified

---

# 3. Field Mapping

- [ ] Contact field mapping completed
- [ ] Lead field mapping completed
- [ ] Ownership mapping completed
- [ ] Communication mapping completed
- [ ] Custom field mapping completed
- [ ] Data transformations documented
- [ ] Validation rules documented

---

# 4. Stage Mapping

- [ ] Integration stages identified
- [ ] Trigger stages documented
- [ ] Aloware actions defined
- [ ] Business rules documented
- [ ] Validation rules documented

---

# 5. Agent Mapping

- [ ] Kommo users identified
- [ ] Aloware agents identified
- [ ] User-to-agent mappings documented
- [ ] Default assignment configured (if applicable)
- [ ] Assignment rules documented

---

# 6. Custom Fields

- [ ] Existing custom fields inventoried
- [ ] Required custom fields documented
- [ ] Data types verified
- [ ] Synchronization rules documented
- [ ] Missing fields identified

---

# 7. Tags & Labels

- [ ] Existing tags inventoried
- [ ] Required tags documented
- [ ] Tag application rules defined
- [ ] Tag removal rules defined
- [ ] Naming conventions validated

---

# 8. Business Rules

- [ ] Customer-specific business rules documented
- [ ] Assignment rules documented
- [ ] Synchronization rules documented
- [ ] Exception scenarios documented

---

# 9. Documentation Review

- [ ] Configuration Discovery Plan completed
- [ ] Kommo Configuration Inventory completed
- [ ] Aloware Configuration Inventory completed
- [ ] Field Mapping Specification completed
- [ ] Stage Mapping Specification completed
- [ ] Agent Mapping Specification completed
- [ ] Custom Fields Specification completed
- [ ] Tags & Labels Specification completed

---

# 10. Readiness Assessment

The Configuration Discovery phase is considered complete when all of the following conditions are satisfied.

- [ ] All configuration inventories completed
- [ ] All mappings documented
- [ ] Customer-specific configuration identified
- [ ] No unknown dependencies remain
- [ ] Customer review completed
- [ ] Integration Engineer review completed

---

# Discovery Summary

| Area | Status |
|------|--------|
| Kommo Configuration | ☐ Passed ☐ Failed |
| Aloware Configuration | ☐ Passed ☐ Failed |
| Field Mapping | ☐ Passed ☐ Failed |
| Stage Mapping | ☐ Passed ☐ Failed |
| Agent Mapping | ☐ Passed ☐ Failed |
| Custom Fields | ☐ Passed ☐ Failed |
| Tags & Labels | ☐ Passed ☐ Failed |
| Business Rules | ☐ Passed ☐ Failed |
| Documentation | ☐ Passed ☐ Failed |

---

# Outstanding Items

| ID | Description | Priority | Owner | Status |
|----|-------------|----------|-------|--------|
| | | High / Medium / Low | | |

---

# Final Approval

| Role | Name | Date |
|------|------|------|
| Integration Engineer | | |
| Customer | | |
| Project Owner | | |

---

# Final Result

| Item | Status |
|------|--------|
| Configuration Discovery Completed | ☐ Yes ☐ No |
| Ready for Implementation | ☐ Yes ☐ No |
| Discovery Completion Date | |