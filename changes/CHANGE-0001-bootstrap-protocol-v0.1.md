---
id: CHANGE-0001
type: change_record
title: Bootstrap Protocol v0.1
status: applied
scope:
  project: dialogue
  domain: governance
  subject: protocol-adoption
revision: 1
created_at: "2026-07-16T03:08:48+09:00"
updated_at: "2026-07-16T03:08:48+09:00"
created_by: agent:codex
updated_by: agent:codex
related:
  - PROPOSAL-0001
  - AUTHORITY-REGISTRY-001
  - PROJECT-CHARTER-001
  - GLOSSARY-001
  - FAILURE-MODEL-001
  - GOVERNANCE-001
  - PROTOCOL-001
  - CONFORMANCE-001
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:current-user-instruction
  bootstrap: true
change_set_id: CHANGESET-0001
proposal_ref: PROPOSAL-0001
change_class: C4
decision: approved
approvals:
  - approval_id: APPROVAL-0001
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 2
    decided_at: "2026-07-16T03:08:48+09:00"
    conditions: []
targets:
  - id: PROPOSAL-0001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: PROJECT-CHARTER-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: GLOSSARY-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: FAILURE-MODEL-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: GOVERNANCE-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: PROTOCOL-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: CONFORMANCE-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: AUTHORITY-REGISTRY-001
    action: create
    before_revision: 0
    after_revision: 1
    result: applied
    error: null
reason: Formally adopt Protocol v0.1 based on the user's direct instruction, and create the first Authority Registry
applied_at: "2026-07-16T03:08:48+09:00"
applied_by: agent:codex
---

# Bootstrap Protocol v0.1

## Before

Governance, Protocol, Failure Model, and Conformance were drafts, and neither the Authority Registry nor a meaningful Change Record existed.

## After

- Normalized the core documents into Protocol-compliant State documents.
- Activated the v0.1 targets.
- Registered `person:project-owner` as the Human Authority.
- Delegated the limited C0–C3 operations to `agent:codex`.

## Decision authority

Recorded the direct instruction of `person:project-owner` as a C4 Approval. The Agent did not approve on their behalf.
