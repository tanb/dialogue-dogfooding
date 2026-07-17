---
id: PROPOSAL-0002
type: proposal
title: Filesystem Reference AdapterとCore Skillを採用する
status: approved
scope:
  project: dialogue
  domain: product
  subject: filesystem-reference-implementation
revision: 3
created_at: "2026-07-16T03:23:25+09:00"
updated_at: "2026-07-16T03:23:25+09:00"
created_by: agent:codex
updated_by: agent:codex
related:
  - STATE-REFERENCE-IMPLEMENTATION-001
  - PROTOCOL-001
  - GOVERNANCE-001
  - CHANGE-0002
extensions:
  approval_source: direct_user_instruction
  approved_subject_revision: 1
  change_record: CHANGE-0002
  approvals:
    - approval_id: APPROVAL-0002
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 1
      decided_at: "2026-07-16T03:23:25+09:00"
      conditions: []
change_class: C3
proposed_by: agent:codex
targets:
  - id: STATE-REFERENCE-IMPLEMENTATION-001
    action: create
    expected_revision: 0
requested_changes:
  - field: STATE-REFERENCE-IMPLEMENTATION-001
    before: null
    after:
      metadata:
        type: state
        title: Filesystem Reference Adapter and Core Skill
        status: active
        scope:
          project: dialogue
          domain: product
          subject: filesystem-reference-implementation
        canonical_for: dialogue/product/filesystem-reference-implementation
        owners:
          - person:project-owner
      body: Filesystem Adapter、CLI、Core Skill、統合テストをv0.1の参照実装として提供する
reason: Protocolの実行可能性をFilesystem上の垂直スライスで実証する
evidence_refs:
  - tests/filesystem_adapter_test.rb
  - tests/filesystem_cli_test.rb
  - skills/manage-project-knowledge/SKILL.md
impact: 人間とAgentが共有知識を安全にResolve、提案、承認、適用できる最小プロダクトが利用可能になる
---

# Filesystem Reference AdapterとCore Skillを採用する

ユーザーの直接指示を、revision 1に対するHuman Approvalとして記録した。Approval記録の追加でrevision 2、適用後のChange Record参照追加でrevision 3となった。
