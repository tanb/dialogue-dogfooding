---
id: PROPOSAL-0008
type: proposal
title: Dialogue開発にSelf-hostingを採用する
status: approved
scope:
  project: dialogue
  domain: development
  subject: self-hosting
revision: 2
created_at: "2026-07-16T04:29:45+09:00"
updated_at: "2026-07-16T04:29:45+09:00"
created_by: agent:codex
updated_by: person:project-owner
related:
  - PROJECT-CHARTER-001
  - STATE-SELF-HOSTING-001
  - STATE-PRODUCT-SCOPE-001
  - CHANGE-0008
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:current-user-instruction
  approved_subject_revision: 1
  change_record: CHANGE-0008
  approvals:
    - approval_id: APPROVAL-0008
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 1
      decided_at: "2026-07-16T04:29:45+09:00"
      conditions: []
change_class: C3
proposed_by: agent:codex
targets:
  - id: PROJECT-CHARTER-001
    action: update
    expected_revision: 3
  - id: STATE-SELF-HOSTING-001
    action: create
    expected_revision: 0
requested_changes:
  - field: project-charter.design-principles.self-hosting
    before: null
    after: Dialogue自身の開発でmanage-project-knowledgeを利用し、実利用結果をProduct改善へ反映する
  - field: agent-skill.decision-capture
    before: Skill名の明示または一般的な編集依頼を主な発火条件とする
    after: 会話で確定した永続的な意思決定を、Skill名の指定なしに暗黙取得する
  - field: agent-policy.bootstrap
    before: Self-hosting用の暫定運用が未定義
    after: 実在するGit remoteの設定までdevelopment/knowledgeを暫定保存先とする
reason: Dialogue自身をDialogueで開発し、Decision Captureの精度、運用負荷、競合処理を実利用から改善する
evidence_refs:
  - conversation:current-user-instruction
  - product/skills/manage-project-knowledge/SKILL.md
  - AGENTS.md
impact: 以後のDialogue開発では、会話で成立した意思決定が自動的なKnowledge記録候補になる
---

# Dialogue開発にSelf-hostingを採用する

## Decision

ユーザーの「その方針で進めましょう」を、直前に提示したDialogue Self-hosting方針への明示的なHuman Approvalとして記録する。
