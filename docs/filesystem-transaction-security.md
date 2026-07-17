---
id: STATE-TRANSACTION-SECURITY-001
type: state
title: Filesystem Transaction Security
status: active
scope:
  project: dialogue
  domain: product
  subject: filesystem-transaction-security
revision: 1
created_at: "2026-07-16T03:27:16+09:00"
updated_at: "2026-07-16T03:27:16+09:00"
created_by: agent:codex
updated_by: agent:codex
related:
  - STATE-REFERENCE-IMPLEMENTATION-001
  - PROPOSAL-0003
  - CHANGE-0003
canonical_for: dialogue/product/filesystem-transaction-security
owners:
  - person:project-owner
extensions:
  document_kind: security-state
---

# Filesystem Transaction Security

## Current state

- Transaction markerは文書バックアップ本体をBase64で保持する。
- Markerは`0600`で作成し、同じOSユーザー以外へ公開しない。
- 通常文書は既存permission、または新規作成時`0644`を維持する。
- Prepared markerは次回操作でロールバックする。
- Committed markerは内容を維持したまま除去する。
- Marker、Lock、一時ファイルはGit管理対象外とする。

## Delegated change boundary

C0〜C2は有効なDelegationによってHuman Approvalなしで適用できる。C3とC4は引き続きHuman Approvalを必須とする。Delegation適用時はChange Recordの`approvals`を空配列とし、`extensions.delegation_ref`へ根拠を記録する。

## Verification

- `test_transaction_marker_is_private`
- `test_recovers_prepared_transaction_from_marker`
- `test_applies_delegated_c2_without_human_approval`
- `C-010-delegated-c2-without-human-approval.yml`
