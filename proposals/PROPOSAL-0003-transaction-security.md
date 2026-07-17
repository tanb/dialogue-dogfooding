---
id: PROPOSAL-0003
type: proposal
title: Synchronize Filesystem transaction security into Governance
status: approved
scope:
  project: dialogue
  domain: product
  subject: filesystem-transaction-security
revision: 2
created_at: "2026-07-16T03:27:16+09:00"
updated_at: "2026-07-16T03:27:16+09:00"
created_by: agent:codex
updated_by: agent:codex
related:
  - STATE-TRANSACTION-SECURITY-001
  - STATE-REFERENCE-IMPLEMENTATION-001
  - CHANGE-0003
extensions:
  delegated_application: true
  delegation_ref: AUTH-AGENT-CODEX-001
  change_record: CHANGE-0003
change_class: C2
proposed_by: agent:codex
targets:
  - id: STATE-TRANSACTION-SECURITY-001
    action: create
    expected_revision: 0
requested_changes:
  - field: STATE-TRANSACTION-SECURITY-001
    before: null
    after:
      metadata:
        type: state
        title: Filesystem Transaction Security
        status: active
        scope:
          project: dialogue
          domain: product
          subject: filesystem-transaction-security
        canonical_for: dialogue/product/filesystem-transaction-security
        owners:
          - person:project-owner
      body: Synchronize the marker permission and the delegated application boundary with the implementation and the test results
reason: Resolve the gap between the existing Governance and the implementation, and guarantee the confidentiality of the recovery backup
evidence_refs:
  - adapters/filesystem/lib/dialogue/repository.rb
  - adapters/filesystem/lib/dialogue/apply_operation.rb
  - tests/filesystem_adapter_test.rb
  - tests/conformance/cases/C-010-delegated-c2-without-human-approval.yml
impact: The transaction marker is protected with 0600, and the C2 and C3/C4 approval boundaries match between the Schema and the Adapter
---

# Synchronize Filesystem transaction security into Governance

Applied based on the C2 delegation of `AUTH-AGENT-CODEX-001`. Human Approval was not required, and the `approvals` of `CHANGE-0003` is an empty array.
