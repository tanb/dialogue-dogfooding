---
id: CHANGE-0010
type: change_record
title: Remove the Filesystem Adapter experimental implementation and its tests from the repository
status: applied
scope:
  project: dialogue
  domain: product
  subject: filesystem-reference-implementation
revision: 1
created_at: "2026-07-17T22:55:37+09:00"
updated_at: "2026-07-17T22:55:37+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - STATE-REFERENCE-IMPLEMENTATION-001
  - CHANGE-0007
  - PROPOSAL-0007
extensions:
  approval_source: direct_user_instruction
  product_boundary: git-discovery-skill
  change_set_id: CHANGESET-0010
change_class: C3
decision: approved
approvals:
  - approval_id: APPROVAL-0010
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 1
    decided_at: "2026-07-17T22:55:37+09:00"
    conditions: []
    evidence: >-
      experiments/filesystem-adapter was experimental code, and there was no plan
      at this point to include it in the repository. So it is fine to delete
      experiments/filesystem-adapter. The tests that go with it also become unnecessary.
targets:
  - id: STATE-REFERENCE-IMPLEMENTATION-001
    action: update
    before_revision: 4
    after_revision: 5
    result: applied
    error: null
reason: >-
  The Reference Adapter was experimental code that was never intended to be included
  in the repository from the outset, and it is unnecessary to the primary path of
  Product v1. Delete the implementation, CLI, and dependent tests, and set the State to Archived.
applied_at: "2026-07-17T22:55:37+09:00"
applied_by: agent:claude
---

# Remove the Filesystem Adapter experimental implementation and its tests from the repository

## Applied changes

- Deleted `development/experiments/filesystem-adapter/` (Adapter, CLI, `lib/dialogue/`, Skill wrapper).
- Deleted the dependent tests `filesystem_adapter_test.rb`, `filesystem_cli_test.rb`, `trusted_approval_test.rb`, and `support/filesystem_fixture.rb`.
- Transitioned `STATE-REFERENCE-IMPLEMENTATION-001` from Inactive to Archived, recording that the implementation has been removed.
- Removed the experimental test execution instructions from CI, `AGENTS.md`, and `README.md`.

## Rationale

The Reference Adapter was experimental code that was never intended to be included in the repository from the outset. The primary path of Product v1 is Git Knowledge Repository discovery via `.knowledge.yml`, and the Adapter-specific Protocol Engine is not part of the distribution. The design knowledge the experiment established (canonical-record uniqueness, Lost Update rejection, multi-document transactions, Trusted Approval bindings) is retained as an Archived State in `STATE-REFERENCE-IMPLEMENTATION-001`.

## Impact

- No impact on the primary path of Product v1 or on Conformance verification.
- The main line of verification is consolidated into Protocol Conformance (the parallel Ruby/Python runners) and `.knowledge.yml` resolution, Skill activation, and Git E2E.
- If a deterministic-operation API equivalent to the Adapter becomes necessary for real use in the future, it will be reconsidered as a new implementation, starting from the resumption conditions of the Archived State.
