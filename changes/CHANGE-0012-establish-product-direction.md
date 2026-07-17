---
id: CHANGE-0012
type: change_record
title: Product Direction v1を正本として新規作成する
status: applied
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
  - PROPOSAL-0012
  - STATE-PRODUCT-DIRECTION-001
  - STATE-PRODUCT-SCOPE-001
extensions:
  approval_source: direct_user_instruction
  session: office-hours-2026-07-17
change_set_id: CHANGESET-0012
proposal_ref: PROPOSAL-0012
change_class: C3
decision: approved
approvals:
  - approval_id: APPROVAL-0012
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 0
    decided_at: "2026-07-17T23:59:31+09:00"
    conditions:
      - Turbovec検索層は正本ではなく派生readアクセラレータとして扱う
      - 本方向性はSTATE-PRODUCT-SCOPE-001のスコープ契約を変更しない
    evidence: >-
      Aとします。なおこの議論によって決めたことはmanage-project-knowledgeスキルを
      利用してドキュメント化してください。
targets:
  - id: STATE-PRODUCT-DIRECTION-001
    action: create
    before_revision: 0
    after_revision: 1
    result: applied
    error: null
reason: >-
  office-hoursで確定した製品方向性（Thesis、Two pillars、Positioning、次の一歩、North Star）を
  独立した正本Stateとして記録し、以後の判断根拠を単一の場所に置く。
applied_at: "2026-07-17T23:59:31+09:00"
applied_by: agent:claude
---

# Product Direction v1を正本として新規作成する

## Applied changes

- `STATE-PRODUCT-DIRECTION-001`（`docs/product-direction-v1.md`）を新規作成し、`canonical_for: dialogue/product/direction-v1`の正本とした。
- Thesis「決定の単一正本」、Two pillars（Governance + Anti-rot）、対Agent memory/対wikiのPositioning、次の一歩（Approach A: 衝突&腐敗デモ）、North Star（Turbovec MCP）を記録した。

## Rationale

`.knowledge.yml`によるGit Knowledge discoveryとHuman EscalationはProduct v1の主導線である。office-hoursで確定した方向性は、スコープ契約（`STATE-PRODUCT-SCOPE-001`）より上位の判断根拠であり、コードやGit履歴ではなく独立した正本Stateに置くべきである。これはDialogue自身のThesisのDogfoodingでもある。

## Impact

- Product v1のスコープ契約・受入基準は不変。
- Anti-rotの「Agentによる継続整理」を製品約束として初めて正本化した。
- Turbovec MCPはv1スコープ外の派生層North Starとして記録し、scope docのVector Database除外と矛盾しない。
- `STATE-PRODUCT-SCOPE-001`は本変更で更新していない（related参照のみ）。
