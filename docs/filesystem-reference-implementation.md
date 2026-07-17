---
id: STATE-REFERENCE-IMPLEMENTATION-001
type: state
title: Filesystem Reference Adapter Experiment
status: archived
scope:
  project: dialogue
  domain: product
  subject: filesystem-reference-implementation
revision: 5
created_at: "2026-07-16T03:23:25+09:00"
updated_at: "2026-07-17T22:55:37+09:00"
created_by: agent:codex
updated_by: agent:claude
related:
  - PROTOCOL-001
  - GOVERNANCE-001
  - CONFORMANCE-001
  - PROPOSAL-0002
  - CHANGE-0002
  - STATE-TRUSTED-APPROVAL-001
  - PROPOSAL-0004
  - CHANGE-0004
  - STATE-PRODUCT-SCOPE-001
  - PROPOSAL-0005
  - CHANGE-0005
  - PROPOSAL-0007
  - CHANGE-0007
  - CHANGE-0010
canonical_for: dialogue/product/filesystem-reference-implementation
owners:
  - person:project-owner
extensions:
  document_kind: product-component
  version: 0.3.0
  development_status: removed
  product_status: out-of-v1
---

# Filesystem Reference Adapter Experiment

## Current disposition

This experimental implementation was removed from the repository on 2026-07-17 (`CHANGE-0010`). The code, CLI, and API/CLI tests no longer remain in the repository. This State is Archived; it is not selected by an ordinary Resolve and is referenced only for explicit history investigation.

Structure before removal (historical record):

- CLI: `development/experiments/filesystem-adapter/bin/dialogue` (removed)
- Adapter: `development/experiments/filesystem-adapter/adapters/filesystem/lib/dialogue/` (removed)
- API tests: `development/tests/filesystem_adapter_test.rb` (removed)
- CLI tests: `development/tests/filesystem_cli_test.rb` (removed)

This implementation was not a distribution target for Product v1. The primary flow for Product v1 is one in which `product/skills/manage-project-knowledge/` discovers the Git Knowledge Repository from `.knowledge.yml` and references and edits it using standard Git and file operations. The following design findings are retained as a starting point for a future re-examination of an Adapter-equivalent deterministic operation API.

## Supported workflow

```text
.knowledge.yml → Git checkout → Resolve → Edit → Change Record → Validate
```

For a Repository that has adopted Trusted Approval, add Proposal → Human Approval → Apply.

CLI commands:

```text
dialogue resolve
dialogue list
dialogue propose
dialogue approve
dialogue apply
dialogue validate
```

Archive, Restore, Supersede, and Deactivate are Applied through the target action and status change of a Proposal.

## Core guarantees

- Verifies the uniqueness of the Active `canonical_for`.
- Rejects a Lost Update via `expected_revision`.
- Creates a recovery transaction marker before writing multiple documents.
- Rolls back the State, Proposal, and Change Record together on a verification failure.
- Does not treat an in-document instruction as Agent authority.

## Optional Trusted Approval profile

Only for a Repository that has adopted it, the following are guaranteed.

- Separates Human Approval and Agent Delegation in the Authority Registry.
- Binds Human Approval to the OS Identity, Proposal ID, revision, and SHA-256 Digest.
- Rejects an expired Approval, revoked authority, diversion to a different Proposal, and reuse.

## Current limits

- Existing documents can change only the top-level front matter.
- New documents can be created with metadata and body together.
- The Identity guarantee of Human Approval is at the `local_account` level of the OS effective UID, and does not distinguish processes with the same UID.
- The `--actor` of an Agent Apply is a Delegation identifier and does not prove runtime identity.
- Recovery after a process crash is performed when the next CLI operation is executed on the same shared Filesystem.
- It does not provide a distributed Lock across multiple hosts.

A Production Adapter that implements the Trusted Approval profile must map the Backend's authenticated user ID to an Actor reference and store the Identity Evidence in the Approval Envelope.

## Resume criteria

- Atomicity or recovery processing of multi-document updates becomes necessary in real use.
- The common operations are ported to a Backend other than Git.
- The same deterministic operation API is used from multiple Agent runtimes.

## Validation

Because the implementation and tests have been removed, there is no execution verification corresponding to this State. For the verification procedure of the entire repository, see Development validation in `README.md`.
