---
id: CHANGE-0014
type: change_record
title: 自己ホスティングのKnowledge rootをdevelopment/dogfoodingへ改名する
status: applied
scope:
  project: dialogue
  domain: development
  subject: self-hosting
revision: 1
created_at: "2026-07-18T01:10:00+09:00"
updated_at: "2026-07-18T01:10:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - PROPOSAL-0014
  - STATE-SELF-HOSTING-001
extensions:
  approval_source: direct_user_instruction
change_set_id: CHANGESET-0014
proposal_ref: PROPOSAL-0014
change_class: C4
decision: approved
approvals:
  - approval_id: APPROVAL-0014
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 2
    decided_at: "2026-07-18T01:10:00+09:00"
    conditions:
      - .dialogue.ymlのsource.pathをdevelopment/dogfoodingに合わせる
      - 歴史的Proposal/Change Recordの旧path development/knowledgeは記録として保持する
    evidence: >-
      development/knowledgeディレクトリをdevelopment/dogfoodingにし、.dialogue.ymlで
      source.pathを development/dogfoodingにしたい #11にそのまま積んで良いです。
targets:
  - id: STATE-SELF-HOSTING-001
    action: update
    before_revision: 2
    after_revision: 3
    result: applied
    error: null
reason: >-
  自己ホスティング構成であることを名前で明示するため、Knowledge rootのpathを
  development/dogfoodingへ改名し、.dialogue.ymlのsource.pathと検証スキャンパスを追随させる。
applied_at: "2026-07-18T01:10:00+09:00"
applied_by: agent:claude
---

# Knowledge rootをdevelopment/dogfoodingへ改名する

## Applied changes

### リネーム
- ディレクトリ `development/knowledge/` → `development/dogfooding/`（docs / proposals / changes / governance / AGENTS.md ごと移動）

### 追随更新（機能・現行）
- ルート `.dialogue.yml` の `source.path`: `development/knowledge` → `development/dogfooding`
- `development/scripts/validate_repository.py` の文書スキャンパスを `development/dogfooding` へ
- `AGENTS.md`（Read first のパスと co-located root 記述）
- `development/README.md`（レイアウトと self-hosting 記述の相対 `knowledge/` → `dogfooding/`）
- pytest `test_knowledge_source.py` の `document_root == development/dogfooding` assertion
- active State `STATE-SELF-HOSTING-001`（rev2→3、Knowledge root path を更新）

### 据え置き（意図的）
- ドメイン語彙 knowledge（Knowledge Repository / knowledge root / knowledge-management-protocol / knowledge.schema.json）
- 歴史的 Proposal / Change Record（CHANGE-0009 / PROPOSAL-0007,0008,0009 / CHANGE-0013）と archived doc の旧path `development/knowledge`（過去の決定記録として保持）

## Rationale

このディレクトリはDialogue自身の意思決定をDialogueのプロトコルで管理するDogfoodingの実体である。`dogfooding` という名前で自己ホスティング構成を明示し、汎用概念 knowledge と区別する。変わるのはroot位置のみで、プロトコルとドメイン語彙は不変。

## Impact

- `.dialogue.yml` は `development/dogfooding` を指し、`validate_repository.py` は同ディレクトリを検証スキャンする。
- 破壊的だが外部利用者ゼロ（自己ホスティングのみ）のため両対応は不要。
- 歴史的記録は旧path `development/knowledge` を保持し、現行の正本 `STATE-SELF-HOSTING-001` のみ新pathへ更新した。
