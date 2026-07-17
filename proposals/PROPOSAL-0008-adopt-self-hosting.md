---
id: PROPOSAL-0008
type: proposal
title: Adopt self-hosting for Dialogue development
status: approved
scope:
  project: dialogue
  domain: development
  subject: self-hosting
revision: 2
created_at: "2026-07-16T04:29:45+09:00"
updated_at: "2026-07-16T04:29:45+09:00"
created_by: agent:codex
updated_by: person:project-owner
related:
  - PROJECT-CHARTER-001
  - STATE-SELF-HOSTING-001
  - STATE-PRODUCT-SCOPE-001
  - CHANGE-0008
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:current-user-instruction
  approved_subject_revision: 1
  change_record: CHANGE-0008
  approvals:
    - approval_id: APPROVAL-0008
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 1
      decided_at: "2026-07-16T04:29:45+09:00"
      conditions: []
change_class: C3
proposed_by: agent:codex
targets:
  - id: PROJECT-CHARTER-001
    action: update
    expected_revision: 3
  - id: STATE-SELF-HOSTING-001
    action: create
    expected_revision: 0
requested_changes:
  - field: project-charter.design-principles.self-hosting
    before: null
    after: Use manage-project-knowledge in Dialogue's own development, and reflect real usage results into Product improvements
  - field: agent-skill.decision-capture
    before: Take an explicit Skill name or a general editing request as the primary trigger condition
    after: Implicitly capture persistent decisions that were settled in conversation, without a Skill name being specified
  - field: agent-policy.bootstrap
    before: Interim operation for self-hosting is undefined
    after: Use development/knowledge as an interim storage location until a real Git remote is configured
reason: Develop Dialogue itself with Dialogue, and improve the accuracy of Decision Capture, the operational load, and conflict handling from real usage
evidence_refs:
  - conversation:current-user-instruction
  - product/skills/manage-project-knowledge/SKILL.md
  - AGENTS.md
impact: In subsequent Dialogue development, decisions reached in conversation become automatic candidates for Knowledge records
---

# Adopt self-hosting for Dialogue development

## Decision

The user's "Let's proceed with that policy" is recorded as explicit Human Approval for the Dialogue self-hosting policy that was presented immediately beforehand.
