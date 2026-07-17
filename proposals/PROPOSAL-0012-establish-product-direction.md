---
id: PROPOSAL-0012
type: proposal
title: Product Direction v1（決定の単一正本とAnti-rot、次の一歩とNorth Star）を正本化する
status: approved
scope:
  project: dialogue
  domain: product
  subject: product-direction-v1
revision: 1
created_at: "2026-07-17T23:59:31+09:00"
updated_at: "2026-07-17T23:59:31+09:00"
created_by: agent:claude
updated_by: person:project-owner
related:
  - STATE-PRODUCT-DIRECTION-001
  - STATE-PRODUCT-SCOPE-001
  - PROJECT-CHARTER-001
  - CHANGE-0012
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:office-hours-2026-07-17
  approved_subject_revision: 0
  change_record: CHANGE-0012
  session: office-hours-2026-07-17
  approvals:
    - approval_id: APPROVAL-0012
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 0
      decided_at: "2026-07-17T23:59:31+09:00"
      conditions:
        - Turbovec検索層は正本ではなく派生readアクセラレータとして扱う
        - 本方向性はSTATE-PRODUCT-SCOPE-001のスコープ契約を変更しない
change_class: C3
proposed_by: agent:claude
targets:
  - id: STATE-PRODUCT-DIRECTION-001
    action: create
    expected_revision: 0
requested_changes:
  - field: thesis
    before: null
    after: 意思決定した事実は一箇所にあるべきである（決定の単一正本）
  - field: pillars
    before: null
    after:
      - governance-single-source-plus-human-escalation
      - anti-rot-staleness-and-duplication-detection-with-agent-cleanup
  - field: positioning
    before: null
    after:
      primary_differentiation: vs-agent-memory
      promotional_headline: 人間のドキュメント管理ほど杜撰なものはない / DialogueはAgent向けGovernance Protocol
  - field: next-step
    before: null
    after: collision-and-rot-demo
  - field: north-star
    before: null
    after:
      concept: turbovec-backed-mcp-fast-canonical-search
      constraint: derivative-read-accelerator-not-canonical
      scope: post-v1
reason: >-
  office-hours（2026-07-17）でユーザーが確定した製品方向性、ポジショニング、次の一歩、
  North Starを正本化し、以後のAgentと人間が同じ方向性を根拠に判断できるようにする。
evidence_refs:
  - conversation:office-hours-2026-07-17
  - STATE-PRODUCT-SCOPE-001
impact: >-
  Product v1のスコープ契約と受入基準は不変。Anti-rotの「Agentによる継続整理」を製品約束として
  初めて正本化し、Turbovec MCPをv1スコープ外の派生層North Starとして記録する。
---

# Product Direction v1を正本化する

## Decision

ユーザーはoffice-hoursセッションで次を確定した。

- Thesis:「意思決定した事実は一箇所にあるべきである」。Dialogueは決定の単一正本である。
- キラー差別化に、陳腐化・重複を検知しAgentに整理させるAnti-rotの約束を加える。
- 主差別化は対Agent memory、プロモーション見出しは対wikiとする。
- 次の一歩はApproach A（衝突&腐敗の実演デモ）とする。
- Turbovecを連携させたMCPによる高速な正本検索をNorth Starとして記録する。ただし正本ではなく派生readアクセラレータとし、v1スコープ外とする。

## Approval evidence

会話中のユーザー確定発言（抜粋）:

- 「意思決定した事実は一箇所にあるべきであるという思想を伝えたいです。」
- 「dialogueでは情報の陳腐化、重複を検知し、Agentに整理させる約束を設けています。これはキラー差別化、あるいはこれが欲しかったという決め手につながると考えています。」
- 「Aで進めたいのですが、じつは今後Turbovecを連携させたmcpを用意し、高速に正本検索ができるようになるのではないか（中略）それがキラーコンテンツになり得ると考えています。」
- 「Aとします。なおこの議論によって決めたことはmanage-project-knowledgeスキルを利用してドキュメント化してください。」
