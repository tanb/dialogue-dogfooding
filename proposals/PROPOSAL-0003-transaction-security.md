---
id: PROPOSAL-0003
type: proposal
title: Filesystem transaction securityをGovernanceへ同期する
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
      body: Marker permissionとDelegation適用境界を、実装およびテスト結果へ同期する
reason: 既存Governanceと実装の差を解消し、回復用バックアップの機密性を保証する
evidence_refs:
  - adapters/filesystem/lib/dialogue/repository.rb
  - adapters/filesystem/lib/dialogue/apply_operation.rb
  - tests/filesystem_adapter_test.rb
  - tests/conformance/cases/C-010-delegated-c2-without-human-approval.yml
impact: Transaction markerが0600で保護され、C2とC3/C4のApproval境界がSchemaとAdapterで一致する
---

# Filesystem transaction securityをGovernanceへ同期する

`AUTH-AGENT-CODEX-001`のC2 Delegationに基づいて適用した。Human Approvalは要求されず、`CHANGE-0003`の`approvals`は空配列である。
