---
id: CHANGE-0008
type: change_record
title: Dialogue開発にSelf-hostingを採用する
status: applied
scope:
  project: dialogue
  domain: development
  subject: self-hosting
revision: 1
created_at: "2026-07-16T04:29:45+09:00"
updated_at: "2026-07-16T04:29:45+09:00"
created_by: agent:codex
updated_by: agent:codex
related:
  - PROPOSAL-0008
  - PROJECT-CHARTER-001
  - STATE-SELF-HOSTING-001
extensions:
  adapter: bootstrap-filesystem
  approval_source: direct_user_instruction
  self_hosted_change: true
  remote_binding_status: pending
change_set_id: CHANGESET-0008
proposal_ref: PROPOSAL-0008
change_class: C3
decision: approved
approvals:
  - approval_id: APPROVAL-0008
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 1
    decided_at: "2026-07-16T04:29:45+09:00"
    conditions: []
targets:
  - id: PROPOSAL-0008
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: PROJECT-CHARTER-001
    action: update
    before_revision: 3
    after_revision: 4
    result: applied
    error: null
  - id: STATE-SELF-HOSTING-001
    action: create
    before_revision: 0
    after_revision: 1
    result: applied
    error: null
reason: Dialogue自身をDialogueで開発し、Decision Captureの精度、運用負荷、競合処理を実利用から改善する
applied_at: "2026-07-16T04:29:45+09:00"
applied_by: agent:codex
---

# Dialogue開発にSelf-hostingを採用する

## Applied changes

- Skill metadataで暗黙呼び出しを有効化した。
- 会話から確定済みDecisionを抽出する手順をSkillへ追加した。
- Dialogueの`AGENTS.md`へLocal Skill activationとbootstrap規則を追加した。
- Project CharterへSelf-hosting原則を追加した。
- Self-hostingの現在状態とremote未接続を記録した。

## First dogfooding observation

「その方針で進めましょう」は、Skill名を含まないが、直前の特定可能なSelf-hosting提案への明確な承認として解決できた。このChange Recordが最初の会話Decision Capture結果である。
