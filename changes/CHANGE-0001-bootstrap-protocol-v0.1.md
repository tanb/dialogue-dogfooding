---
id: CHANGE-0001
type: change_record
title: Protocol v0.1をBootstrapする
status: applied
scope:
  project: dialogue
  domain: governance
  subject: protocol-adoption
revision: 1
created_at: "2026-07-16T03:08:48+09:00"
updated_at: "2026-07-16T03:08:48+09:00"
created_by: agent:codex
updated_by: agent:codex
related:
  - PROPOSAL-0001
  - AUTHORITY-REGISTRY-001
  - PROJECT-CHARTER-001
  - GLOSSARY-001
  - FAILURE-MODEL-001
  - GOVERNANCE-001
  - PROTOCOL-001
  - CONFORMANCE-001
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:current-user-instruction
  bootstrap: true
change_set_id: CHANGESET-0001
proposal_ref: PROPOSAL-0001
change_class: C4
decision: approved
approvals:
  - approval_id: APPROVAL-0001
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 2
    decided_at: "2026-07-16T03:08:48+09:00"
    conditions: []
targets:
  - id: PROPOSAL-0001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: PROJECT-CHARTER-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: GLOSSARY-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: FAILURE-MODEL-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: GOVERNANCE-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: PROTOCOL-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: CONFORMANCE-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: AUTHORITY-REGISTRY-001
    action: create
    before_revision: 0
    after_revision: 1
    result: applied
    error: null
reason: ユーザーの直接指示に基づきProtocol v0.1を正式採用し、最初のAuthority Registryを作成する
applied_at: "2026-07-16T03:08:48+09:00"
applied_by: agent:codex
---

# Protocol v0.1をBootstrapする

## Before

Governance、Protocol、Failure Model、Conformanceはdraftであり、Authority Registryと意味上のChange Recordは存在しなかった。

## After

- 中核文書をProtocol準拠のState Documentへ正規化した。
- v0.1対象をActive化した。
- `person:project-owner`をHuman Authorityとして登録した。
- `agent:codex`へC0〜C3の限定操作を委任した。

## Decision authority

`person:project-owner`の直接指示をC4 Approvalとして記録した。Agentは承認を代行していない。
