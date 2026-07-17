---
id: PROPOSAL-0013
type: proposal
title: 設定ファイルを.dialogue.ymlへ、Core Skillをdialogue-knowledgeへ改名する
status: approved
scope:
  project: dialogue
  domain: product
  subject: product-scope-v1
revision: 1
created_at: "2026-07-18T00:47:00+09:00"
updated_at: "2026-07-18T00:47:00+09:00"
created_by: agent:claude
updated_by: person:project-owner
related:
  - STATE-PRODUCT-SCOPE-001
  - STATE-PRODUCT-DIRECTION-001
  - CHANGE-0013
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:rename-dialogue-yml-2026-07-18
  approved_subject_revision: 2
  change_record: CHANGE-0013
  naming_principle: entry-points-branded-domain-vocabulary-descriptive
  approvals:
    - approval_id: APPROVAL-0013
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 2
      decided_at: "2026-07-18T00:47:00+09:00"
      conditions:
        - ドメイン語彙knowledgeは記述として保持し入口のみ改名する
        - 歴史的Proposal/Change Recordの旧名は記録として保持する
        - 素のdialogueはSkillファミリ名として温存しCore Skillはdialogue-knowledgeとする
change_class: C4
proposed_by: agent:claude
targets:
  - id: STATE-PRODUCT-SCOPE-001
    action: update
    expected_revision: 2
requested_changes:
  - field: config-filename
    before: .knowledge.yml
    after: .dialogue.yml
  - field: core-skill-name
    before: manage-project-knowledge
    after: dialogue-knowledge
reason: >-
  製品名Dialogueに入口（設定ファイルとCore Skill）を揃え、利用者の記憶性と指示のしやすさを高める。
  ランタイムファイルは既に.dialogue.lock / .dialogue-transaction.jsonと一貫しており、設定ファイルだけが
  .knowledge.ymlで浮いていた不整合も解消する。
evidence_refs:
  - conversation:rename-dialogue-yml-2026-07-18
  - STATE-PRODUCT-SCOPE-001
impact: >-
  v1配布物の設定ファイル名とCore Skill名が変わる（破壊的変更）。外部利用者はまだ存在せず自己
  ドッグフーディングのみのため両対応は設けずハードリネームする。ドメイン語彙knowledgeと
  スキーマファイルknowledge.schema.jsonは据え置く。
---

# 設定ファイルとCore Skillを製品名に揃える

## Decision

ユーザーは次を確定した。

- 設定ファイル `.knowledge.yml` を `.dialogue.yml` に改名する。
- Core Skill `manage-project-knowledge` を `dialogue-knowledge` に改名する。
- 素の `dialogue` はSkillファミリ名として温存し、将来 `dialogue-git` / `dialogue-conformance` 等を並べる。charterが計画するCore Skillとbackend固有Skillの複数化に備える。

## Naming principle

入口（設定ファイル・Skill名）は製品ブランドに寄せ、ドメイン語彙（Knowledge Repository、knowledge root、knowledge-governance）と `knowledge.schema.json` は記述的なまま保持する。

## Approval evidence

会話中のユーザー確定発言（抜粋）:

- 「.knowledge.ymlを.dialogue.ymlにしたいです。dialogueというプロダクト名に揃えた方がユーザーが使いやすくなります。スキル名も合わせて変更し、さらに短い方が使用しやすいと感じます。」
- 「そもそもこれ自体がdialogueという名前のスキルと考えて良いのであれば、dialogueがよさそうです。dialogueのなかに複数のスキルがある場合は、名前をわけなければなりません。」
- 「それでお願いします。」（Core Skill を `dialogue-knowledge`、`dialogue` はファミリ名温存の方針に対して）
