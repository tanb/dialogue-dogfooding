---
id: PROPOSAL-0014
type: proposal
title: 自己ホスティングのKnowledge rootをdevelopment/dogfoodingへ改名する
status: approved
scope:
  project: dialogue
  domain: development
  subject: self-hosting
revision: 1
created_at: "2026-07-18T01:10:00+09:00"
updated_at: "2026-07-18T01:10:00+09:00"
created_by: agent:claude
updated_by: person:project-owner
related:
  - STATE-SELF-HOSTING-001
  - CHANGE-0014
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:rename-knowledge-root-2026-07-18
  approved_subject_revision: 2
  change_record: CHANGE-0014
  approvals:
    - approval_id: APPROVAL-0014
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 2
      decided_at: "2026-07-18T01:10:00+09:00"
      conditions:
        - .dialogue.ymlのsource.pathをdevelopment/dogfoodingに合わせる
        - 歴史的Proposal/Change Recordの旧path development/knowledgeは記録として保持する
change_class: C4
proposed_by: agent:claude
targets:
  - id: STATE-SELF-HOSTING-001
    action: update
    expected_revision: 2
requested_changes:
  - field: knowledge-root-path
    before: development/knowledge
    after: development/dogfooding
  - field: dialogue-yml-source-path
    before: development/knowledge
    after: development/dogfooding
reason: >-
  このディレクトリはDialogue自身の自己ホスティング（Dogfooding）用のKnowledge rootである。
  汎用概念のknowledgeと区別し、「この構成はDialogue自身のDogfooding」であることを名前で明示する。
evidence_refs:
  - conversation:rename-knowledge-root-2026-07-18
  - .dialogue.yml
  - STATE-SELF-HOSTING-001
impact: >-
  co-located Knowledge rootのpathがdevelopment/dogfoodingへ変わり、.dialogue.ymlの
  source.pathとvalidate_repository.pyのスキャンパスが追随する。ドメイン語彙knowledgeは
  据え置き、pathの位置のみ変更する。
---

# Knowledge rootをdevelopment/dogfoodingへ改名する

## Decision

ユーザーは自己ホスティングのKnowledge rootディレクトリ `development/knowledge` を `development/dogfooding` に改名し、`.dialogue.yml` の `source.path` を `development/dogfooding` に合わせる方針を確定した。

## Rationale

このディレクトリはDialogue自身の意思決定をDialogueのプロトコルで管理する「Dogfooding」の実体である。名前を `dogfooding` にすることで、汎用概念の knowledge（Knowledge Repository / knowledge root）と、Dialogue自身の自己ホスティング構成を明確に区別できる。ドメイン語彙 knowledge は据え置き、変わるのはこのリポジトリ内でのroot位置だけである。

## Approval evidence

- 「development/knowledgeディレクトリをdevelopment/dogfoodingにし、.dialogue.ymlでsource.pathを development/dogfoodingにしたい #11にそのまま積んで良いです。」
