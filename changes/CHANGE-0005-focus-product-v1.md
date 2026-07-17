---
id: CHANGE-0005
type: change_record
title: Focus Product v1 on Knowledge Repository discovery
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
reason: Return the user value to be validated first to the discovery, reference, and editing of a shared Knowledge Repository
applied_at: "2026-07-16T04:00:43+09:00"
applied_by: agent:codex
---

# Focus Product v1 on Knowledge Repository discovery

## Applied changes

- Moved the distribution deliverables to `product/`.
- Moved the design knowledge, Proposals, Change Records, tests, and verification scripts to `development/`.
- Added the `.knowledge.yml` v1 Schema, template, and Resolver.
- Changed the entry point of the Agent Skill to `.knowledge.yml`.
- Changed Trusted Approval to an optional profile.
- Synced the Project Scope and Reference Implementation to the new flow.

## Verification

```text
Repository validation: 21 documents, 28 Markdown files, 13 conformance cases passed
KnowledgeSourceTest: 5 runs, 20 assertions, 0 failures
FilesystemAdapterTest: 8 runs, 41 assertions, 0 failures
FilesystemCliTest: 4 runs, 24 assertions, 0 failures
TrustedApprovalTest: 7 runs, 31 assertions, 0 failures
Product protocol closure passed
```
