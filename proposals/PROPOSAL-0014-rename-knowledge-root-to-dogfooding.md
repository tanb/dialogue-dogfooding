---
id: PROPOSAL-0014
type: proposal
title: Rename the self-hosting Knowledge root to development/dogfooding
status: approved
scope:
  project: dialogue
  domain: development
  subject: self-hosting
revision: 1
created_at: "2026-07-18T01:10:00+09:00"
updated_at: "2026-07-18T01:10:00+09:00"
created_by: agent:claude
updated_by: person:project-owner
related:
  - STATE-SELF-HOSTING-001
  - CHANGE-0014
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:rename-knowledge-root-2026-07-18
  approved_subject_revision: 2
  change_record: CHANGE-0014
  approvals:
    - approval_id: APPROVAL-0014
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 2
      decided_at: "2026-07-18T01:10:00+09:00"
      conditions:
        - Align source.path in .dialogue.yml with development/dogfooding
        - Preserve the old path development/knowledge in historical Proposals/Change Records as a record
change_class: C4
proposed_by: agent:claude
targets:
  - id: STATE-SELF-HOSTING-001
    action: update
    expected_revision: 2
requested_changes:
  - field: knowledge-root-path
    before: development/knowledge
    after: development/dogfooding
  - field: dialogue-yml-source-path
    before: development/knowledge
    after: development/dogfooding
reason: >-
  This directory is the Knowledge root for Dialogue's own self-hosting (dogfooding). Distinguish it from
  the general concept "knowledge" and make it explicit in the name that "this configuration is Dialogue's
  own dogfooding."
evidence_refs:
  - conversation:rename-knowledge-root-2026-07-18
  - .dialogue.yml
  - STATE-SELF-HOSTING-001
impact: >-
  The path of the co-located Knowledge root changes to development/dogfooding, and the source.path in
  .dialogue.yml and the scan path in validate_repository.py follow suit. The domain vocabulary "knowledge"
  stays unchanged; only the path location changes.
---

# Rename the Knowledge root to development/dogfooding

## Decision

The user finalized the policy of renaming the self-hosting Knowledge root directory `development/knowledge` to `development/dogfooding` and aligning `source.path` in `.dialogue.yml` to `development/dogfooding`.

## Rationale

This directory is the concrete embodiment of "dogfooding," where Dialogue's own decisions are managed by Dialogue's protocol. Naming it `dogfooding` clearly distinguishes the general concept "knowledge" (Knowledge Repository / knowledge root) from Dialogue's own self-hosting configuration. The domain vocabulary "knowledge" stays unchanged; the only change is the root location within this repository.

## Approval evidence

- "I want to change the development/knowledge directory to development/dogfooding, and set source.path to development/dogfooding in .dialogue.yml. You can stack it directly onto #11."
