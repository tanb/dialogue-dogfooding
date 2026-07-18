---
id: STATE-PRODUCT-SCOPE-001
type: state
title: Dialogue Product Scope v1
status: active
scope:
  project: dialogue
  domain: product
  subject: product-scope-v1
revision: 5
created_at: "2026-07-16T04:00:43+09:00"
updated_at: "2026-07-18T21:30:00+09:00"
created_by: agent:codex
updated_by: agent:claude
related:
  - PROJECT-CHARTER-001
  - STATE-REFERENCE-IMPLEMENTATION-001
  - PROPOSAL-0005
  - CHANGE-0005
  - PROPOSAL-0007
  - CHANGE-0007
  - PROPOSAL-0013
  - CHANGE-0013
  - PROPOSAL-0015
  - CHANGE-0015
  - PROPOSAL-0021
  - CHANGE-0022
canonical_for: dialogue/product/scope-v1
owners:
  - person:project-owner
extensions:
  document_kind: product-scope
  version: 1
---

# Dialogue Product Scope v1

## Product outcome

Enable an Agent to discover, reference, and edit, in a consistent way, a shared Knowledge Repository that is independent of the project repository.

```text
Project Repository
  └── .dialogue.yml
          ↓
Dialogue Knowledge Skill
          ↓
Knowledge Git Repository
```

## Consumer-facing deliverables

- `.dialogue.yml` v1 Schema
- An adoption `.dialogue.yml` template describing a Git source
- An Agent Skill (`dialogue-knowledge`) that reads `.dialogue.yml` and resolves the Knowledge source
- A history-maintenance Agent Skill (`dialogue-history`) for Change Record Merge and lossless Pack
- The Knowledge Governance and Knowledge Management Protocol

The distribution boundary is declared by `.claude-plugin/` (the plugin manifest). The deliverables are placed under `skills/` (the Agent Skill), `protocol/` (the specification), `schemas/` (the JSON Schema), and `templates/` (the adoption template). Dialogue's own design knowledge, Proposals, and Change Records (`dogfooding/`), the tests (`tests/`), and the validation scripts (`scripts/`) are separated from these as internal assets.

Dialogue can be distributed as a Claude Code plugin via `.claude-plugin/`, and as a copy-based install via `skills.sh` (`npx skills add`).

## `.dialogue.yml` v1 contract

```yaml
version: 1
source:
  type: git
  url: git@github.com:example/project-knowledge.git
  ref: main
  path: .
history:
  pack:
    strategy: none
```

- `type` is only `git` in v1.
- `url` is the remote of the Knowledge Git Repository. Do not include credentials.
- `ref` is a shared branch, tag, or commit, with a default of `main`.
- `path` is the document root within the checkout, with a default of `.`.
- `history.pack` selects the Change Record Pack granularity, chosen at bootstrap: `strategy: none` disables Pack, `time` needs a `period`, `count` needs a `size`. Write an explicit `strategy` rather than omitting it; never write `off` (a YAML 1.1 boolean).
- Reject unknown fields, absolute paths, and paths containing `..`.

## Required user flow

1. The Agent discovers the `.dialogue.yml` at the project root.
2. The Skill validates the configuration and resolves the Git URL, ref, and document root.
3. The Agent fetches or synchronizes a dedicated checkout.
4. It explores the Repository-specific guidance and the current state.
5. It answers questions using the Active source of truth as the basis.
6. For an edit request, it updates the current state and an independent Change Record.
7. On a sync conflict or semantic ambiguity, it does not guess and escalates to a human.

## Initial scope

- Git Knowledge Repository discovery
- Fetch and synchronization of a Git checkout
- Exploration and reference of Markdown knowledge
- Creation and editing of state documents, Proposals, and Change Records
- Basic exploration distinction of Active, Superseded, and Archived
- Human Escalation on duplication or conflict
- Change Record Merge for divergent revisions of the same canonical target
- Lossless Pack of closed change history, with granularity selected via `history.pack`

## Outside initial scope

- Proof of Actor runtime identity
- Making Trusted Approval mandatory
- Cryptographic signing of the Approval Envelope
- Backends other than Git, such as Notion, Obsidian, and Google Drive
- RAG or Vector Database
- A proprietary Document SaaS
- A Filesystem Adapter or a standalone operation CLI

The results of Trusted Approval are not deleted, and are maintained as an optional profile for a Knowledge Repository that explicitly adopts it.
The Filesystem Adapter and CLI created during initial validation are stored in `development/experiments/`, and are not developed further in v1.

## Acceptance criteria

1. A Git source can be deterministically resolved from a valid `.dialogue.yml`.
2. An invalid or unknown configuration can be rejected before connecting to the shared Repository.
3. The Skill does not treat a document inside the code repository as an implicit source of truth.
4. Current knowledge can be searched from the Git Knowledge Repository and answered.
5. A semantic Change Record can be left when editing.
6. The deliverables (`skills/` `protocol/` `schemas/` `templates/`) and the internal assets (`dogfooding/` `scripts/` `tests/`) are separated by directory boundaries, and the distribution boundary is declared by `.claude-plugin/`.
