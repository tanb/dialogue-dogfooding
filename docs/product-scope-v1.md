---
id: STATE-PRODUCT-SCOPE-001
type: state
title: Dialogue Product Scope v1
status: active
scope:
  project: dialogue
  domain: product
  subject: product-scope-v1
revision: 4
created_at: "2026-07-16T04:00:43+09:00"
updated_at: "2026-07-18T02:30:00+09:00"
created_by: agent:codex
updated_by: agent:claude
related:
  - PROJECT-CHARTER-001
  - STATE-REFERENCE-IMPLEMENTATION-001
  - PROPOSAL-0005
  - CHANGE-0005
  - PROPOSAL-0007
  - CHANGE-0007
  - PROPOSAL-0013
  - CHANGE-0013
  - PROPOSAL-0015
  - CHANGE-0015
canonical_for: dialogue/product/scope-v1
owners:
  - person:project-owner
extensions:
  document_kind: product-scope
  version: 1
---

# Dialogue Product Scope v1

## Product outcome

プロジェクトリポジトリから独立した共有Knowledge Repositoryを、Agentが一貫した方法で発見、参照、編集できるようにする。

```text
Project Repository
  └── .dialogue.yml
          ↓
Dialogue Knowledge Skill
          ↓
Knowledge Git Repository
```

## Consumer-facing deliverables

- `.dialogue.yml` v1 Schema
- Git sourceを記述した導入用`.dialogue.yml` template
- `.dialogue.yml`を読み、Knowledge sourceを解決するAgent Skill
- Knowledge GovernanceとKnowledge Management Protocol

配布境界は`.claude-plugin/`（plugin manifest）が宣言する。配布物は`skills/`（Agent Skill）、`protocol/`（仕様）、`schemas/`（JSON Schema）、`templates/`（導入テンプレート）に置く。Dialogue自身の設計知識・Proposal・Change Record（`dogfooding/`）、テスト（`tests/`）、検証スクリプト（`scripts/`）は内部資産としてこれと分離する。

Dialogueは`.claude-plugin/`によりClaude Codeプラグインとして、また`skills.sh`（`npx skills add`）によりコピー導入として配布できる。

## `.dialogue.yml` v1 contract

```yaml
version: 1
source:
  type: git
  url: git@github.com:example/project-knowledge.git
  ref: main
  path: .
```

- `type`はv1では`git`のみ。
- `url`はKnowledge Git Repositoryのremote。認証情報を含めない。
- `ref`は共有branch、tag、commitで、既定値は`main`。
- `path`はcheckout内のdocument rootで、既定値は`.`。
- 未知フィールド、絶対path、`..`を含むpathは拒否する。

## Required user flow

1. Agentがプロジェクトルートの`.dialogue.yml`を発見する。
2. Skillが設定を検証し、Git URL、ref、document rootを解決する。
3. Agentが専用checkoutを取得または同期する。
4. Repository固有の案内と現在状態を探索する。
5. 質問にはActiveな正本を根拠として回答する。
6. 編集依頼では現在状態と独立したChange Recordを更新する。
7. 同期競合または意味上の曖昧さでは推測せず人間へEscalationする。

## Initial scope

- Git Knowledge Repository discovery
- Git checkoutの取得と同期
- Markdown knowledgeの探索と参照
- 状態文書、Proposal、Change Recordの作成・編集
- Active、Superseded、Archivedの基本的な探索区別
- 重複・競合時のHuman Escalation

## Outside initial scope

- Actor runtime identityの証明
- Trusted Approvalの必須化
- Approval Envelopeの暗号署名
- Notion、Obsidian、Google DriveなどGit以外のBackend
- RAGまたはVector Database
- 独自Document SaaS
- Filesystem Adapterまたは独立した操作CLI

Trusted Approvalの成果は削除せず、明示的に採用するKnowledge Repository向けの任意profileとして維持する。
初期検証で作成したFilesystem AdapterとCLIは`development/experiments/`に保存し、v1では機能開発しない。

## Acceptance criteria

1. 有効な`.dialogue.yml`からGit sourceを決定的に解決できる。
2. 不正または未知の設定を共有Repositoryへの接続前に拒否できる。
3. Skillがcode repository内の文書を暗黙の正本として扱わない。
4. Git Knowledge Repositoryから現在の知識を検索して回答できる。
5. 編集時に意味上のChange Recordを残せる。
6. 配布物（`skills/` `protocol/` `schemas/` `templates/`）と内部資産（`dogfooding/` `scripts/` `tests/`）がディレクトリ境界で分離され、配布境界を`.claude-plugin/`が宣言する。
