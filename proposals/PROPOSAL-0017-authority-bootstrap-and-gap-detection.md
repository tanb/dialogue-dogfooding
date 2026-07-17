---
id: PROPOSAL-0017
type: proposal
title: Introduce the Authority bootstrap minimum, a safe default for unregistered actors, and Authority gap detection
status: approved
scope:
  project: dialogue
  domain: governance
  subject: knowledge-governance
revision: 1
created_at: "2026-07-18T04:00:00+09:00"
updated_at: "2026-07-18T04:00:00+09:00"
created_by: agent:claude
updated_by: person:project-owner
related:
  - GOVERNANCE-001
  - FAILURE-MODEL-001
  - AUTHORITY-REGISTRY-001
  - CHANGE-0017
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:authority-gap-detection-2026-07-18
  approved_subject_revision: 4
  change_record: CHANGE-0017
  operation: change_governance
  approvals:
    - approval_id: APPROVAL-0017
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 4
      decided_at: "2026-07-18T04:00:00+09:00"
      conditions:
        - Detection ships as a deterministic checker the Skill can run without depending on CI
        - hard is limited to unregistered approvers and fails closed; soft only surfaces for visibility
change_class: C4
proposed_by: agent:claude
targets:
  - id: GOVERNANCE-001
    action: update
    expected_revision: 4
  - id: FAILURE-MODEL-001
    action: update
    expected_revision: 2
requested_changes:
  - field: registry-bootstrap
    before: No minimum-configuration rule (the first creator could create agent authority under a vendor name)
    after: Require Human Authority x1 and a vendor-neutral delegated-agent role (agent:*) x1
  - field: unregistered-actor-default
    before: propose also requires authority (an unregistered actor can do nothing)
    after: read/search/propose are ungated; update_state/approve/applying C1-and-above require authority
  - field: authority-gap-detection
    before: No detection means (missing registrations are invisible)
    after: Define a machine reconciliation of actor vs registry. hard=fail-closed on unregistered approver, soft=visibility. Run via a bundled script
reason: >-
  Because the Registry was first created under the vendor name agent:codex, the judgment problem of whether
  to later register claude arose. Codify a role-based bootstrap minimum, and introduce a safe default for
  unregistered actors and Authority gap detection (a bundled, CI-independent script) so that missing
  registrations are not overlooked.
evidence_refs:
  - conversation:authority-gap-detection-2026-07-18
  - GOVERNANCE-001
  - FAILURE-MODEL-001
impact: >-
  No matter which agents are added going forward, no registration is needed. Unregistered actors can still
  go as far as proposing and the system does not halt, but an unregistered approver for C3/C4 fails closed
  and halts/escalates, while other unregistered cases surface as maintenance items for visibility. Detection
  does not depend on whether the user has CI.
---

# Introduce the Authority bootstrap minimum and Authority gap detection

## Decision

Because the Authority Registry was first created with `agent:codex` (a vendor name), the judgment problem of whether to later register `agent:claude` arose. By the user's judgment, fix the foundations with the following.

1. **Bootstrap minimum**: Every Registry has Human Authority x1 and a vendor-neutral delegated-agent role (`agent:*`, C0-C3, C3 requires human approval, C4 not allowed).
2. **Safe default for unregistered actors**: read/search/propose are ungated; anything beyond that requires authority (fail-closed, but proposing is not blocked).
3. **Authority gap detection**: Machine-reconcile actor vs registry. hard (a C3/C4 approver that is an unregistered Human Authority) fails closed; soft (other unregistered cases) surfaces for visibility. Provided as a **CI-independent bundled script** `skills/dialogue-knowledge/scripts/check-authority`.

## Approval evidence

- "Would it be better to make it explicit to prepare HUMAN and AGENT first? Or are there other processes we could consider?"
- "I think 1 is fine, but if we still cannot detect unregistered actors, forgotten registrations may continue to be overlooked."
- "We don't necessarily know whether a user who used the skill is running CI in that repository." (Making CI-independence a requirement.)
- "A" (finalizing the policy of bundling a deterministic checker).
