---
id: AUTHORITY-REGISTRY-001
type: authority_registry
title: Dialogue Authority Registry
status: active
scope:
  project: dialogue
  domain: "*"
  subject: "*"
revision: 3
created_at: "2026-07-16T03:08:48+09:00"
updated_at: "2026-07-18T03:00:00+09:00"
created_by: agent:codex
updated_by: agent:claude
related:
  - PROPOSAL-0001
  - CHANGE-0001
  - PROPOSAL-0004
  - CHANGE-0004
  - PROPOSAL-0016
  - CHANGE-0016
extensions:
  identity_binding_version: 2
registry_for: dialogue
identity_bindings:
  - binding_id: IDENTITY-FILESYSTEM-OWNER-001
    provider: filesystem
    authenticated_id: uid:501
    actor_ref: person:project-owner
    assurance_level: local_account
    valid_from: "2026-07-16T03:38:10+09:00"
    valid_until: null
    status: active
authorities:
  - authority_id: AUTH-HUMAN-001
    actor_ref: person:project-owner
    role: human_authority
    scope:
      project: dialogue
      domain: "*"
      subject: "*"
    operations:
      - read
      - search
      - propose
      - review
      - approve
      - approve_semantic_change
      - resolve_conflict
      - activate
      - supersede
      - deactivate
      - archive
      - restore
      - change_governance
    change_classes: [C0, C1, C2, C3, C4]
    valid_from: "2026-07-16T03:08:48+09:00"
    valid_until: null
    delegated_by: null
    status: active
    conditions: []
  - authority_id: AUTH-AGENT-001
    actor_ref: "agent:*"
    role: agent
    scope:
      project: dialogue
      domain: "*"
      subject: "*"
    operations:
      - read
      - search
      - propose
      - edit_nonsemantic
      - update_state
      - review
      - activate
      - supersede
      - deactivate
      - archive
      - restore
    change_classes: [C0, C1, C2, C3]
    valid_from: "2026-07-18T03:00:00+09:00"
    valid_until: null
    delegated_by: AUTH-HUMAN-001
    status: active
    conditions:
      - Applying C3 requires an Approval by person:project-owner for the target revision
      - "agent:* represents any delegated AI agent (codex, claude, etc.). Individual actors are audited via the created_by/applied_by of the Change Record"
---

# Dialogue Authority Registry

This Registry is the canonical record of the Human Authority and Agent Delegation for the Dialogue project.

`person:project-owner` is a logical Actor representing the project owner. It maps the effective UID of the local OS account as the authenticating subject, and does not treat CLI arguments alone as authentication of the person.

`local_account` does not distinguish between processes running under the same OS account. For operations that require stronger assurance, replace it with a backend session, a signature, or a short-lived capability.

`agent:*` is a single delegated authority representing any delegated AI agent (codex, claude, etc.). Authority is not split per agent implementation; individual actions are audited via the `created_by` / `applied_by` of the Change Record. C4 and `change_governance` are reserved for `person:project-owner` and are not delegated to agents.
