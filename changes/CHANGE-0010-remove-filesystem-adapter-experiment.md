---
id: CHANGE-0010
type: change_record
title: Filesystem Adapter実験実装とテストをリポジトリから削除する
status: applied
scope:
  project: dialogue
  domain: product
  subject: filesystem-reference-implementation
revision: 1
created_at: "2026-07-17T22:55:37+09:00"
updated_at: "2026-07-17T22:55:37+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - STATE-REFERENCE-IMPLEMENTATION-001
  - CHANGE-0007
  - PROPOSAL-0007
extensions:
  approval_source: direct_user_instruction
  product_boundary: git-discovery-skill
  change_set_id: CHANGESET-0010
change_class: C3
decision: approved
approvals:
  - approval_id: APPROVAL-0010
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 1
    decided_at: "2026-07-17T22:55:37+09:00"
    conditions: []
    evidence: >-
      experiments/filesystem-adapterは実験コードだったのでレポジトリに含む予定は
      現時点ではありませんでした。なので、experiments/filesystem-adapterを削除して
      よいです。それに付随するテストも不要になります。
targets:
  - id: STATE-REFERENCE-IMPLEMENTATION-001
    action: update
    before_revision: 4
    after_revision: 5
    result: applied
    error: null
reason: >-
  Reference Adapterは当初からリポジトリへ含める予定のない実験コードであり、
  Product v1の主導線に不要なため、実装・CLI・依存テストを削除しStateをArchivedにする
applied_at: "2026-07-17T22:55:37+09:00"
applied_by: agent:claude
---

# Filesystem Adapter実験実装とテストをリポジトリから削除する

## Applied changes

- `development/experiments/filesystem-adapter/`（Adapter、CLI、`lib/dialogue/`、Skill wrapper）を削除した。
- 依存テスト `filesystem_adapter_test.rb`、`filesystem_cli_test.rb`、`trusted_approval_test.rb`、`support/filesystem_fixture.rb`を削除した。
- `STATE-REFERENCE-IMPLEMENTATION-001`をInactiveからArchivedへ遷移し、実装が撤去済みであることを記録した。
- CI、`AGENTS.md`、`README.md`から実験テストの実行手順を除去した。

## Rationale

Reference Adapterは当初からリポジトリへ含める予定のない実験コードであった。Product v1の主導線は`.knowledge.yml`によるGit Knowledge Repository discoveryであり、Adapter固有のProtocol Engineは配布対象に含めない。実験が確立した設計知見（正本一意性、Lost Update拒否、multi-document transaction、Trusted Approvalの束縛）は、`STATE-REFERENCE-IMPLEMENTATION-001`にArchived Stateとして保持する。

## Impact

- Product v1の主導線とConformance検証には影響しない。
- 検証の主線はProtocol Conformance（Ruby/Python並走ランナー）と`.knowledge.yml`解決・Skill起動・Git E2Eに集約される。
- 将来Adapter相当の決定的操作APIが実利用で必要になった場合は、Archived Stateの再開条件を起点に新規実装として再検討する。
