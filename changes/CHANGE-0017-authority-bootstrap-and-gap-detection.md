---
id: CHANGE-0017
type: change_record
title: Authority bootstrap最小構成・未登録安全既定・Authority gap検出を導入する
status: applied
scope:
  project: dialogue
  domain: governance
  subject: knowledge-governance
revision: 1
created_at: "2026-07-18T04:00:00+09:00"
updated_at: "2026-07-18T04:00:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - PROPOSAL-0017
  - GOVERNANCE-001
  - FAILURE-MODEL-001
  - AUTHORITY-REGISTRY-001
extensions:
  approval_source: direct_user_instruction
  operation: change_governance
change_set_id: CHANGESET-0017
proposal_ref: PROPOSAL-0017
change_class: C4
decision: approved
approvals:
  - approval_id: APPROVAL-0017
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 4
    decided_at: "2026-07-18T04:00:00+09:00"
    conditions:
      - 検知はCIに依存せずSkillが実行できる決定的スクリプトとして同梱する
      - hardは承認者未登録に限定しfail-closed、softは可視化にとどめる
    evidence: >-
      A（決定的スクリプト同梱）。skillを使用したユーザーが必ずしもそのレポジトリでCIを
      実施しているかどうかわかりません。
targets:
  - id: GOVERNANCE-001
    action: update
    before_revision: 4
    after_revision: 5
    result: applied
    error: null
  - id: FAILURE-MODEL-001
    action: update
    before_revision: 2
    after_revision: 3
    result: applied
    error: null
reason: >-
  役割ベースのbootstrap最小構成、未登録アクターの安全既定、CI非依存のAuthority gap検出を
  導入し、実装名でのagent権限付与が生む判断課題と登録漏れの不可視化を解消する。
applied_at: "2026-07-18T04:00:00+09:00"
applied_by: agent:claude
---

# Authority bootstrap最小構成とAuthority gap検出を導入する

## Applied changes

### Protocol / Failure model
- `GOVERNANCE-001` rev4→5：§5.1 Bootstrap 最小構成（Human + `agent:*`）、§5.2 未登録アクターの安全既定（read/search/propose は ungated）、§5.3 Authority gap 検出（hard=承認者未登録で fail-closed、soft=可視化、CI 非依存）を追加。
- `FAILURE-MODEL-001` rev2→3：`F16. Authority gap（未登録アクター）` を追加。

### 製品成果物（配布物）
- `skills/dialogue-knowledge/scripts/check-authority`（新規）：actor↔registry を機械突合する決定的チェッカー。hard gap で exit 2（fail-closed）、soft gap は一覧化。PyYAML 依存、CI 非依存。
- `skills/dialogue-knowledge/SKILL.md`：Registry bootstrap 手順と "Reconcile authority" 手順（checker 実行、hard=停止・エスカレーション、soft=保守項目）を追加。
- `templates/authority-registry.md`（新規）：Human + `agent:*` を持つ既定 Registry テンプレート。

### 内部（dogfooding）
- `scripts/validate_repository.py`：同梱 checker を自身の `dogfooding/` に対して実行する `validate_authority()` を追加（hard gap で検証失敗）。
- `tests/test_authority_check.py`（新規）：clean / hard（未登録 C4 承認者）/ agent:* カバレッジ / soft の4契約を固定。`tests/dialogue_support.py` に `CHECKER` パスを追加。

## Rationale

Registry を最初に `agent:codex` という実装名で作ったため、新エージェント登録の判断課題が生じた。権限を役割（`agent:*`）に束ねる bootstrap 最小構成でこれを恒久的に解消する。安全既定だけでは登録漏れが不可視化するため、検知を規範化し、ユーザーの CI 有無に依存しないよう Skill 同梱の決定的スクリプトとして提供する。

## Impact

- 新しいエージェントの追加で Registry 登録が不要。
- 未登録アクターは提案まで可能（系は止まらない）。C3/C4 の承認者未登録は fail-closed で停止、その他の未登録は可視化される。
- 検知は `python3 skills/dialogue-knowledge/scripts/check-authority --document-root <root>` で誰でも実行でき、CI に依存しない。
- Conformance ケースは自己完結型のため影響を受けない。歴史的記録の `agent:codex` 等は保持。
