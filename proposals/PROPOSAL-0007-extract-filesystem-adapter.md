---
id: PROPOSAL-0007
type: proposal
title: Separate the Filesystem Adapter from Product v1
status: approved
scope:
  project: dialogue
  domain: product
  subject: product-scope-v1
revision: 2
created_at: "2026-07-16T04:18:01+09:00"
updated_at: "2026-07-16T04:18:01+09:00"
created_by: agent:codex
updated_by: person:project-owner
related:
  - STATE-PRODUCT-SCOPE-001
  - STATE-REFERENCE-IMPLEMENTATION-001
  - PROPOSAL-0005
  - CHANGE-0007
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:current-user-instruction
  approved_subject_revision: 1
  change_record: CHANGE-0007
  approvals:
    - approval_id: APPROVAL-0007
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 1
      decided_at: "2026-07-16T04:18:01+09:00"
      conditions: []
change_class: C3
proposed_by: agent:codex
targets:
  - id: STATE-PRODUCT-SCOPE-001
    action: update
    expected_revision: 1
  - id: STATE-REFERENCE-IMPLEMENTATION-001
    action: update
    expected_revision: 3
requested_changes:
  - field: product-v1-deliverables
    before: Includes the Filesystem Adapter and a standalone CLI
    after: Includes only .knowledge.yml, the Git discovery Skill, and the Protocol
  - field: filesystem-reference-implementation.status
    before: active
    after: inactive
  - field: filesystem-reference-implementation.location
    before: product/
    after: development/experiments/filesystem-adapter/
reason: Remove Adapter-specific Protocol Engine development from the MVP, and focus on validating the user value of referencing and editing a Git Knowledge Repository through a Skill
evidence_refs:
  - development/tests/knowledge_git_e2e_test.rb
  - development/knowledge/docs/mvp-git-e2e-validation.md
  - product/skills/manage-project-knowledge/SKILL.md
impact: The distribution surface and maintenance scope of Product v1 shrink, and the existing Adapter remains as an experimental asset that is not deleted and has a resumption condition
---

# Separate the Filesystem Adapter from Product v1

## Decision

The user approved the policy of not developing `adapters/filesystem/lib` within the v1 scope. The Adapter and CLI are removed from the Product deliverables and preserved as an inactive development experiment.
