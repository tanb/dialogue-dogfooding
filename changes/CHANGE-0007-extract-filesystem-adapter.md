---
id: CHANGE-0007
type: change_record
title: Separate the Filesystem Adapter from Product v1
status: applied
scope:
  project: dialogue
  domain: product
  subject: product-scope-v1
revision: 1
created_at: "2026-07-16T04:18:01+09:00"
updated_at: "2026-07-16T04:18:01+09:00"
created_by: agent:codex
updated_by: agent:codex
related:
  - PROPOSAL-0007
  - STATE-PRODUCT-SCOPE-001
  - STATE-REFERENCE-IMPLEMENTATION-001
extensions:
  adapter: manual-filesystem
  approval_source: direct_user_instruction
  product_boundary: git-discovery-skill
change_set_id: CHANGESET-0007
proposal_ref: PROPOSAL-0007
change_class: C3
decision: approved
approvals:
  - approval_id: APPROVAL-0007
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 1
    decided_at: "2026-07-16T04:18:01+09:00"
    conditions: []
targets:
  - id: PROPOSAL-0007
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: STATE-PRODUCT-SCOPE-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: STATE-REFERENCE-IMPLEMENTATION-001
    action: update
    before_revision: 3
    after_revision: 4
    result: applied
    error: null
reason: Remove Adapter-specific Protocol Engine development from the MVP and focus on validating the user value of referencing and editing a Git Knowledge Repository with a Skill
applied_at: "2026-07-16T04:18:01+09:00"
applied_by: agent:codex
---

# Separate the Filesystem Adapter from Product v1

## Applied changes

- Moved the Adapter, CLI, and Skill wrapper to `development/experiments/filesystem-adapter/`.
- Removed the dependency of the Product Skill on the reference CLI.
- Excluded the Adapter and CLI from the Product Scope.
- Made the Reference Implementation inactive and recorded the conditions for resumption.
