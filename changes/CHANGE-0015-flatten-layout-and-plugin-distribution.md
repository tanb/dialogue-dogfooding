---
id: CHANGE-0015
type: change_record
title: レイアウトをフラット化しClaude Codeプラグインとして配布可能にする
status: applied
scope:
  project: dialogue
  domain: product
  subject: product-scope-v1
revision: 1
created_at: "2026-07-18T02:30:00+09:00"
updated_at: "2026-07-18T02:30:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - PROPOSAL-0015
  - STATE-PRODUCT-SCOPE-001
  - STATE-SELF-HOSTING-001
extensions:
  approval_source: direct_user_instruction
  reference: github:mattpocock/skills
change_set_id: CHANGESET-0015
proposal_ref: PROPOSAL-0015
change_class: C4
decision: approved
approvals:
  - approval_id: APPROVAL-0015
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 3
    decided_at: "2026-07-18T02:30:00+09:00"
    conditions:
      - product/ と development/ を解消し配布物を直下に置く
      - 配布境界は .claude-plugin の manifest が宣言する
      - LICENSE(MIT)を同一PRで追加する
    evidence: >-
      すでに#12までマージされているのでリストラクチャして欲しいです。
      そのあとでLICENSEの追加をし、１つのPRで提出してください。
targets:
  - id: STATE-PRODUCT-SCOPE-001
    action: update
    before_revision: 3
    after_revision: 4
    result: applied
    error: null
  - id: STATE-SELF-HOSTING-001
    action: update
    before_revision: 3
    after_revision: 4
    result: applied
    error: null
reason: >-
  配布しやすくモダンな構成にするため、product/ と development/ を解消して配布物を直下に置き、
  .claude-plugin により Claude Code プラグインとして配布可能にする。
applied_at: "2026-07-18T02:30:00+09:00"
applied_by: agent:claude
---

# レイアウトをフラット化しプラグイン配布可能にする

## Applied changes

### ディレクトリのフラット化（product/ と development/ を解消）
- `product/skills/dialogue-knowledge/` → `skills/dialogue-knowledge/`
- `product/protocol/*.md` → `protocol/`
- `product/config/knowledge.schema.json` + `product/protocol/schemas/*.json` → `schemas/`（統合）
- `product/templates/.dialogue.yml` → `templates/.dialogue.yml`
- `development/dogfooding/` → `dogfooding/`
- `development/scripts/` → `scripts/`、`development/tests/` → `tests/`
- `development/{pyproject.toml,uv.lock,.python-version}` → ルート
- 陳腐化した `product/README.md` / `development/README.md` を削除

### 配布機構
- `.claude-plugin/marketplace.json`（name/owner/plugins[{ name:"dialogue", source:"./" }]）
- `.claude-plugin/plugin.json`（name:"dialogue", version, license:MIT …）
- `source: "./"` により `skills/dialogue-knowledge/SKILL.md` が自動発見される
- `LICENSE`（MIT）を追加

### 追随更新
- `.dialogue.yml` の `source.path`: `dogfooding`
- `scripts/validate_repository.py`（ROOT階層、schema/protocol/dogfooding/tests/skills の各 glob）
- `scripts/check_conformance.py`（ROOT階層、cases glob）
- `tests/dialogue_support.py`（REPO_ROOT階層、RESOLVER）、`tests/test_skill_activation.py`、`tests/test_knowledge_source.py`
- `.github/workflows/ci.yml`（`working-directory: development` を除去、root から実行）
- `AGENTS.md` / `README.md` / `protocol/protocol-conformance.md` の全パス、`schemas/knowledge.schema.json` の `$id`

### ガバナンス
- `STATE-PRODUCT-SCOPE-001` rev3→4：配布境界の再定義（受入基準 #6）、レイアウトと配布経路を更新

## Rationale

`product/` は非慣用かつ冗長。skills を直下に出しモダンな潮流に沿わせる。配布のしやすさの本体は `.claude-plugin` であり、product/development の分離思想は「配布境界を manifest が宣言」する形で保持する。

## Impact

- `/plugin marketplace add tanb/dialogue` → `/plugin install dialogue@dialogue`、および `npx skills add tanb/dialogue` で配布可能。
- 検証は root から `uv run python scripts/validate_repository.py` / `uv run pytest`。
- プロトコル契約・スキーマ・安全判断の意味は不変。歴史的 Proposal/Change Record の旧パスは記録として保持。
