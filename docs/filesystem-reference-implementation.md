---
id: STATE-REFERENCE-IMPLEMENTATION-001
type: state
title: Filesystem Reference Adapter Experiment
status: archived
scope:
  project: dialogue
  domain: product
  subject: filesystem-reference-implementation
revision: 5
created_at: "2026-07-16T03:23:25+09:00"
updated_at: "2026-07-17T22:55:37+09:00"
created_by: agent:codex
updated_by: agent:claude
related:
  - PROTOCOL-001
  - GOVERNANCE-001
  - CONFORMANCE-001
  - PROPOSAL-0002
  - CHANGE-0002
  - STATE-TRUSTED-APPROVAL-001
  - PROPOSAL-0004
  - CHANGE-0004
  - STATE-PRODUCT-SCOPE-001
  - PROPOSAL-0005
  - CHANGE-0005
  - PROPOSAL-0007
  - CHANGE-0007
  - CHANGE-0010
canonical_for: dialogue/product/filesystem-reference-implementation
owners:
  - person:project-owner
extensions:
  document_kind: product-component
  version: 0.3.0
  development_status: removed
  product_status: out-of-v1
---

# Filesystem Reference Adapter Experiment

## Current disposition

この実験実装は2026-07-17にリポジトリから削除された（`CHANGE-0010`）。コード、CLI、API/CLIテストはリポジトリに残っていない。本StateはArchivedであり、通常のResolveでは選択されず、明示的な履歴調査のためにのみ参照する。

削除前の構成（歴史的記録）:

- CLI: `development/experiments/filesystem-adapter/bin/dialogue`（削除済み）
- Adapter: `development/experiments/filesystem-adapter/adapters/filesystem/lib/dialogue/`（削除済み）
- API tests: `development/tests/filesystem_adapter_test.rb`（削除済み）
- CLI tests: `development/tests/filesystem_cli_test.rb`（削除済み）

この実装はProduct v1の配布対象ではなかった。Product v1の主導線は、`product/skills/manage-project-knowledge/`が`.knowledge.yml`からGit Knowledge Repositoryを発見し、標準のGit操作とファイル操作で参照・編集するフローである。以下の設計知見は、将来Adapter相当の決定的操作APIを再検討する際の起点として保持する。

## Supported workflow

```text
.knowledge.yml → Git checkout → Resolve → Edit → Change Record → Validate
```

Trusted Approvalを採用したRepositoryでは、Proposal → Human Approval → Applyを追加する。

CLI commands:

```text
dialogue resolve
dialogue list
dialogue propose
dialogue approve
dialogue apply
dialogue validate
```

Archive、Restore、Supersede、Deactivateは、Proposalのtarget actionとstatus変更を通じてApplyする。

## Core guarantees

- Activeな`canonical_for`の一意性を検証する。
- `expected_revision`によってLost Updateを拒否する。
- 複数文書の書込み前に回復用transaction markerを作る。
- 検証失敗時にState、Proposal、Change Recordをまとめてロールバックする。
- 文書内命令をAgent権限として扱わない。

## Optional Trusted Approval profile

採用したRepositoryに限り、次を保証する。

- Human ApprovalとAgent DelegationをAuthority Registryで分離する。
- Human ApprovalをOS Identity、Proposal ID、revision、SHA-256 Digestへ束縛する。
- Approvalの期限切れ、権限失効、別Proposalへの転用、再利用を拒否する。

## Current limits

- 既存文書はtop-level front matterのみ変更できる。
- 新規文書はmetadataと本文をまとめて作成できる。
- Human ApprovalのIdentity保証はOS実効UIDの`local_account`水準であり、同一UIDのプロセスを区別しない。
- Agent Applyの`--actor`はDelegation識別子であり、ランタイム本人性を証明しない。
- Process crash後の回復は、同じ共有Filesystemで次回CLI操作が行われたときに実行する。
- 複数ホスト間の分散Lockは提供しない。

Trusted Approval profileを実装するProduction Adapterは、Backendの認証済みユーザーIDをActor referenceへ写像し、Approval EnvelopeへIdentity Evidenceを保存しなければならない。

## Resume criteria

- 複数文書更新の原子性または回復処理が実利用で必要になる。
- Git以外のBackendへ共通操作を移植する。
- 複数のAgent runtimeから同じ決定的操作APIを利用する。

## Validation

実装とテストは削除済みのため、本Stateに対応する実行検証はない。リポジトリ全体の検証手順は`README.md`の Development validation を参照する。
