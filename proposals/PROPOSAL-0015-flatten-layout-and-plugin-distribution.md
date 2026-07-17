---
id: PROPOSAL-0015
type: proposal
title: レイアウトをフラット化しClaude Codeプラグインとして配布可能にする
status: approved
scope:
  project: dialogue
  domain: product
  subject: product-scope-v1
revision: 1
created_at: "2026-07-18T02:30:00+09:00"
updated_at: "2026-07-18T02:30:00+09:00"
created_by: agent:claude
updated_by: person:project-owner
related:
  - STATE-PRODUCT-SCOPE-001
  - STATE-SELF-HOSTING-001
  - CHANGE-0015
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:flatten-modern-layout-2026-07-18
  approved_subject_revision: 3
  change_record: CHANGE-0015
  reference: github:mattpocock/skills
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
change_class: C4
proposed_by: agent:claude
targets:
  - id: STATE-PRODUCT-SCOPE-001
    action: update
    expected_revision: 3
  - id: STATE-SELF-HOSTING-001
    action: update
    expected_revision: 3
requested_changes:
  - field: repository-layout
    before: product/ と development/ の二分。skills は product/skills 配下
    after: skills/protocol/schemas/templates/dogfooding/scripts/tests を直下。pyproject.toml をルートへ
  - field: distribution
    before: 配布機構なし（ディレクトリ規約のみ）
    after: .claude-plugin(marketplace.json + plugin.json, source ./)によりClaude Codeプラグイン配布。skills.shにも対応
  - field: acceptance-6
    before: ProductとDevelopmentのディレクトリ境界分離
    after: 配布物と内部資産の境界を .claude-plugin manifest が宣言
reason: >-
  配布しやすくモダンな構成にする。product/ は一般的でなく冗長なため解消し、skills を直下に出す。
  mattpocock/skills を参考に .claude-plugin でインストール可能にする。
evidence_refs:
  - conversation:flatten-modern-layout-2026-07-18
  - github:mattpocock/skills
  - STATE-PRODUCT-SCOPE-001
impact: >-
  配布物のディレクトリ配置が変わり、.claude-plugin で /plugin marketplace add tanb/dialogue から
  インストール可能になる。product/development分離は「配布境界をmanifestが宣言」に再定義。
  プロトコル契約・スキーマ・拒否メッセージの意味は不変。
---

# レイアウトをフラット化しプラグイン配布可能にする

## Decision

ユーザーは次を確定した。

- `product/` と `development/` を解消し、`skills/` `protocol/` `schemas/` `templates/` `dogfooding/` `scripts/` `tests/` を直下に置く。`pyproject.toml` はルートへ（Python慣習）。
- `mattpocock/skills` を参考に `.claude-plugin/`（`marketplace.json` + `plugin.json`, `source: "./"`）を追加し、Claude Code プラグインとして配布可能にする。skills.sh の `npx skills add` にも対応。
- `LICENSE`（MIT）を同一 PR で追加する。

## Rationale

`product/` は一般的なリポジトリで使われず冗長。skills を直下に出すのがモダンな潮流に沿う。配布のしやすさの本体は `.claude-plugin` の manifest であり、`source: "./"` で `skills/` が自動発見される（公式仕様で確認済み）。product/development の分離思想は「配布境界を manifest が宣言する」形で保つ。

## Approval evidence

- 「それでもskillsをtopレベルにした方が良いでしょう。なぜならproductというディレクトリが一般的なレポジトリで使用されるディレクトリではなく、しかも冗長です。」
- 「完全フラット（推奨）」「スタックをマージ後に単独PR（推奨）」（範囲とタイミングの確定）
- 「すでに#12までマージされているのでリストラクチャして欲しいです。そのあとでLICENSEの追加をし、１つのPRで提出してください。」
