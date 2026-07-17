---
id: CHANGE-0008
type: change_record
title: Adopt Self-hosting for Dialogue development
status: applied
scope:
  project: dialogue
  domain: development
  subject: self-hosting
revision: 1
created_at: "2026-07-16T04:29:45+09:00"
updated_at: "2026-07-16T04:29:45+09:00"
created_by: agent:codex
updated_by: agent:codex
related:
  - PROPOSAL-0008
  - PROJECT-CHARTER-001
  - STATE-SELF-HOSTING-001
extensions:
  adapter: bootstrap-filesystem
  approval_source: direct_user_instruction
  self_hosted_change: true
  remote_binding_status: pending
change_set_id: CHANGESET-0008
proposal_ref: PROPOSAL-0008
change_class: C3
decision: approved
approvals:
  - approval_id: APPROVAL-0008
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 1
    decided_at: "2026-07-16T04:29:45+09:00"
    conditions: []
targets:
  - id: PROPOSAL-0008
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: PROJECT-CHARTER-001
    action: update
    before_revision: 3
    after_revision: 4
    result: applied
    error: null
  - id: STATE-SELF-HOSTING-001
    action: create
    before_revision: 0
    after_revision: 1
    result: applied
    error: null
reason: Develop Dialogue itself with Dialogue, and improve the accuracy of Decision Capture, the operational load, and conflict handling from real usage
applied_at: "2026-07-16T04:29:45+09:00"
applied_by: agent:codex
---

# Adopt Self-hosting for Dialogue development

## Applied changes

- Enabled implicit invocation via the Skill metadata.
- Added a procedure to the Skill for extracting decided facts from conversations.
- Added Local Skill activation and bootstrap rules to Dialogue's `AGENTS.md`.
- Added the Self-hosting principle to the Project Charter.
- Recorded the current state of Self-hosting and the not-yet-connected remote.

## First dogfooding observation

"Let's proceed with that approach" does not contain a Skill name, but it could be resolved as a clear approval of the immediately preceding, identifiable Self-hosting proposal. This Change Record is the first conversational Decision Capture result.
