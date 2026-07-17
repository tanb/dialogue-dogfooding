---
id: CHANGE-0011
type: change_record
title: Fully migrate the verification tools and Product Skill scripts from Ruby to Python
status: applied
scope:
  project: dialogue
  domain: governance
  subject: protocol-conformance
revision: 1
created_at: "2026-07-17T22:55:37+09:00"
updated_at: "2026-07-17T22:55:37+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - CONFORMANCE-001
  - STATE-MVP-GIT-E2E-VALIDATION-001
  - CHANGE-0010
extensions:
  approval_source: direct_user_instruction
  toolchain: python-uv
  change_set_id: CHANGESET-0011
change_class: C3
decision: approved
approvals:
  - approval_id: APPROVAL-0011
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 1
    decided_at: "2026-07-17T22:55:37+09:00"
    conditions: []
    evidence: >-
      Go with option 1. And I would also like to go further and eliminate Ruby completely.
targets:
  - id: CONFORMANCE-001
    action: update
    before_revision: 4
    after_revision: 5
    result: applied
    error: null
  - id: STATE-MVP-GIT-E2E-VALIDATION-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
reason: >-
  To unify the verification stack on Python/uv and secure reproducibility of the
  environment, retire the Ruby verification scripts and Product Skill scripts and
  replace them with the Python reference implementation.
applied_at: "2026-07-17T22:55:37+09:00"
applied_by: agent:claude
---

# Fully migrate the verification tools and Product Skill scripts from Ruby to Python

## Applied changes

- Retired the reference oracle `check-conformance.rb` and made `scripts/check_conformance.py` the sole Conformance runner.
- Ported `validate-repository.rb` to `scripts/validate_repository.py`.
- Rewrote the Product Skill's `scripts/resolve-source` from Ruby to Python (with a PyYAML dependency).
- Consolidated the verification harness onto pytest and removed the Ruby/Python parity tests.
- Removed the Ruby toolchain from CI, adopting a configuration that verifies with uv alone.
- Updated `CONFORMANCE-001` (reference oracle and commands) and `STATE-MVP-GIT-E2E-VALIDATION-001` (test_file and reproduction steps) to the current state.

## Rationale

Git Knowledge Repository discovery via `.knowledge.yml` and Conformance verification are the primary path of Product v1. The Ruby implementation of the verification and scripts did not pin its environment dependencies, so we unify on a policy of guaranteeing reproducibility through a Python environment managed by uv. The Conformance YAML remains a language-neutral contract; only the runner language changes. The meaning of the inputs and the expected results are not weakened.

## Impact

- The repository's dependency on a Ruby runtime disappears, and verification is completed with Python 3 + uv.
- The Product Skill's `resolve-source` requires Python 3 and PyYAML.
- The Conformance cases, the Protocol specification's safety judgments, and the required observed results are unchanged.
