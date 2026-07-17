---
id: PROPOSAL-0016
type: proposal
title: agent権限をベンダー中立なAUTH-AGENT-001へ統合しfilesystem文言を刷新する
status: approved
scope:
  project: dialogue
  domain: "*"
  subject: "*"
revision: 1
created_at: "2026-07-18T03:00:00+09:00"
updated_at: "2026-07-18T03:00:00+09:00"
created_by: agent:claude
updated_by: person:project-owner
related:
  - AUTHORITY-REGISTRY-001
  - CHANGE-0016
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:refresh-authority-registry-2026-07-18
  approved_subject_revision: 2
  change_record: CHANGE-0016
  operation: change_governance
  approvals:
    - approval_id: APPROVAL-0016
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 2
      decided_at: "2026-07-18T03:00:00+09:00"
      conditions:
        - C4とchange_governanceはperson:project-owner専用のまま維持する
        - identity binding IDENTITY-FILESYSTEM-OWNER-001 は有効なlocal_account束縛として保持する
change_class: C4
proposed_by: agent:claude
targets:
  - id: AUTHORITY-REGISTRY-001
    action: update
    expected_revision: 2
requested_changes:
  - field: agent-authority
    before:
      authority_id: AUTH-AGENT-CODEX-001
      actor_ref: agent:codex
    after:
      authority_id: AUTH-AGENT-001
      actor_ref: "agent:*"
      change_classes: [C0, C1, C2, C3]
  - field: identity-prose
    before: Filesystem AdapterではOSの実効UIDを認証主体として写像する
    after: ローカルOSアカウントの実効UIDを認証主体として写像する
reason: >-
  agent:codex と agent:claude は同一の権限（operations・C0–C3）で運用されており、ベンダー別に
  分ける実益が乏しい。単一のベンダー中立な委任権限 AUTH-AGENT-001（actor_ref: agent:*）へ統合し、
  将来のエージェント追加で登録を不要にする。あわせて削除済みのFilesystem Adapterを名指す
  陳腐化した本人認証の記述を一般化する。
evidence_refs:
  - conversation:refresh-authority-registry-2026-07-18
  - AUTHORITY-REGISTRY-001
impact: >-
  委任エージェントの権限はactor_ref: agent:* の単一authorityで表現される。監査は各Change Recordの
  created_by/applied_byで担保する。C4・change_governanceは人間専用のまま不変。identity bindingは保持。
---

# agent権限をベンダー中立なAUTH-AGENT-001へ統合する

## Decision

`AUTHORITY-REGISTRY-001` が陳腐化していた。`agent:claude` は本セッションで多数の Proposal / Change Record（C3・C4）を作成・適用してきたが、Registry には `AUTH-AGENT-CODEX-001`（agent:codex）しか登録されていなかった。

ユーザー（person:project-owner）の判断により、ベンダー別に分けず、単一のベンダー中立な委任権限へ統合する。

- `AUTH-AGENT-CODEX-001`（agent:codex）→ `AUTH-AGENT-001`（`actor_ref: agent:*`, role:agent, operations 同一, change_classes C0–C3, delegated_by AUTH-HUMAN-001, C3 は owner Approval 必須）
- 削除済み Filesystem Adapter を名指す本人認証の記述を「ローカルOSアカウントの実効UID」に一般化
- C4 と `change_governance` は `person:project-owner` 専用のまま

## Approval evidence

- 「AUTHORITY-REGISTRY-001.mdが陳腐化しています。dialogue-knowledgeスキルを使用して修正してください。」
- 「CLAUDEとCODEXで分ける必要があるのか疑問です。」
- 「統合する（AUTH-AGENT-001, agent:*）」「一緒に修正」（D1再/D2 の確定）
