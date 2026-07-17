---
id: PROPOSAL-0005
type: proposal
title: Product v1をKnowledge Repository discoveryへ集中する
status: approved
scope:
  project: dialogue
  domain: product
  subject: product-scope-v1
revision: 2
created_at: "2026-07-16T04:00:43+09:00"
updated_at: "2026-07-16T04:00:43+09:00"
created_by: agent:codex
updated_by: person:project-owner
related:
  - PROJECT-CHARTER-001
  - STATE-PRODUCT-SCOPE-001
  - STATE-REFERENCE-IMPLEMENTATION-001
  - PROTOCOL-001
  - GOVERNANCE-001
  - CONFORMANCE-001
  - STATE-TRUSTED-APPROVAL-001
  - CHANGE-0005
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:current-user-instruction
  approved_subject_revision: 1
  change_record: CHANGE-0005
  approvals:
    - approval_id: APPROVAL-0005
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 1
      decided_at: "2026-07-16T04:00:43+09:00"
      conditions: []
change_class: C4
proposed_by: agent:codex
targets:
  - id: STATE-PRODUCT-SCOPE-001
    action: create
    expected_revision: 0
  - id: PROJECT-CHARTER-001
    action: update
    expected_revision: 2
  - id: STATE-REFERENCE-IMPLEMENTATION-001
    action: update
    expected_revision: 2
  - id: PROTOCOL-001
    action: update
    expected_revision: 3
  - id: GOVERNANCE-001
    action: update
    expected_revision: 3
  - id: CONFORMANCE-001
    action: update
    expected_revision: 3
  - id: STATE-TRUSTED-APPROVAL-001
    action: update
    expected_revision: 1
requested_changes:
  - field: product-layout
    before: ProductとDevelopment assetsがトップレベルで混在する
    after: 配布物をproduct/、開発資産をdevelopment/へ分離する
  - field: product-discovery
    before: Knowledge Repositoryの場所を暗黙に仮定する
    after: プロジェクトルートの.knowledge.ymlからGit sourceを解決する
  - field: trusted-approval-profile
    before: Core Approvalの事実上の必須要件
    after: Knowledge Repositoryが明示的に採用する任意profile
reason: 最初に検証すべき利用者価値を、共有Knowledge Repositoryの発見・参照・編集へ戻す
evidence_refs:
  - product/README.md
  - product/config/knowledge.schema.json
  - product/templates/.knowledge.yml
  - product/skills/manage-project-knowledge/SKILL.md
  - development/tests/knowledge_source_test.rb
impact: Product境界とMVP導線が明確になり、Actor検証は本筋を妨げない任意拡張になる
---

# Product v1をKnowledge Repository discoveryへ集中する

## Decision

ユーザーは、成果物と開発資産の分離、`.knowledge.yml`によるGit Knowledge Repository指定、Actor検証の優先度低下を明示した。この判断をProduct v1のスコープとして採用する。
