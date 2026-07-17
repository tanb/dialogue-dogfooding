---
id: CHANGE-0004
type: change_record
title: Adopt Trusted Approval v0.2
status: applied
scope:
  project: dialogue
  domain: governance
  subject: trusted-approval
revision: 1
created_at: "2026-07-16T03:38:10+09:00"
updated_at: "2026-07-16T03:38:10+09:00"
created_by: agent:codex
updated_by: agent:codex
related:
  - PROPOSAL-0004
  - STATE-TRUSTED-APPROVAL-001
  - AUTHORITY-REGISTRY-001
  - PROTOCOL-001
  - GOVERNANCE-001
  - CONFORMANCE-001
  - STATE-REFERENCE-IMPLEMENTATION-001
extensions:
  adapter: manual-filesystem
  approval_source: direct_user_instruction
  approval_format: v0.1-bootstrap
  validation_cases: 13
change_set_id: CHANGESET-0004
proposal_ref: PROPOSAL-0004
change_class: C4
decision: approved
approvals:
  - approval_id: APPROVAL-0004
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 1
    decided_at: "2026-07-16T03:38:10+09:00"
    conditions: []
targets:
  - id: PROPOSAL-0004
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: STATE-TRUSTED-APPROVAL-001
    action: create
    before_revision: 0
    after_revision: 1
    result: applied
    error: null
  - id: AUTHORITY-REGISTRY-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: PROTOCOL-001
    action: update
    before_revision: 2
    after_revision: 3
    result: applied
    error: null
  - id: GOVERNANCE-001
    action: update
    before_revision: 2
    after_revision: 3
    result: applied
    error: null
  - id: CONFORMANCE-001
    action: update
    before_revision: 2
    after_revision: 3
    result: applied
    error: null
  - id: STATE-REFERENCE-IMPLEMENTATION-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
reason: Prevent impersonation of Human Approval, post-approval tampering, reuse for a different Proposal, and the use of expired or revoked approvals
applied_at: "2026-07-16T03:38:10+09:00"
applied_by: agent:codex
---

# Adopt Trusted Approval v0.2

## Applied changes

- Added an Identity Resolver that resolves the OS effective UID to a logical Human Actor.
- Fixed the approval subject of a Proposal to a canonical JSON and a SHA-256 Digest.
- Added the Subject ID, revision, Digest, expiration, and Identity Evidence to the Approval Envelope.
- Verified tampering, reuse for another Proposal, replay, expiration, and Identity/Authority revocation at Apply time.
- Removed the self-declared `--actor` from the Human Approval CLI.
- Synced the Core Skill, Schema, Authority Registry, and reference implementation documents to v0.2.

## Verification evidence

```text
13 conformance cases passed
FilesystemAdapterTest: 8 runs, 41 assertions, 0 failures, 0 errors
FilesystemCliTest: 4 runs, 24 assertions, 0 failures, 0 errors
TrustedApprovalTest: 7 runs, 31 assertions, 0 failures, 0 errors
```

## Residual limits

- `local_account` does not distinguish between multiple processes running under the same OS UID.
- The `--actor` of Agent Apply is a Delegation identifier, not proof of the Agent runtime identity.
- The Approval Envelope is not signed within the reference implementation. Strong tamper resistance requires a Backend audit or signing.
