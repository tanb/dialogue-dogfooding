---
id: CHANGE-0004
type: change_record
title: Trusted Approval v0.2を採用する
status: applied
scope:
  project: dialogue
  domain: governance
  subject: trusted-approval
revision: 1
created_at: "2026-07-16T03:38:10+09:00"
updated_at: "2026-07-16T03:38:10+09:00"
created_by: agent:codex
updated_by: agent:codex
related:
  - PROPOSAL-0004
  - STATE-TRUSTED-APPROVAL-001
  - AUTHORITY-REGISTRY-001
  - PROTOCOL-001
  - GOVERNANCE-001
  - CONFORMANCE-001
  - STATE-REFERENCE-IMPLEMENTATION-001
extensions:
  adapter: manual-filesystem
  approval_source: direct_user_instruction
  approval_format: v0.1-bootstrap
  validation_cases: 13
change_set_id: CHANGESET-0004
proposal_ref: PROPOSAL-0004
change_class: C4
decision: approved
approvals:
  - approval_id: APPROVAL-0004
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 1
    decided_at: "2026-07-16T03:38:10+09:00"
    conditions: []
targets:
  - id: PROPOSAL-0004
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: STATE-TRUSTED-APPROVAL-001
    action: create
    before_revision: 0
    after_revision: 1
    result: applied
    error: null
  - id: AUTHORITY-REGISTRY-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: PROTOCOL-001
    action: update
    before_revision: 2
    after_revision: 3
    result: applied
    error: null
  - id: GOVERNANCE-001
    action: update
    before_revision: 2
    after_revision: 3
    result: applied
    error: null
  - id: CONFORMANCE-001
    action: update
    before_revision: 2
    after_revision: 3
    result: applied
    error: null
  - id: STATE-REFERENCE-IMPLEMENTATION-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
reason: Human Approvalのなりすまし、承認後改変、別Proposalへの転用、期限切れまたは失効済み承認の利用を防ぐ
applied_at: "2026-07-16T03:38:10+09:00"
applied_by: agent:codex
---

# Trusted Approval v0.2を採用する

## Applied changes

- OS実効UIDを論理Human Actorへ解決するIdentity Resolverを追加した。
- Proposalの承認対象をcanonical JSONとSHA-256 Digestへ固定した。
- Approval EnvelopeへSubject ID、revision、Digest、有効期限、Identity Evidenceを追加した。
- Apply時に改変、転用、再利用、期限切れ、Identity/Authority失効を検証した。
- Human Approval CLIから自己申告の`--actor`を削除した。
- Core Skill、Schema、Authority Registry、参照実装文書をv0.2へ同期した。

## Verification evidence

```text
13 conformance cases passed
FilesystemAdapterTest: 8 runs, 41 assertions, 0 failures, 0 errors
FilesystemCliTest: 4 runs, 24 assertions, 0 failures, 0 errors
TrustedApprovalTest: 7 runs, 31 assertions, 0 failures, 0 errors
```

## Residual limits

- `local_account`は同じOS UIDで動く複数プロセスを区別しない。
- Agent Applyの`--actor`はDelegation識別子であり、Agent runtime identityの証明ではない。
- Approval Envelopeは参照実装内で署名されない。強い改ざん耐性にはBackend監査または署名が必要である。
