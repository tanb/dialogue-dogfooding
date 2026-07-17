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

- The transaction marker holds the document backup itself in Base64.
- The marker is created with `0600` and is not exposed to anyone other than the same OS user.
- Ordinary documents keep their existing permissions, or `0644` at new creation.
- A prepared marker is rolled back at the next operation.
- A committed marker is removed while keeping its content.
- Markers, Locks, and temporary files are excluded from Git management.

## Delegated change boundary

C0 through C2 can be applied without Human Approval by a valid Delegation. C3 and C4 continue to require Human Approval. When a Delegation is applied, the Change Record's `approvals` is an empty array, and the basis is recorded in `extensions.delegation_ref`.

## Verification

- `test_transaction_marker_is_private`
- `test_recovers_prepared_transaction_from_marker`
- `test_applies_delegated_c2_without_human_approval`
- `C-010-delegated-c2-without-human-approval.yml`
