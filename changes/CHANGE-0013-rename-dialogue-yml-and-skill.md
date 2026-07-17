---
id: CHANGE-0013
type: change_record
title: 設定ファイルを.dialogue.ymlへ、Core Skillをdialogue-knowledgeへ改名する
status: applied
scope:
  project: dialogue
  domain: product
  subject: product-scope-v1
revision: 1
created_at: "2026-07-18T00:47:00+09:00"
updated_at: "2026-07-18T00:47:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - PROPOSAL-0013
  - STATE-PRODUCT-SCOPE-001
  - STATE-PRODUCT-DIRECTION-001
extensions:
  approval_source: direct_user_instruction
  naming_principle: entry-points-branded-domain-vocabulary-descriptive
change_set_id: CHANGESET-0013
proposal_ref: PROPOSAL-0013
change_class: C4
decision: approved
approvals:
  - approval_id: APPROVAL-0013
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 2
    decided_at: "2026-07-18T00:47:00+09:00"
    conditions:
      - ドメイン語彙knowledgeは記述として保持し入口のみ改名する
      - 歴史的Proposal/Change Recordの旧名は記録として保持する
    evidence: >-
      それでお願いします。（Core Skillをdialogue-knowledge、dialogueはファミリ名温存の方針に対して）
targets:
  - id: STATE-PRODUCT-SCOPE-001
    action: update
    before_revision: 2
    after_revision: 3
    result: applied
    error: null
reason: >-
  製品名Dialogueに入口を揃え、記憶性と指示のしやすさを高める。ランタイムファイル
  （.dialogue.lock / .dialogue-transaction.json）との命名一貫性も回復する。
applied_at: "2026-07-18T00:47:00+09:00"
applied_by: agent:claude
---

# 設定ファイルとCore Skillを製品名に揃える

## Applied changes

### リネーム
- ルート設定 `.knowledge.yml` → `.dialogue.yml`
- 導入用テンプレート `product/templates/.knowledge.yml` → `product/templates/.dialogue.yml`
- Core Skill ディレクトリ `product/skills/manage-project-knowledge/` → `product/skills/dialogue-knowledge/`（`name: dialogue-knowledge`、`agents/openai.yaml` の `$dialogue-knowledge`、display名を更新）

### 識別子の追随更新（製品配布物・機能コード・active current-state docs）
- `resolve-source` の既定ファイル名と拒否メッセージを `.dialogue.yml` へ
- `README.md` / `product/README.md` / `AGENTS.md` / `development/README.md` / `development/knowledge/AGENTS.md`
- pytest（`test_knowledge_source.py` / `test_knowledge_git_e2e.py` / `test_skill_activation.py` / `dialogue_support.py`）
- active State: `STATE-PRODUCT-SCOPE-001`(rev2→3)、`product-direction-v1`、`project-charter`、`self-hosting`、`mvp-git-e2e-validation`
- `product/config/knowledge.schema.json` の `title` を `.dialogue.yml` へ（ファイル名 `knowledge.schema.json` は据え置き）

### 据え置き（意図的）
- ドメイン語彙 knowledge（Knowledge Repository / knowledge root / knowledge-governance / knowledge-management-protocol）
- スキーマファイル名 `knowledge.schema.json` と `$id`
- 歴史的 Proposal / Change Record / archived `filesystem-reference-implementation.md` の旧名（過去の決定記録として保持）

## Rationale

入口（設定ファイル・Core Skill）を製品ブランドに寄せると、記憶性と「dialogue-knowledge スキルを使って」のような指示のしやすさが上がる。ランタイムファイルは既に `.dialogue` 接頭辞で揃っており、設定ファイルだけが浮いていた不整合を解消する。ドメイン語彙は記述性を優先して保持し、過度なブランド化で文書が曖昧になるのを避ける。

## Impact

- v1配布物の設定ファイル名とCore Skill名が変わる破壊的変更。外部利用者が存在しないため両対応は設けずハードリネーム。
- `.dialogue.yml` は据え置きの `knowledge.schema.json` で検証される（ドメイン語彙の据え置きと整合）。
- charterが計画する将来の複数スキル（Core + backend固有）に向け、`dialogue` をファミリ名として温存した。
