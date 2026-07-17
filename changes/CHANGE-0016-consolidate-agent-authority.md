---
id: CHANGE-0016
type: change_record
title: Consolidate agent authority into the vendor-neutral AUTH-AGENT-001 and refresh the filesystem wording
status: applied
scope:
  project: dialogue
  domain: "*"
  subject: "*"
revision: 1
created_at: "2026-07-18T03:00:00+09:00"
updated_at: "2026-07-18T03:00:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - PROPOSAL-0016
  - AUTHORITY-REGISTRY-001
extensions:
  approval_source: direct_user_instruction
  operation: change_governance
  change_set_id: CHANGESET-0016
proposal_ref: PROPOSAL-0016
change_class: C4
decision: approved
approvals:
  - approval_id: APPROVAL-0016
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 2
    decided_at: "2026-07-18T03:00:00+09:00"
    conditions:
      - Keep C4 and change_governance exclusive to person:project-owner
      - Retain identity binding IDENTITY-FILESYSTEM-OWNER-001 as a valid local_account binding
    evidence: >-
      Consolidate them (AUTH-AGENT-001, agent:*). I question whether there is any need
      to split CLAUDE and CODEX.
targets:
  - id: AUTHORITY-REGISTRY-001
    action: update
    before_revision: 2
    after_revision: 3
    result: applied
    error: null
reason: >-
  To resolve the Registry's staleness (agent:claude was not registered), consolidate agent
  authority into the vendor-neutral AUTH-AGENT-001 (agent:*), and generalize the wording that
  names the already-deleted Filesystem Adapter.
applied_at: "2026-07-18T03:00:00+09:00"
applied_by: agent:claude
---

# Consolidate agent authority into the vendor-neutral AUTH-AGENT-001

## Applied changes

- Updated `AUTHORITY-REGISTRY-001` from rev2 to rev3 (`change_governance` operation, C4).
- Replaced `AUTH-AGENT-CODEX-001` (actor_ref: agent:codex) with `AUTH-AGENT-001` (actor_ref: `agent:*`). The operations and change_classes (C0–C3) are unchanged, and `delegated_by: AUTH-HUMAN-001` and the condition that C3 requires owner Approval are preserved.
- Added to the conditions: "`agent:*` represents any delegated AI agent, and individual actors are audited via the created_by/applied_by of the Change Record."
- Generalized the body text from "The Filesystem Adapter maps the OS's effective UID as the authenticating principal…" to "the effective UID of the local OS account…". Stated explicitly the human-only nature of `agent:*` and of C4/change_governance.
- Retained the identity binding `IDENTITY-FILESYSTEM-OWNER-001` as a valid local_account binding.

## Rationale

agent:codex and agent:claude are operated with the same authority, and per-vendor authority only increases maintenance cost. Consolidating them into a single vendor-neutral authority removes the need to register future agents, and auditing is guaranteed by the created_by/applied_by of each Change Record. The Filesystem Adapter has been deleted and archived, and naming it had become stale.

## Impact

- The authority of delegated agents (codex, claude, and future implementations) is expressed by the single `AUTH-AGENT-001`.
- C4 and `change_governance` remain exclusive to `person:project-owner`. They are not delegated to agents.
- The Conformance cases are self-contained, each carrying its authorities inline, so they are unaffected by this change.
- The `AUTH-AGENT-CODEX-001` / `agent:codex` within historical Proposals/Change Records are retained as past records.
