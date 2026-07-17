---
id: CHANGE-0005
type: change_record
title: Product v1をKnowledge Repository discoveryへ集中する
status: applied
scope:
  project: dialogue
  domain: product
  subject: product-scope-v1
revision: 1
created_at: "2026-07-16T04:00:43+09:00"
updated_at: "2026-07-16T04:00:43+09:00"
created_by: agent:codex
updated_by: agent:codex
related:
  - PROPOSAL-0005
  - PROJECT-CHARTER-001
  - STATE-PRODUCT-SCOPE-001
  - STATE-REFERENCE-IMPLEMENTATION-001
  - PROTOCOL-001
  - GOVERNANCE-001
  - CONFORMANCE-001
  - STATE-TRUSTED-APPROVAL-001
extensions:
  adapter: manual-filesystem
  approval_source: direct_user_instruction
  product_layout: product-development-split
change_set_id: CHANGESET-0005
proposal_ref: PROPOSAL-0005
change_class: C4
decision: approved
approvals:
  - approval_id: APPROVAL-0005
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 1
    decided_at: "2026-07-16T04:00:43+09:00"
    conditions: []
targets:
  - {id: PROPOSAL-0005, action: update, before_revision: 1, after_revision: 2, result: applied, error: null}
  - {id: STATE-PRODUCT-SCOPE-001, action: create, before_revision: 0, after_revision: 1, result: applied, error: null}
  - {id: PROJECT-CHARTER-001, action: update, before_revision: 2, after_revision: 3, result: applied, error: null}
  - {id: STATE-REFERENCE-IMPLEMENTATION-001, action: update, before_revision: 2, after_revision: 3, result: applied, error: null}
  - {id: PROTOCOL-001, action: update, before_revision: 3, after_revision: 4, result: applied, error: null}
  - {id: GOVERNANCE-001, action: update, before_revision: 3, after_revision: 4, result: applied, error: null}
  - {id: CONFORMANCE-001, action: update, before_revision: 3, after_revision: 4, result: applied, error: null}
  - {id: STATE-TRUSTED-APPROVAL-001, action: update, before_revision: 1, after_revision: 2, result: applied, error: null}
reason: 最初に検証すべき利用者価値を、共有Knowledge Repositoryの発見・参照・編集へ戻す
applied_at: "2026-07-16T04:00:43+09:00"
applied_by: agent:codex
---

# Product v1をKnowledge Repository discoveryへ集中する

## Applied changes

- 配布成果物を`product/`へ移動した。
- 設計知識、Proposal、Change Record、テスト、検証Scriptを`development/`へ移動した。
- `.knowledge.yml` v1 Schema、template、Resolverを追加した。
- Agent Skillの入口を`.knowledge.yml`へ変更した。
- Trusted Approvalを任意profileへ変更した。
- Project ScopeとReference Implementationを新しい導線へ同期した。

## Verification

```text
Repository validation: 21 documents, 28 Markdown files, 13 conformance cases passed
KnowledgeSourceTest: 5 runs, 20 assertions, 0 failures
FilesystemAdapterTest: 8 runs, 41 assertions, 0 failures
FilesystemCliTest: 4 runs, 24 assertions, 0 failures
TrustedApprovalTest: 7 runs, 31 assertions, 0 failures
Product protocol closure passed
```
