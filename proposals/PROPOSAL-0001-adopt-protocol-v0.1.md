---
id: PROPOSAL-0001
type: proposal
title: Adopt Knowledge Management Protocol v0.1
status: approved
scope:
  project: dialogue
  domain: governance
  subject: protocol-adoption
revision: 2
created_at: "2026-07-16T03:00:14+09:00"
updated_at: "2026-07-16T03:08:48+09:00"
created_by: agent:codex
updated_by: agent:codex
related:
  - PROJECT-CHARTER-001
  - GLOSSARY-001
  - FAILURE-MODEL-001
  - GOVERNANCE-001
  - PROTOCOL-001
  - CONFORMANCE-001
  - AUTHORITY-REGISTRY-001
  - CHANGE-0001
extensions:
  approval_required: true
  approval_record: CHANGE-0001
  approval_source: direct_user_instruction
change_class: C4
proposed_by: agent:codex
targets:
  - id: PROJECT-CHARTER-001
    action: update
    expected_revision: 1
  - id: GLOSSARY-001
    action: update
    expected_revision: 1
  - id: FAILURE-MODEL-001
    action: update
    expected_revision: 1
  - id: GOVERNANCE-001
    action: update
    expected_revision: 1
  - id: PROTOCOL-001
    action: update
    expected_revision: 1
  - id: CONFORMANCE-001
    action: update
    expected_revision: 1
  - id: AUTHORITY-REGISTRY-001
    action: create
    expected_revision: 0
requested_changes:
  - field: PROJECT-CHARTER-001.metadata
    before: legacy
    after: protocol-v0.1
  - field: GLOSSARY-001.metadata
    before: legacy
    after: protocol-v0.1
  - field: FAILURE-MODEL-001.status
    before: draft
    after: active
  - field: GOVERNANCE-001.status
    before: draft
    after: active
  - field: PROTOCOL-001.status
    before: draft
    after: active
  - field: CONFORMANCE-001.status
    before: draft
    after: active
  - field: AUTHORITY-REGISTRY-001
    before: null
    after: active
reason: Establish an implementable Governance, Protocol, and conformance conditions as the operational baseline for the project
evidence_refs:
  - PROJECT-CHARTER-001
  - tests/conformance/cases
  - conversation:current-user-instruction
impact: After approval, Agents and Adapters follow v0.1 authority, the document model, state transitions, safe stops, and the conformance tests
---

# Adopt Knowledge Management Protocol v0.1

## Decision

Adopt v0.1 of Knowledge Governance, the Knowledge Management Protocol, Protocol Conformance, and the Failure Model as the active operational baseline for the Dialogue project.

## Included artifacts

- `docs/failure-model.md`
- `docs/knowledge-governance.md`
- `docs/knowledge-management-protocol.md`
- `docs/protocol-conformance.md`
- `schemas/*.schema.json`
- `tests/conformance/cases/*.yml`
- `scripts/check-conformance.rb`
- `scripts/validate-repository.rb`

## Validation evidence

The nine mandatory cases of the reference oracle pass, and the Schema JSON, local references, document IDs, and Markdown links have been validated.

## Approval

`person:project-owner` approved revision 2 through a direct instruction in the conversation. The application result and the approval record are recorded in `CHANGE-0001`.
