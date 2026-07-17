---
id: AUTHORITY-REGISTRY-001
type: authority_registry
title: Dialogue Authority Registry
status: active
scope:
  project: dialogue
  domain: "*"
  subject: "*"
revision: 3
created_at: "2026-07-16T03:08:48+09:00"
updated_at: "2026-07-18T03:00:00+09:00"
created_by: agent:codex
updated_by: agent:claude
related:
  - PROPOSAL-0001
  - CHANGE-0001
  - PROPOSAL-0004
  - CHANGE-0004
  - PROPOSAL-0016
  - CHANGE-0016
extensions:
  identity_binding_version: 2
registry_for: dialogue
identity_bindings:
  - binding_id: IDENTITY-FILESYSTEM-OWNER-001
    provider: filesystem
    authenticated_id: uid:501
    actor_ref: person:project-owner
    assurance_level: local_account
    valid_from: "2026-07-16T03:38:10+09:00"
    valid_until: null
    status: active
authorities:
  - authority_id: AUTH-HUMAN-001
    actor_ref: person:project-owner
    role: human_authority
    scope:
      project: dialogue
      domain: "*"
      subject: "*"
    operations:
      - read
      - search
      - propose
      - review
      - approve
      - approve_semantic_change
      - resolve_conflict
      - activate
      - supersede
      - deactivate
      - archive
      - restore
      - change_governance
    change_classes: [C0, C1, C2, C3, C4]
    valid_from: "2026-07-16T03:08:48+09:00"
    valid_until: null
    delegated_by: null
    status: active
    conditions: []
  - authority_id: AUTH-AGENT-001
    actor_ref: "agent:*"
    role: agent
    scope:
      project: dialogue
      domain: "*"
      subject: "*"
    operations:
      - read
      - search
      - propose
      - edit_nonsemantic
      - update_state
      - review
      - activate
      - supersede
      - deactivate
      - archive
      - restore
    change_classes: [C0, C1, C2, C3]
    valid_from: "2026-07-18T03:00:00+09:00"
    valid_until: null
    delegated_by: AUTH-HUMAN-001
    status: active
    conditions:
      - C3の適用にはperson:project-ownerによる対象revisionへのApprovalが必要
      - "agent:* は委任された任意のAIエージェント（codex, claude 等）を表す。個々のactorはChange Recordのcreated_by/applied_byで監査する"
---

# Dialogue Authority Registry

本RegistryはDialogueプロジェクトのHuman AuthorityとAgent Delegationの正本である。

`person:project-owner`はプロジェクト所有者を表す論理Actorである。ローカルOSアカウントの実効UIDを認証主体として写像し、CLI引数だけを本人認証として扱わない。

`local_account`は同じOSアカウントで動くプロセスを区別しない。より強い保証が必要な運用では、Backendセッション、署名、または短命Capabilityへ置換する。

`agent:*`は委任された任意のAIエージェント（codex、claude 等）を表す単一の委任権限である。エージェント実装ごとに権限を分けず、個々の行為はChange Recordの`created_by`/`applied_by`で監査する。C4および`change_governance`は`person:project-owner`専用で、エージェントへ委任しない。
