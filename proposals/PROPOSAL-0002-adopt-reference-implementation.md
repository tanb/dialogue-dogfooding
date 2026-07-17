---
id: PROPOSAL-0002
type: proposal
title: Adopt the Filesystem Reference Adapter and the Core Skill
status: approved
scope:
  project: dialogue
  domain: product
  subject: filesystem-reference-implementation
revision: 3
created_at: "2026-07-16T03:23:25+09:00"
updated_at: "2026-07-16T03:23:25+09:00"
created_by: agent:codex
updated_by: agent:codex
related:
  - STATE-REFERENCE-IMPLEMENTATION-001
  - PROTOCOL-001
  - GOVERNANCE-001
  - CHANGE-0002
extensions:
  approval_source: direct_user_instruction
  approved_subject_revision: 1
  change_record: CHANGE-0002
  approvals:
    - approval_id: APPROVAL-0002
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 1
      decided_at: "2026-07-16T03:23:25+09:00"
      conditions: []
change_class: C3
proposed_by: agent:codex
targets:
  - id: STATE-REFERENCE-IMPLEMENTATION-001
    action: create
    expected_revision: 0
requested_changes:
  - field: STATE-REFERENCE-IMPLEMENTATION-001
    before: null
    after:
      metadata:
        type: state
        title: Filesystem Reference Adapter and Core Skill
        status: active
        scope:
          project: dialogue
          domain: product
          subject: filesystem-reference-implementation
        canonical_for: dialogue/product/filesystem-reference-implementation
        owners:
          - person:project-owner
      body: Provide the Filesystem Adapter, CLI, Core Skill, and integration tests as the v0.1 reference implementation
reason: Demonstrate the executability of the Protocol through a vertical slice on the filesystem
evidence_refs:
  - tests/filesystem_adapter_test.rb
  - tests/filesystem_cli_test.rb
  - skills/manage-project-knowledge/SKILL.md
impact: A minimum product becomes available in which humans and Agents can safely resolve, propose, approve, and apply shared knowledge
---

# Adopt the Filesystem Reference Adapter and the Core Skill

The user's direct instruction was recorded as Human Approval for revision 1. Adding the approval record produced revision 2, and adding the Change Record reference after application produced revision 3.
