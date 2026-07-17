---
id: CHANGE-0003
type: change_record
title: Filesystem transaction securityをGovernanceへ同期する
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
reason: 既存Governanceと実装の差を解消し、回復用バックアップの機密性を保証する
applied_at: "2026-07-16T03:27:16+09:00"
applied_by: agent:codex
---

# Filesystem transaction securityをGovernanceへ同期する

## Result

- Transaction markerを`0600`へ制限した。
- C3/C4だけにHuman Approvalを要求するようChange Record Schemaを修正した。
- Delegationに基づくC2 ApplyをAdapterへ実装した。
- C2 Conformance CaseとAdapter security testsを追加した。
