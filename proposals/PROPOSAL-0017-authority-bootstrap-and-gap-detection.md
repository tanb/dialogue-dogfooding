---
id: PROPOSAL-0017
type: proposal
title: Authority bootstrap最小構成・未登録安全既定・Authority gap検出を導入する
status: approved
scope:
  project: dialogue
  domain: governance
  subject: knowledge-governance
revision: 1
created_at: "2026-07-18T04:00:00+09:00"
updated_at: "2026-07-18T04:00:00+09:00"
created_by: agent:claude
updated_by: person:project-owner
related:
  - GOVERNANCE-001
  - FAILURE-MODEL-001
  - AUTHORITY-REGISTRY-001
  - CHANGE-0017
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:authority-gap-detection-2026-07-18
  approved_subject_revision: 4
  change_record: CHANGE-0017
  operation: change_governance
  approvals:
    - approval_id: APPROVAL-0017
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 4
      decided_at: "2026-07-18T04:00:00+09:00"
      conditions:
        - 検知はCIに依存せずSkillが実行できる決定的スクリプトとして同梱する
        - hardは承認者未登録に限定しfail-closed、softは可視化にとどめる
change_class: C4
proposed_by: agent:claude
targets:
  - id: GOVERNANCE-001
    action: update
    expected_revision: 4
  - id: FAILURE-MODEL-001
    action: update
    expected_revision: 2
requested_changes:
  - field: registry-bootstrap
    before: 最小構成の規定なし（最初の作成者が実装名でagent権限を作りうる）
    after: Human Authority ×1 と ベンダー中立な委任エージェント役割(agent:*) ×1 を必須化
  - field: unregistered-actor-default
    before: propose も authority 必須（未登録は何もできない）
    after: read/search/propose は ungated、update_state/approve/C1以上の適用は authority 必須
  - field: authority-gap-detection
    before: 検知手段なし（登録漏れが不可視）
    after: actor↔registry の機械突合を規定。hard=承認者未登録でfail-closed、soft=可視化。同梱スクリプトで実行
reason: >-
  Registryを最初にagent:codexという実装名で作ったため、claudeを後から登録すべきかという
  判断課題が生じた。役割ベースのbootstrap最小構成を明文化し、未登録アクターの安全既定と、
  登録漏れを見逃さないためのAuthority gap検出（CI非依存の同梱スクリプト）を導入する。
evidence_refs:
  - conversation:authority-gap-detection-2026-07-18
  - GOVERNANCE-001
  - FAILURE-MODEL-001
impact: >-
  今後どのエージェントが増えても登録不要。未登録アクターは提案まで可能で系は止まらないが、
  C3/C4の承認者未登録はfail-closedで停止・エスカレーション、その他の未登録は保守項目として
  可視化される。検知はユーザーのCIの有無に依存しない。
---

# Authority bootstrap最小構成とAuthority gap検出を導入する

## Decision

Authority Registry を最初に `agent:codex`（実装名）で作ったことで、`agent:claude` を後から登録すべきかという判断課題が生じた。ユーザー判断により、根本を次で固定する。

1. **Bootstrap 最小構成**: すべての Registry は Human Authority ×1 と ベンダー中立な委任エージェント役割（`agent:*`, C0–C3, C3 は人間承認必須, C4 不可）を持つ。
2. **未登録アクターの安全既定**: read/search/propose は ungated、それ以上は authority 必須（fail-closed だが提案は塞がない）。
3. **Authority gap 検出**: actor↔registry を機械突合し、hard（C3/C4 の承認者が未登録 Human Authority）は fail-closed、soft（その他の未登録）は可視化。**CI 非依存の同梱スクリプト** `skills/dialogue-knowledge/scripts/check-authority` として提供する。

## Approval evidence

- 「HUMANとAGENTを最初に用意するように明確化した方が良いでしょうか？またはほかのプロセスが考えられますか？」
- 「1で良いと考えますが、以前として未登録アクターを検知することができなければ、登録忘れが見逃され続ける可能性があります。」
- 「skillを使用したユーザーが必ずしもそのレポジトリでCIを実施しているかどうかわかりません。」（CI 非依存を要件化）
- 「A」（決定的スクリプトを同梱する方針の確定）
