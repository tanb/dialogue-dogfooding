---
id: PROPOSAL-0001
type: proposal
title: Knowledge Management Protocol v0.1を採用する
status: approved
scope:
  project: dialogue
  domain: governance
  subject: protocol-adoption
revision: 2
created_at: "2026-07-16T03:00:14+09:00"
updated_at: "2026-07-16T03:08:48+09:00"
created_by: agent:codex
updated_by: agent:codex
related:
  - PROJECT-CHARTER-001
  - GLOSSARY-001
  - FAILURE-MODEL-001
  - GOVERNANCE-001
  - PROTOCOL-001
  - CONFORMANCE-001
  - AUTHORITY-REGISTRY-001
  - CHANGE-0001
extensions:
  approval_required: true
  approval_record: CHANGE-0001
  approval_source: direct_user_instruction
change_class: C4
proposed_by: agent:codex
targets:
  - id: PROJECT-CHARTER-001
    action: update
    expected_revision: 1
  - id: GLOSSARY-001
    action: update
    expected_revision: 1
  - id: FAILURE-MODEL-001
    action: update
    expected_revision: 1
  - id: GOVERNANCE-001
    action: update
    expected_revision: 1
  - id: PROTOCOL-001
    action: update
    expected_revision: 1
  - id: CONFORMANCE-001
    action: update
    expected_revision: 1
  - id: AUTHORITY-REGISTRY-001
    action: create
    expected_revision: 0
requested_changes:
  - field: PROJECT-CHARTER-001.metadata
    before: legacy
    after: protocol-v0.1
  - field: GLOSSARY-001.metadata
    before: legacy
    after: protocol-v0.1
  - field: FAILURE-MODEL-001.status
    before: draft
    after: active
  - field: GOVERNANCE-001.status
    before: draft
    after: active
  - field: PROTOCOL-001.status
    before: draft
    after: active
  - field: CONFORMANCE-001.status
    before: draft
    after: active
  - field: AUTHORITY-REGISTRY-001
    before: null
    after: active
reason: 実装可能なGovernance、Protocol、適合条件をプロジェクトの運用基準として確立する
evidence_refs:
  - PROJECT-CHARTER-001
  - tests/conformance/cases
  - conversation:current-user-instruction
impact: 承認後、AgentとAdapterはv0.1の権限、文書モデル、状態遷移、安全停止、適合テストに従う
---

# Knowledge Management Protocol v0.1を採用する

## Decision

Knowledge Governance、Knowledge Management Protocol、Protocol Conformance、Failure Modelのv0.1を、DialogueプロジェクトのActiveな運用基準として採用する。

## Included artifacts

- `docs/failure-model.md`
- `docs/knowledge-governance.md`
- `docs/knowledge-management-protocol.md`
- `docs/protocol-conformance.md`
- `schemas/*.schema.json`
- `tests/conformance/cases/*.yml`
- `scripts/check-conformance.rb`
- `scripts/validate-repository.rb`

## Validation evidence

参照オラクルの必須9ケースが通過し、Schema JSON、ローカル参照、文書ID、Markdownリンクを検証済みである。

## Approval

`person:project-owner`が会話上の直接指示によりrevision 2を承認した。適用結果と承認証跡は`CHANGE-0001`に記録する。
