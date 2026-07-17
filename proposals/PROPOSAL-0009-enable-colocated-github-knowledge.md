---
id: PROPOSAL-0009
type: proposal
title: Enable a co-located Knowledge source on private GitHub
status: approved
scope:
  project: dialogue
  domain: development
  subject: self-hosting
revision: 2
created_at: "2026-07-16T04:39:53+09:00"
updated_at: "2026-07-16T04:39:53+09:00"
created_by: agent:codex
updated_by: person:project-owner
related:
  - STATE-SELF-HOSTING-001
  - STATE-PRODUCT-SCOPE-001
  - PROPOSAL-0008
  - CHANGE-0009
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:private-github-request
  approved_subject_revision: 1
  change_record: CHANGE-0009
  approvals:
    - approval_id: APPROVAL-0009
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 1
      decided_at: "2026-07-16T04:39:53+09:00"
      conditions:
        - Make the GitHub Repository private
        - Use tanb as the GitHub owner
change_class: C4
proposed_by: agent:codex
targets:
  - id: STATE-SELF-HOSTING-001
    action: update
    expected_revision: 1
requested_changes:
  - field: knowledge-source
    before:
      status: pending-remote
      url: null
      path: development/knowledge
    after:
      status: active
      url: https://github.com/tanb/dialogue.git
      ref: main
      path: development/knowledge
  - field: source-topology
    before: bootstrap-filesystem
    after: co-located-git
  - field: repository-visibility
    before: not-created
    after: private
reason: Continuously dogfood Knowledge discovery and conversational Decision Capture within Dialogue's own Git workflow
evidence_refs:
  - conversation:private-github-request
  - .knowledge.yml
  - github:tanb/dialogue
impact: Dialogue's code and Knowledge share the same private remote, and Knowledge operations are limited to development/knowledge on main
---

# Enable a co-located Knowledge source on private GitHub

## Decision

The user explicitly stated the policy of using the GitHub `tanb` owner and developing Dialogue as a private Repository. Based on the co-located structure considered immediately beforehand, `development/knowledge/` of the same Repository is adopted as the Knowledge root.
