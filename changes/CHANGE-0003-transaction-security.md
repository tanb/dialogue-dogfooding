---
id: CHANGE-0003
type: change_record
title: Sync filesystem transaction security into Governance
status: applied
scope:
  project: dialogue
  domain: product
  subject: filesystem-transaction-security
revision: 1
created_at: "2026-07-16T03:27:16+09:00"
updated_at: "2026-07-16T03:27:16+09:00"
created_by: agent:codex
updated_by: agent:codex
related:
  - PROPOSAL-0003
  - STATE-TRANSACTION-SECURITY-001
  - STATE-REFERENCE-IMPLEMENTATION-001
extensions:
  adapter: manual-filesystem
  delegation_ref: AUTH-AGENT-CODEX-001
change_set_id: CHANGESET-0003
proposal_ref: PROPOSAL-0003
change_class: C2
decision: approved
approvals: []
targets:
  - id: PROPOSAL-0003
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: STATE-TRANSACTION-SECURITY-001
    action: create
    before_revision: 0
    after_revision: 1
    result: applied
    error: null
reason: Resolve the gap between the existing Governance and the implementation, and guarantee the confidentiality of recovery backups
applied_at: "2026-07-16T03:27:16+09:00"
applied_by: agent:codex
---

# Sync filesystem transaction security into Governance

## Result

- Restricted the transaction marker to `0600`.
- Amended the Change Record Schema to require Human Approval only for C3/C4.
- Implemented delegation-based C2 Apply in the Adapter.
- Added a C2 Conformance Case and Adapter security tests.
