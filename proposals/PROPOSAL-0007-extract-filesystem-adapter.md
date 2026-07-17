---
id: PROPOSAL-0007
type: proposal
title: Filesystem AdapterをProduct v1から分離する
status: approved
scope:
  project: dialogue
  domain: product
  subject: product-scope-v1
revision: 2
created_at: "2026-07-16T04:18:01+09:00"
updated_at: "2026-07-16T04:18:01+09:00"
created_by: agent:codex
updated_by: person:project-owner
related:
  - STATE-PRODUCT-SCOPE-001
  - STATE-REFERENCE-IMPLEMENTATION-001
  - PROPOSAL-0005
  - CHANGE-0007
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:current-user-instruction
  approved_subject_revision: 1
  change_record: CHANGE-0007
  approvals:
    - approval_id: APPROVAL-0007
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 1
      decided_at: "2026-07-16T04:18:01+09:00"
      conditions: []
change_class: C3
proposed_by: agent:codex
targets:
  - id: STATE-PRODUCT-SCOPE-001
    action: update
    expected_revision: 1
  - id: STATE-REFERENCE-IMPLEMENTATION-001
    action: update
    expected_revision: 3
requested_changes:
  - field: product-v1-deliverables
    before: Filesystem Adapterと独立CLIを含む
    after: .knowledge.yml、Git discovery Skill、Protocolだけを含む
  - field: filesystem-reference-implementation.status
    before: active
    after: inactive
  - field: filesystem-reference-implementation.location
    before: product/
    after: development/experiments/filesystem-adapter/
reason: Adapter固有のProtocol Engine開発をMVPから外し、Git Knowledge RepositoryをSkillで参照・編集する利用者価値の検証へ集中する
evidence_refs:
  - development/tests/knowledge_git_e2e_test.rb
  - development/knowledge/docs/mvp-git-e2e-validation.md
  - product/skills/manage-project-knowledge/SKILL.md
impact: Product v1の配布面と保守対象が縮小し、既存Adapterは削除せず再開条件付きの実験資産として残る
---

# Filesystem AdapterをProduct v1から分離する

## Decision

ユーザーは、`adapters/filesystem/lib`をv1スコープでは開発しない方針を承認した。AdapterとCLIをProduct成果物から外し、Inactiveな開発実験として保存する。
