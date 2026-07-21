---
id: CHANGE-0024
type: change_record
title: Adopt agent confidentiality boundary handling as a mandatory skill practice
status: applied
scope:
  project: dialogue
  domain: governance
  subject: confidentiality-boundary
revision: 1
created_at: "2026-07-21T12:00:00+09:00"
updated_at: "2026-07-21T12:00:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - PROPOSAL-0024
  - STATE-CONFIDENTIALITY-BOUNDARY-001
  - FAILURE-MODEL-001
  - GLOSSARY-001
  - GOVERNANCE-001
extensions:
  approval_source: direct_user_instruction
  operation: change_governance
  change_set_id: CHANGESET-0024
proposal_ref: PROPOSAL-0024
change_class: C4
decision: approved
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
    evidence: >-
      Selection of perspective A to draft into the Skill and record in the Knowledge Repository, then
      approval of the change set and design decisions with the instruction to proceed ("おねがいします").
targets:
  - id: STATE-CONFIDENTIALITY-BOUNDARY-001
    action: create
    before_revision: 0
    after_revision: 1
    result: applied
    error: null
  - id: FAILURE-MODEL-001
    action: update
    before_revision: 3
    after_revision: 4
    result: applied
    error: null
  - id: GLOSSARY-001
    action: update
    before_revision: 3
    after_revision: 4
    result: applied
    error: null
reason: >-
  Codify confidentiality handling as a non-delegable agent practice in the distributed Skill, separate from
  the document-system's enforcement of access control, encryption, and retention. The agent observes and
  respects the boundary and must not become the leak path through chat, provenance fields, or Derived
  Artifacts.
applied_at: "2026-07-21T12:00:00+09:00"
applied_by: agent:claude
---

# Adopt agent confidentiality boundary handling as a mandatory skill practice

## Applied changes

### Governance state (this Knowledge Repository)
- `STATE-CONFIDENTIALITY-BOUNDARY-001` (new): the canonical confidentiality-boundary policy — a Backend-enforces / agent-observes division of responsibility, the five-point boundary practice, the no-bundled-checker rationale, and the optional `sensitivity` seam.
- `FAILURE-MODEL-001` rev3→4: added F17 (Confidential exposure through the agent) and linked the new State and this change set.
- `GLOSSARY-001` rev3→4: added Confidential Content, PII, Sensitivity Label, Need-to-know, and Redaction under a new Confidentiality section.

### Product deliverables (distribution — dialogue PR, branch tanb/agent-confidentiality-boundary)
- `skills/dialogue-knowledge/SKILL.md`: new "Handle confidential knowledge at the boundary" section between "Read project knowledge" and "Edit project knowledge" — classify before use, apply need-to-know, never copy secrets into governed or derived fields, redact, escalate on uncertainty; states that access control, encryption, and retention remain Backend responsibilities and that no checker is bundled.

## Rationale

Separating what the agent must practice from what the document system (Git/GitHub, later Notion) must govern exposed a gap a robust Backend cannot close on its own: the agent emits text into chat, summaries, Derived Artifacts, and the provenance fields of governed documents — output paths outside Backend control. Confidentiality handling is therefore a non-delegable agent responsibility and belongs in the distributed Skill. This mirrors the maintenance-cycle precedent (CHANGE-0020) of moving a mandatory practice into the Skill, but deliberately ships no checker: mechanical PII or secret detection is heuristic and a "clean" result would create false assurance.

## Impact

- A Knowledge Repository the Skill manages gains a mandatory confidentiality practice that works today without a schema change, falling back to conservative content-based judgment when no sensitivity label is declared.
- Adding an optional `extensions.sensitivity` label to the managed-document schema is a forward-compatible enhancement (the deferred seam), not a precondition.
- No deterministic checker is bundled, so the practice does not create false assurance from heuristic detection; F17 detection is a behavioral obligation of the agent.
- Access control, encryption at rest, and retention/disposition execution remain Backend and Adapter responsibilities and are unchanged.
