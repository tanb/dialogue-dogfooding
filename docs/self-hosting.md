---
id: STATE-SELF-HOSTING-001
type: state
title: Dialogue Self-hosting Policy
status: active
scope:
  project: dialogue
  domain: development
  subject: self-hosting
revision: 5
created_at: "2026-07-16T04:29:45+09:00"
updated_at: "2026-07-18T05:00:00+09:00"
created_by: agent:codex
updated_by: agent:claude
related:
  - PROJECT-CHARTER-001
  - STATE-PRODUCT-SCOPE-001
  - PROPOSAL-0008
  - CHANGE-0008
  - PROPOSAL-0009
  - CHANGE-0009
  - PROPOSAL-0014
  - CHANGE-0014
  - PROPOSAL-0015
  - CHANGE-0015
  - PROPOSAL-0018
  - CHANGE-0018
canonical_for: dialogue/development/self-hosting
owners:
  - person:project-owner
extensions:
  document_kind: operating-policy
  activation_status: active
  knowledge_source_status: active
  source_topology: separate-repository
  repository_visibility: private
---

# Dialogue Self-hosting Policy

## Decision

Dialogueは、自身の開発に`dialogue-knowledge`を使用する。会話の中で成立した永続的な意思決定を自動的に検出し、現在状態と意味上のChange Recordへ反映する。

ユーザーはSkill名を指定する必要がない。ただし、Agentは議論中の案と確定した決定を区別し、曖昧な場合はActiveな知識を変更せず人間へ確認する。

## Activation rules

1. 作業に関連するActiveな知識を意思決定前に確認する。
2. 会話のtask boundaryで、確定した永続的な決定を抽出する。
3. 明確な承認がある場合だけState、Proposal、Change Recordを更新する。
4. 競合、曖昧さ、同期失敗では更新を停止する。
5. 作業結果で、記録したKnowledge Itemまたは未記録理由を報告する。

## Runtime status

- Local Skill activation rule: active
- Implicit invocation metadata: active
- Semantic Decision Capture: active
- `.dialogue.yml`: active
- Knowledge Git Repository remote: `https://github.com/tanb/dialogue-dogfooding.git`
- Git ref: `main`
- Knowledge root: `.`（リポジトリトップレベル）
- Source topology: separate-repository
- Repository visibility: private

Dialogueのコードリポジトリ`tanb/dialogue`は`.dialogue.yml`で独立したPrivate Knowledge Repository`tanb/dialogue-dogfooding`を指す。専用checkoutの`main`トップレベルをKnowledge rootとして扱う。この構成はDialogueの主用途（プロジェクトから独立した共有Knowledge Repository）そのものをDogfoodingし、コードとKnowledgeのRepository分離も同時に検証する。配布物（Skill／protocol／schemas／templates）にDialogue内部の統治インスタンスを含めないため、Knowledgeを製品リポジトリから分離する。

## Evaluation signals

- 記録すべき決定の未記録件数
- 検討中の案を確定扱いした誤検出件数
- Decision Captureに必要な追加確認回数
- 競合とstale revisionの検出件数
- Knowledge更新が作業時間へ与える影響
