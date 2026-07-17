---
id: PROPOSAL-0005
type: proposal
title: Focus Product v1 on Knowledge Repository discovery
status: approved
scope:
  project: dialogue
  domain: product
  subject: product-scope-v1
revision: 2
created_at: "2026-07-16T04:00:43+09:00"
updated_at: "2026-07-16T04:00:43+09:00"
created_by: agent:codex
updated_by: person:project-owner
related:
  - PROJECT-CHARTER-001
  - STATE-PRODUCT-SCOPE-001
  - STATE-REFERENCE-IMPLEMENTATION-001
  - PROTOCOL-001
  - GOVERNANCE-001
  - CONFORMANCE-001
  - STATE-TRUSTED-APPROVAL-001
  - CHANGE-0005
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:current-user-instruction
  approved_subject_revision: 1
  change_record: CHANGE-0005
  approvals:
    - approval_id: APPROVAL-0005
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 1
      decided_at: "2026-07-16T04:00:43+09:00"
      conditions: []
change_class: C4
proposed_by: agent:codex
targets:
  - id: STATE-PRODUCT-SCOPE-001
    action: create
    expected_revision: 0
  - id: PROJECT-CHARTER-001
    action: update
    expected_revision: 2
  - id: STATE-REFERENCE-IMPLEMENTATION-001
    action: update
    expected_revision: 2
  - id: PROTOCOL-001
    action: update
    expected_revision: 3
  - id: GOVERNANCE-001
    action: update
    expected_revision: 3
  - id: CONFORMANCE-001
    action: update
    expected_revision: 3
  - id: STATE-TRUSTED-APPROVAL-001
    action: update
    expected_revision: 1
requested_changes:
  - field: product-layout
    before: Product and Development assets are mixed at the top level
    after: Separate deliverables into product/ and development assets into development/
  - field: product-discovery
    before: Implicitly assume the location of the Knowledge Repository
    after: Resolve the Git source from the .knowledge.yml at the project root
  - field: trusted-approval-profile
    before: A de facto mandatory requirement of Core Approval
    after: An optional profile that a Knowledge Repository explicitly adopts
reason: Return the first user value to be validated to discovering, referencing, and editing a shared Knowledge Repository
evidence_refs:
  - product/README.md
  - product/config/knowledge.schema.json
  - product/templates/.knowledge.yml
  - product/skills/manage-project-knowledge/SKILL.md
  - development/tests/knowledge_source_test.rb
impact: The product boundary and the MVP path become clear, and actor verification becomes an optional extension that does not obstruct the main line
---

# Focus Product v1 on Knowledge Repository discovery

## Decision

The user explicitly stated the separation of deliverables and development assets, the designation of a Git Knowledge Repository via `.knowledge.yml`, and the lowered priority of actor verification. This judgment is adopted as the scope of Product v1.
