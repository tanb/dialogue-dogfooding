---
id: CHANGE-0016
type: change_record
title: agent権限をベンダー中立なAUTH-AGENT-001へ統合しfilesystem文言を刷新する
status: applied
scope:
  project: dialogue
  domain: "*"
  subject: "*"
revision: 1
created_at: "2026-07-18T03:00:00+09:00"
updated_at: "2026-07-18T03:00:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - PROPOSAL-0016
  - AUTHORITY-REGISTRY-001
extensions:
  approval_source: direct_user_instruction
  operation: change_governance
change_set_id: CHANGESET-0016
proposal_ref: PROPOSAL-0016
change_class: C4
decision: approved
approvals:
  - approval_id: APPROVAL-0016
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 2
    decided_at: "2026-07-18T03:00:00+09:00"
    conditions:
      - C4とchange_governanceはperson:project-owner専用のまま維持する
      - identity binding IDENTITY-FILESYSTEM-OWNER-001 は有効なlocal_account束縛として保持する
    evidence: >-
      統合する（AUTH-AGENT-001, agent:*）。CLAUDEとCODEXで分ける必要があるのか疑問です。
targets:
  - id: AUTHORITY-REGISTRY-001
    action: update
    before_revision: 2
    after_revision: 3
    result: applied
    error: null
reason: >-
  Registryの陳腐化（agent:claude未登録）を解消するため、agent権限をベンダー中立な
  AUTH-AGENT-001（agent:*）へ統合し、削除済みFilesystem Adapterを名指す記述を一般化する。
applied_at: "2026-07-18T03:00:00+09:00"
applied_by: agent:claude
---

# agent権限をベンダー中立なAUTH-AGENT-001へ統合する

## Applied changes

- `AUTHORITY-REGISTRY-001` を rev2→3 に更新（`change_governance` 操作、C4）。
- `AUTH-AGENT-CODEX-001`（actor_ref: agent:codex）を `AUTH-AGENT-001`（actor_ref: `agent:*`）へ置換。operations と change_classes(C0–C3) は不変、`delegated_by: AUTH-HUMAN-001`、C3 は owner Approval 必須の条件を維持。
- 条件に「`agent:*` は委任された任意のAIエージェントを表し、個々のactorはChange Recordのcreated_by/applied_byで監査する」を追記。
- 本文の「Filesystem AdapterではOSの実効UIDを認証主体として写像し…」を「ローカルOSアカウントの実効UID…」へ一般化。`agent:*` と C4/change_governance の人間専用性を明記。
- identity binding `IDENTITY-FILESYSTEM-OWNER-001` は有効な local_account 束縛として保持。

## Rationale

agent:codex と agent:claude は同一権限で運用されており、ベンダー別 authority は保守コストのみ増やす。単一のベンダー中立 authority に統合すると、将来のエージェント追加で登録が不要になり、監査は各 Change Record の created_by/applied_by で担保できる。Filesystem Adapter は削除・Archive 済みで、その名指しは陳腐化していた。

## Impact

- 委任エージェント（codex, claude, 将来の実装）の権限が `AUTH-AGENT-001` 一本で表現される。
- C4 と `change_governance` は `person:project-owner` 専用のまま。エージェントへ委任しない。
- Conformance ケースは各自 inline に authorities を持つ自己完結型のため、本変更の影響を受けない。
- 歴史的 Proposal/Change Record 内の `AUTH-AGENT-CODEX-001` / `agent:codex` は過去の記録として保持。
