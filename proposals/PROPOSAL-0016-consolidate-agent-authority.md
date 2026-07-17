---
id: PROPOSAL-0016
type: proposal
title: Consolidate agent authority into the vendor-neutral AUTH-AGENT-001 and refresh the filesystem wording
status: approved
scope:
  project: dialogue
  domain: "*"
  subject: "*"
revision: 1
created_at: "2026-07-18T03:00:00+09:00"
updated_at: "2026-07-18T03:00:00+09:00"
created_by: agent:claude
updated_by: person:project-owner
related:
  - AUTHORITY-REGISTRY-001
  - CHANGE-0016
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:refresh-authority-registry-2026-07-18
  approved_subject_revision: 2
  change_record: CHANGE-0016
  operation: change_governance
  approvals:
    - approval_id: APPROVAL-0016
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 2
      decided_at: "2026-07-18T03:00:00+09:00"
      conditions:
        - Keep C4 and change_governance reserved to person:project-owner
        - Keep identity binding IDENTITY-FILESYSTEM-OWNER-001 as a valid local_account binding
change_class: C4
proposed_by: agent:claude
targets:
  - id: AUTHORITY-REGISTRY-001
    action: update
    expected_revision: 2
requested_changes:
  - field: agent-authority
    before:
      authority_id: AUTH-AGENT-CODEX-001
      actor_ref: agent:codex
    after:
      authority_id: AUTH-AGENT-001
      actor_ref: "agent:*"
      change_classes: [C0, C1, C2, C3]
  - field: identity-prose
    before: The Filesystem Adapter maps the OS effective UID as the authentication subject
    after: Map the effective UID of the local OS account as the authentication subject
reason: >-
  agent:codex and agent:claude operate with identical authority (operations and C0-C3), so there is little
  practical benefit to splitting them by vendor. Consolidate them into a single vendor-neutral delegated
  authority AUTH-AGENT-001 (actor_ref: agent:*), making registration unnecessary when future agents are
  added. At the same time, generalize the stale identity-authentication wording that names the already-removed
  Filesystem Adapter.
evidence_refs:
  - conversation:refresh-authority-registry-2026-07-18
  - AUTHORITY-REGISTRY-001
impact: >-
  Delegated-agent authority is expressed by the single authority actor_ref: agent:*. Auditing is ensured by
  the created_by/applied_by of each Change Record. C4 and change_governance remain human-only and unchanged.
  The identity binding is preserved.
---

# Consolidate agent authority into the vendor-neutral AUTH-AGENT-001

## Decision

`AUTHORITY-REGISTRY-001` had gone stale. `agent:claude` created and applied numerous Proposals / Change Records (C3 and C4) in this session, but the Registry only had `AUTH-AGENT-CODEX-001` (agent:codex) registered.

By the judgment of the user (person:project-owner), rather than splitting by vendor, consolidate into a single vendor-neutral delegated authority.

- `AUTH-AGENT-CODEX-001` (agent:codex) → `AUTH-AGENT-001` (`actor_ref: agent:*`, role:agent, identical operations, change_classes C0-C3, delegated_by AUTH-HUMAN-001, C3 requires owner Approval)
- Generalize the identity-authentication wording that names the already-removed Filesystem Adapter to "the effective UID of the local OS account"
- C4 and `change_governance` remain reserved to `person:project-owner`

## Approval evidence

- "AUTHORITY-REGISTRY-001.md has gone stale. Please fix it using the dialogue-knowledge skill."
- "I question whether we need to split CLAUDE and CODEX."
- "Consolidate (AUTH-AGENT-001, agent:*)" "Fix together" (finalizing D1-redo / D2).
