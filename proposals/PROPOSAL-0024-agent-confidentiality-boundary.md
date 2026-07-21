---
id: PROPOSAL-0024
type: proposal
title: Adopt agent confidentiality boundary handling as a mandatory skill practice
status: approved
scope:
  project: dialogue
  domain: governance
  subject: confidentiality-boundary
revision: 1
created_at: "2026-07-21T12:00:00+09:00"
updated_at: "2026-07-21T12:00:00+09:00"
created_by: agent:claude
updated_by: person:project-owner
related:
  - GOVERNANCE-001
  - GLOSSARY-001
  - FAILURE-MODEL-001
  - STATE-CONFIDENTIALITY-BOUNDARY-001
  - CHANGE-0024
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:agent-confidentiality-boundary-2026-07-21
  change_record: CHANGE-0024
  operation: change_governance
  approvals:
    - approval_id: APPROVAL-0024
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 0
      decided_at: "2026-07-21T12:00:00+09:00"
      conditions:
        - Separate the agent's practice from Backend/document-system governance; the agent observes and respects, never enforces or circumvents
        - Function today without a schema change; treat the sensitivity label as an optional, forward-compatible seam
        - Ship no bundled checker, because mechanical PII or secret detection is heuristic and would create false assurance
change_class: C4
proposed_by: agent:claude
targets:
  - id: STATE-CONFIDENTIALITY-BOUNDARY-001
    action: create
    expected_revision: 0
  - id: FAILURE-MODEL-001
    action: update
    expected_revision: 3
  - id: GLOSSARY-001
    action: update
    expected_revision: 3
requested_changes:
  - field: confidentiality-practice
    before: The Skill had no practice for confidential content. The principle that confidential info is passed to the agent only after confirming read scope lived only in the Protocol Conformance spec, never operationalized in the distributed Skill, and provenance/derived output paths were unaddressed
    after: Adopt a mandatory "Handle confidential knowledge at the boundary" practice in the distributed dialogue-knowledge Skill, backed by a canonical State document, so the agent classifies, applies need-to-know, never transcribes secrets into governed or derived fields, redacts, and escalates on uncertainty
  - field: failure-model
    before: The failure model covered instruction injection (F13), retrieval omission (F14), and authority gaps (F16), but had no failure for the agent itself exposing confidential content
    after: Add F17 (Confidential exposure through the agent), covering exposure beyond the authorized audience and leakage into broadly readable provenance or derived fields, with a behavioral (not mechanical) detection obligation
  - field: glossary
    before: The glossary had no confidentiality vocabulary
    after: Add Confidential Content, PII, Sensitivity Label, Need-to-know, and Redaction, aligned with the new State and F17
reason: >-
  Separating what the agent must practice from what the document-system (Git/GitHub, later Notion) must
  govern showed a real gap: even a robust Backend cannot close it, because the agent emits text into chat,
  summaries, Derived Artifacts, and the provenance fields of governed documents — paths the Backend does
  not control. Confidentiality handling is therefore a non-delegable agent responsibility and must live in
  the distributed Skill, mirroring the maintenance-cycle precedent (CHANGE-0020) but, unlike it, without a
  bundled checker.
evidence_refs:
  - conversation:agent-confidentiality-boundary-2026-07-21
  - GOVERNANCE-001
  - FAILURE-MODEL-001
impact: >-
  Any Knowledge Repository the Skill manages gains a mandatory confidentiality practice that works today
  without a schema change, falling back to conservative content-based judgment when no sensitivity label is
  declared. Adding an optional extensions.sensitivity label is a forward-compatible enhancement (the
  deferred schema seam), not a precondition. No deterministic checker is bundled, so the practice does not
  create false assurance from heuristic detection.
---

# Adopt agent confidentiality boundary handling as a mandatory skill practice

## Decision

By the user's judgment, the agent's confidentiality handling is separated from the document-system's governance and adopted as a mandatory practice of the distributed `dialogue-knowledge` Skill.

1. **Skill practice**: Add "Handle confidential knowledge at the boundary" to the distributed Skill — classify before use, apply need-to-know, never copy secrets into governed or derived fields, redact, and escalate on uncertainty.
2. **Canonical state**: Record the policy as `STATE-CONFIDENTIALITY-BOUNDARY-001`, framing it as a Backend-enforces / agent-observes division of responsibility.
3. **Failure model**: Add `FAILURE-MODEL-001` F17 (Confidential exposure through the agent).
4. **Glossary**: Add Confidential Content, PII, Sensitivity Label, Need-to-know, and Redaction.

The `sensitivity` label is an optional, forward-compatible seam; the practice works today by falling back to content-based judgment. No deterministic checker is bundled, unlike the maintenance cycle and authority gap detection.

## Approval evidence

- Selection of perspective A (confidentiality boundary handling) as the item to draft into the Skill and record in the Knowledge Repository, in a conversation that first separated agent practice from document-system governance.
- Approval of the proposed change set and design decisions (no mandatory schema change; no bundled checker) with the instruction to proceed ("おねがいします").
