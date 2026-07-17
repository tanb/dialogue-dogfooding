---
id: PROPOSAL-0004
type: proposal
title: Adopt Trusted Approval v0.2
status: approved
scope:
  project: dialogue
  domain: governance
  subject: trusted-approval
revision: 2
created_at: "2026-07-16T03:38:10+09:00"
updated_at: "2026-07-16T03:38:10+09:00"
created_by: agent:codex
updated_by: person:project-owner
related:
  - AUTHORITY-REGISTRY-001
  - STATE-TRUSTED-APPROVAL-001
  - STATE-REFERENCE-IMPLEMENTATION-001
  - CHANGE-0004
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:current-user-instruction
  change_record: CHANGE-0004
  approved_subject_revision: 1
  approvals:
    - approval_id: APPROVAL-0004
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 1
      decided_at: "2026-07-16T03:38:10+09:00"
      conditions: []
change_class: C4
proposed_by: agent:codex
targets:
  - id: STATE-TRUSTED-APPROVAL-001
    action: create
    expected_revision: 0
  - id: AUTHORITY-REGISTRY-001
    action: update
    expected_revision: 1
requested_changes:
  - field: STATE-TRUSTED-APPROVAL-001
    before: null
    after: Create the normative specification of Trusted Approval v0.2 as an active State
  - field: AUTHORITY-REGISTRY-001.identity_bindings
    before: null
    after: Bind filesystem:uid:501 to person:project-owner with a local_account guarantee
  - field: filesystem-approval-flow
    before: Trust the actor_ref of the CLI argument
    after: Verify the OS Identity, the Proposal Digest, and the Approval Envelope
reason: Prevent impersonation of Human Approval, post-approval tampering, reuse for a different Proposal, and use of an expired or revoked approval
evidence_refs:
  - docs/failure-model.md
  - docs/knowledge-governance.md
  - adapters/filesystem/lib/dialogue/workflow.rb
  - adapters/filesystem/lib/dialogue/apply_operation.rb
  - tests/filesystem_cli_test.rb
impact: The binding between an approval's authenticity and its target content is strengthened, and the old CLI contract is changed in a breaking way
---

# Adopt Trusted Approval v0.2

## Decision

The user explicitly stated "Please go ahead" regarding the Trusted Approval v0.2 work presented immediately beforehand. This instruction is recorded as Human Approval for the C4 change.

This approval occurred before the introduction of the new specification, so it uses the v0.1 history format. Approvals created after `STATE-TRUSTED-APPROVAL-001` takes effect require the v0.2 Envelope.
