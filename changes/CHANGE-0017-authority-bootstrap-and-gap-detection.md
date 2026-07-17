---
id: CHANGE-0017
type: change_record
title: Introduce an Authority bootstrap minimum configuration, a safe default for unregistered actors, and Authority gap detection
status: applied
scope:
  project: dialogue
  domain: governance
  subject: knowledge-governance
revision: 1
created_at: "2026-07-18T04:00:00+09:00"
updated_at: "2026-07-18T04:00:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - PROPOSAL-0017
  - GOVERNANCE-001
  - FAILURE-MODEL-001
  - AUTHORITY-REGISTRY-001
extensions:
  approval_source: direct_user_instruction
  operation: change_governance
  change_set_id: CHANGESET-0017
proposal_ref: PROPOSAL-0017
change_class: C4
decision: approved
approvals:
  - approval_id: APPROVAL-0017
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 4
    decided_at: "2026-07-18T04:00:00+09:00"
    conditions:
      - Bundle detection as a deterministic checker that the Skill can run without depending on CI
      - Limit hard to unregistered approvers and fail-closed; keep soft to visibility only
    evidence: >-
      A (bundle the deterministic checker). We cannot know whether a user who uses the
      skill is necessarily running CI in that repository.
targets:
  - id: GOVERNANCE-001
    action: update
    before_revision: 4
    after_revision: 5
    result: applied
    error: null
  - id: FAILURE-MODEL-001
    action: update
    before_revision: 2
    after_revision: 3
    result: applied
    error: null
reason: >-
  Introduce a role-based bootstrap minimum configuration, a safe default for unregistered actors,
  and CI-independent Authority gap detection, to resolve the judgment problem that granting agent
  authority by vendor name creates and the invisibility of missing registrations.
applied_at: "2026-07-18T04:00:00+09:00"
applied_by: agent:claude
---

# Introduce an Authority bootstrap minimum configuration and Authority gap detection

## Applied changes

### Protocol / Failure model
- `GOVERNANCE-001` rev4→5: added §5.1 Bootstrap minimum configuration (Human + `agent:*`), §5.2 Safe default for unregistered actors (read/search/propose are ungated), and §5.3 Authority gap detection (hard = fail-closed when an approver is unregistered, soft = visibility, CI-independent).
- `FAILURE-MODEL-001` rev2→3: added `F16. Authority gap (unregistered actor)`.

### Product deliverables (distribution)
- `skills/dialogue-knowledge/scripts/check-authority` (new): a deterministic checker that machine-reconciles actor ↔ registry. Exit 2 on a hard gap (fail-closed), lists soft gaps. PyYAML dependency, CI-independent.
- `skills/dialogue-knowledge/SKILL.md`: added the Registry bootstrap steps and a "Reconcile authority" procedure (run the checker; hard = stop and escalate; soft = maintenance item).
- `templates/authority-registry.md` (new): a default Registry template holding Human + `agent:*`.

### Internal (dogfooding)
- `scripts/validate_repository.py`: added `validate_authority()`, which runs the bundled checker against its own `dogfooding/` (verification fails on a hard gap).
- `tests/test_authority_check.py` (new): pins the four contracts of clean / hard (unregistered C4 approver) / agent:* coverage / soft. Added the `CHECKER` path to `tests/dialogue_support.py`.

## Rationale

Because the Registry was first created with the vendor name `agent:codex`, a judgment problem arose over registering new agents. Binding authority to a role (`agent:*`) with a bootstrap minimum configuration resolves this permanently. Since a safe default alone leaves missing registrations invisible, detection is normalized and provided as a Skill-bundled deterministic checker so that it does not depend on whether the user has CI.

## Impact

- Adding a new agent requires no Registry registration.
- Unregistered actors can go as far as proposing (the system does not stop). An unregistered C3/C4 approver stops fail-closed, and other unregistered cases are made visible.
- Detection can be run by anyone with `python3 skills/dialogue-knowledge/scripts/check-authority --document-root <root>`, independent of CI.
- The Conformance cases are self-contained, so they are unaffected. The `agent:codex` and similar in historical records are retained.
