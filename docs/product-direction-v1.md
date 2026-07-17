---
id: STATE-PRODUCT-DIRECTION-001
type: state
title: Dialogue Product Direction v1
status: active
scope:
  project: dialogue
  domain: product
  subject: product-direction-v1
revision: 1
created_at: "2026-07-17T23:59:31+09:00"
updated_at: "2026-07-17T23:59:31+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - PROJECT-CHARTER-001
  - STATE-PRODUCT-SCOPE-001
  - PROPOSAL-0012
  - CHANGE-0012
canonical_for: dialogue/product/direction-v1
owners:
  - person:project-owner
extensions:
  document_kind: product-direction
  version: 1
  session: office-hours-2026-07-17
---

# Dialogue Product Direction v1

`STATE-PRODUCT-SCOPE-001`がProduct v1の配布物と受入基準を定める正本である。本ドキュメントはその上位にある方向性・ポジショニング・次の一歩・North Starの正本であり、スコープ契約は変更しない。

## Thesis

**意思決定した事実は、一箇所にあるべきである。**

Dialogueが提供するのは知識管理ツールではなく、**決定の単一正本（single source of truth for decisions）**である。コード、チャットログ、Gitコミット履歴のいずれでもなく、「何を、なぜ決めたか」だけが一箇所に住む。人間も複数のAI Agentも、同じ正本を読み、同じ正本へ書く。マルチエージェント×マルチヒューマンで作業しても、決定は単数のまま保たれる。

## Two pillars

1. **Governance（決定の単一正本 + 競合→人間Escalation）**
   複数のActorが同じ知識を更新して食い違ったとき、last-write-winsで正本を静かに分岐させない。停止して人間へEscalationする。この「止まって人間に聞く」がGovernanceの本体であり、共有ストレージそのものではない。

2. **Anti-rot（陳腐化・重複の検知とAgentによる継続整理）**
   Dialogueは重複、矛盾、参照切れ、陳腐化を継続的な保守対象とし、Agentに整理させることを約束する。人間の文書は放置すれば腐る。Agent駆動の継続メンテナンスで「腐らない知識」を保つ。これがキラー差別化＝「これが欲しかった」の決め手である。

## Positioning and differentiation

- **主差別化（対 Agent memory: CLAUDE.md / rules 等）**
  Agent memoryは「1エージェントの私的メモ」でrepo・人ごとにサイロ化し、書き直しも矛盾も検知しない。Dialogueは共有・正本・競合時Escalation。全員のmemoryを一つにし、バラつきを止める。

- **プロモーションの見出し（対 Notion / Confluence 等のwiki）**
  「人間のドキュメント管理ほど杜撰なものはない」。wikiは人間向けUIでAgentが機械的に発見・検証できず、腐敗を検知しない。Dialogueは`.dialogue.yml`によるAgent-native discoveryと、Schema + Conformanceによる機械検証、Agent向けに構築されたGovernance Protocolを持つ。

## Canonical placement is configurable

正本の置き場所は`.dialogue.yml`で選べる。独立RepositoryでもよいしKnowledge rootに同一Repositoryを指定してもよい。ただし同一Repositoryを正本にした場合、branchごとに正本の状態が生じるため、マージの運用負荷が発生する。この負荷は導入者が理解した上で選択する必要がある。Protocolは配置に中立であり、独立Repositoryを強制しない。

## Next step (decided): Collision & rot demo

方向性を伝える最大のボトルネックは「見せられる証拠」の不在である。次の一歩は、動くexample Knowledge Repositoryとドライバによる実演デモとする。

1. 2つのAgentが同じ決定を更新して衝突し、Dialogueが停止して人間へEscalationするシーン。
2. 陳腐化・重複を検知し、Agentが整理するシーン。

既存の`tests/conformance`、Product Skillの`resolve-source`、`.dialogue.yml` templateを再利用する。このデモはNorth Star（下記）とプロモーション双方の前提物になる。

## North star: Turbovec-backed MCP for fast canonical search

将来、Turbovecを連携させたMCPを用意し、正本への高速検索を提供する構想をNorth Starとして記録する。正本アクセスの高速化はドキュメント参照と意思決定の高速化につながり、キラーコンテンツになり得る。

**制約（正本性の保護）:**

- Turbovec検索層は**正本ではなく、Git正本の上に乗る派生的なreadアクセラレータ**として位置づける。これは「RAG・検索インデックスは派生物とし、知識の正本にしない」というDialogueの原則と整合する。
- ベクトル/意味検索は近似でありlossyであるため、**discovery（どこで何を扱うか、関連する決定）の高速化**に用い、権威ある読み取り（我々は何を決めたか）は近似の推測ではなく**正確な正本レコードへハンドオフ**する。
- 本構想は**Product v1スコープ外**であり、`STATE-PRODUCT-SCOPE-001`の「Outside initial scope: RAGまたはVector Database」と矛盾しない。v1では実装せず、上記デモ（次の一歩）を先行させる。

## Relationship to Product Scope v1

- 本ドキュメントは`STATE-PRODUCT-SCOPE-001`のスコープ契約・受入基準を変更しない。
- Turbovec MCPはv1スコープ外のNorth Starであり、正本ではない派生層であるため、scope docのVector Database除外と整合する。
- Two pillarsのうちGovernanceはv1の主導線（Human Escalation、独立Change Record）と一致する。Anti-rotの「Agentによる継続整理」を明示的な製品約束として本ドキュメントで初めて正本化する。

## Open questions

1. Anti-rot（陳腐化・重複検知とAgent整理）をProtocolの正式オペレーションとしてどこまで規定するか（将来のApproach B候補）。
2. 同一Repository正本時のbranch×マージ運用負荷を、どの導線・ドキュメントで導入者へ提示するか。
3. Turbovec MCPのdiscovery→正本ハンドオフ境界の具体設計（v1後）。
