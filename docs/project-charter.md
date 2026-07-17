---
id: PROJECT-CHARTER-001
type: state
title: Dialogue プロジェクト憲章
status: active
scope:
  project: dialogue
  domain: governance
  subject: project-charter
revision: 4
created_at: "2026-07-16T00:00:00+09:00"
updated_at: "2026-07-16T04:29:45+09:00"
created_by: agent:codex
updated_by: agent:codex
related:
  - PROPOSAL-0001
  - STATE-PRODUCT-SCOPE-001
  - PROPOSAL-0005
  - CHANGE-0005
  - STATE-SELF-HOSTING-001
  - PROPOSAL-0008
  - CHANGE-0008
canonical_for: dialogue/governance/project-charter
owners:
  - person:project-owner
extensions:
  document_kind: charter
  created_time_precision: date
---

# Dialogue プロジェクト憲章

## 目的

複数の人間と複数の AI エージェントが同時に活動するプロジェクトにおいて、共有知識の現在状態、変更理由、決定権限、ライフサイクルを一貫して管理できる、ツール非依存の Knowledge Governance と Knowledge Management Protocol を設計する。

さらに、このプロトコルを実際のドキュメント基盤上で正しく実行する Agent Skills を作成し、知識の探索、作成、更新、変更記録、整合性検証、整理、アーカイブ、人間へのエスカレーションを再現可能にする。

## 解決する問題

- 作業ブランチごとに情報が分断され、参加者が同じ最新知識を参照できない。
- 同じ内容が複数文書に重複し、どれが現在の正本か分からない。
- 古い記述が検索結果へ混入し、現在有効な知識として誤用される。
- Git の差分は残っていても、変更理由、却下案、決定者、影響が追跡できない。
- 複数エージェントの同時更新により、意味上の競合が発生する。
- 文書数の増加に伴い、重複、矛盾、参照切れ、知識の陳腐化が蓄積する。
- ドキュメントツールごとに運用が閉じ、エージェントの振る舞いを移植できない。

## 基本仮説

問題の中心はドキュメント保存サービスではなく、知識を扱う主体の振る舞いと変更手続きである。したがって、知識の意味とライフサイクルをプロトコルとして定義し、保存先固有の操作はアダプターまたはスキルへ分離する。

最初のProduct検証では、プロジェクトリポジトリの`.dialogue.yml`からGit Knowledge Repositoryを発見し、Agent Skillが参照・編集する導線へ集中する。Actor Identity、Trusted Approval、RAG、Git以外のBackendはこの導線を確立した後の拡張とする。

```text
Knowledge Governance
        ↓
Knowledge Management Protocol
        ↓
Agent Skills
        ↓
Notion | Obsidian | GitHub | Filesystem | Other
```

## 設計原則

### 1. Human sovereignty

エージェントは根拠から確定できない真実を決定しない。競合、曖昧さ、権限不足がある場合は、安全に停止して人間へ判断材料と選択肢を提示する。

### 2. State and history separation

現在有効な状態を表す文書と、状態が変わった理由を表す変更履歴文書を分離する。Git コミット履歴は補助証拠にはなり得るが、意味上の変更履歴の代替にはしない。

### 3. Explicit source of truth

文書種別ごとに責務と優先順位を定義する。同一の事実を複数箇所で独立管理せず、非正本側は正本を参照する。

### 4. Lifecycle over CRUD

知識を単純な作成、参照、更新、削除ではなく、提案、レビュー、承認、有効化、統合、置換、非アクティブ化、アーカイブのライフサイクルとして扱う。

### 5. Archive is cold knowledge

アーカイブは削除ではない。通常の探索と判断から除外するが、経緯調査や明示的な要求では参照可能にする。

### 6. Continuous curation

重複整理は比較的短い周期で行い、古い内容の非アクティブ化は一〜二か月程度の周期を初期仮説とする。周期は実運用の変更頻度と誤検出率に基づいて調整する。

### 7. Retrieval is subordinate

全文検索、メタデータ検索、RAG、ベクトル検索は探索手段であり、真実を決定する仕組みではない。検索インデックスは常に正本から再生成可能な派生物とする。

### 8. Backend portability

プロトコルの適合性を Notion、Obsidian、GitHub などの製品機能へ依存させない。基盤が必要な能力を持たない場合は、補助メタデータまたはアダプターで差を吸収する。

### 9. Self-hosting

Dialogue自身の開発で`dialogue-knowledge`を使用し、会話から成立した意思決定を同じProtocolで記録する。記録漏れ、誤検出、競合、運用負荷をProduct改善の実利用Evidenceとして扱う。

## 初期成果物

1. Knowledge Governance specification
   - 役割、権限、決定主体、承認、競合時のエスカレーション
2. Knowledge Management Protocol specification
   - 文書種別、メタデータ、状態遷移、正本規則、変更履歴、統合、アーカイブ
3. Core Agent Skill
   - 基盤非依存の探索、判断、編集、検証フロー
4. Backend adapters or specialized skills
   - Filesystem/Git を最初の参照実装候補とし、他基盤への移植性を検証
5. Knowledge Curator workflow
   - 重複、矛盾、参照切れ、陳腐化の検出と整理提案
6. Conformance tests
   - スキルと基盤がプロトコルを守ることを、シナリオベースで検証

## 初期スコープ外

- 独自のドキュメント SaaS の開発
- ベクトルデータベースを正本とする設計
- エージェントによる無条件の自動承認
- Git コミットログのみを使った意思決定履歴の復元
- すべての既存ドキュメント基盤への同時対応

## 最初に検証するシナリオ

1. エージェントが現在有効な設計を特定し、根拠とともに回答できる。
2. 承認済み変更に合わせて状態文書を更新し、独立した変更履歴を残せる。
3. 二つの active な文書が矛盾した場合、勝手に選ばず人間へエスカレーションできる。
4. 重複記述を検出し、正本への統合案と影響範囲を提示できる。
5. 古い文書をアーカイブし、通常検索から除外しつつ経緯調査では参照できる。
6. 同じプロトコルを少なくとも二種類のドキュメント基盤で実行できる。

## 設計上の未決事項

- 文書種別と必須メタデータの最小集合
- 状態遷移と、状態ごとの探索優先度
- 変更履歴を文書単位、事実単位、変更セット単位のどれで記録するか
- 同時更新の競合検出方式と楽観的ロックの必要性
- 人間の承認を表す移植可能な証跡形式
- 重複判定と陳腐化判定の安全な閾値
- Core Skill と基盤固有 Skill の責務境界
- プロトコル適合性を評価するテスト形式

## 初期ロードマップ

1. 用語集と脅威・失敗モデルを作成する。
2. Governance の役割、権限、決定規則を定義する。
3. Protocol の文書モデル、状態機械、操作、整合性制約を定義する。
4. 代表シナリオから conformance tests を作成する。
5. Filesystem/Git 向けの参照スキルを実装する。
6. 実利用で評価し、別のドキュメント基盤へ移植して境界を検証する。
