---
id: PROPOSAL-0004
type: proposal
title: Trusted Approval v0.2を採用する
status: approved
scope:
  project: dialogue
  domain: governance
  subject: trusted-approval
revision: 2
created_at: "2026-07-16T03:38:10+09:00"
updated_at: "2026-07-16T03:38:10+09:00"
created_by: agent:codex
updated_by: person:project-owner
related:
  - AUTHORITY-REGISTRY-001
  - STATE-TRUSTED-APPROVAL-001
  - STATE-REFERENCE-IMPLEMENTATION-001
  - CHANGE-0004
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:current-user-instruction
  change_record: CHANGE-0004
  approved_subject_revision: 1
  approvals:
    - approval_id: APPROVAL-0004
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 1
      decided_at: "2026-07-16T03:38:10+09:00"
      conditions: []
change_class: C4
proposed_by: agent:codex
targets:
  - id: STATE-TRUSTED-APPROVAL-001
    action: create
    expected_revision: 0
  - id: AUTHORITY-REGISTRY-001
    action: update
    expected_revision: 1
requested_changes:
  - field: STATE-TRUSTED-APPROVAL-001
    before: null
    after: Trusted Approval v0.2の規範仕様をActive Stateとして作成する
  - field: AUTHORITY-REGISTRY-001.identity_bindings
    before: null
    after: filesystem:uid:501をperson:project-ownerへlocal_account保証で束縛する
  - field: filesystem-approval-flow
    before: CLI引数のactor_refを信頼する
    after: OS Identity、Proposal Digest、Approval Envelopeを検証する
reason: Human Approvalのなりすまし、承認後改変、別Proposalへの転用、期限切れまたは失効済み承認の利用を防ぐ
evidence_refs:
  - docs/failure-model.md
  - docs/knowledge-governance.md
  - adapters/filesystem/lib/dialogue/workflow.rb
  - adapters/filesystem/lib/dialogue/apply_operation.rb
  - tests/filesystem_cli_test.rb
impact: Approvalの本人性と対象内容の結合が強化され、旧CLI契約は破壊的に変更される
---

# Trusted Approval v0.2を採用する

## Decision

ユーザーは、直前に提示されたTrusted Approval v0.2の作業内容に対して「お願いします」と明示した。この指示をC4変更のHuman Approvalとして記録する。

このApprovalは新仕様の導入前に発生したためv0.1履歴形式である。`STATE-TRUSTED-APPROVAL-001`の発効後に作成されるApprovalはv0.2 Envelopeを必須とする。
