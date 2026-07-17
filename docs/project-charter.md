---
id: PROJECT-CHARTER-001
type: state
title: Dialogue Project Charter
status: active
scope:
  project: dialogue
  domain: governance
  subject: project-charter
revision: 4
created_at: "2026-07-16T00:00:00+09:00"
updated_at: "2026-07-16T04:29:45+09:00"
created_by: agent:codex
updated_by: agent:codex
related:
  - PROPOSAL-0001
  - STATE-PRODUCT-SCOPE-001
  - PROPOSAL-0005
  - CHANGE-0005
  - STATE-SELF-HOSTING-001
  - PROPOSAL-0008
  - CHANGE-0008
canonical_for: dialogue/governance/project-charter
owners:
  - person:project-owner
extensions:
  document_kind: charter
  created_time_precision: date
---

# Dialogue Project Charter

## Purpose

For a project in which multiple humans and multiple AI agents are active at the same time, design a tool-independent Knowledge Governance and Knowledge Management Protocol that can consistently manage the current state, reasons for changes, decision authority, and lifecycle of shared knowledge.

Furthermore, create Agent Skills that correctly execute this protocol on an actual document foundation, making reproducible the exploration, creation, update, change recording, consistency verification, curation, archiving, and escalation to humans of knowledge.

## Problems to solve

- Information is fragmented per working branch, and participants cannot reference the same latest knowledge.
- The same content is duplicated across multiple documents, and it is unclear which is the current source of truth.
- Old descriptions get mixed into search results and are misused as currently valid knowledge.
- Even though the Git diff remains, the reason for a change, the rejected alternatives, the decider, and the impact cannot be traced.
- Simultaneous updates by multiple agents cause semantic conflicts.
- As the number of documents grows, duplication, contradiction, broken references, and knowledge staleness accumulate.
- Operations are closed off per document tool, and agent behavior cannot be ported.

## Basic hypothesis

The center of the problem is not the document storage service but the behavior of the subjects that handle knowledge and the change procedures. Therefore, the meaning and lifecycle of knowledge are defined as a protocol, and storage-specific operations are separated into an adapter or a skill.

The first Product validation concentrates on the flow in which the Git Knowledge Repository is discovered from the project repository's `.dialogue.yml`, and an Agent Skill references and edits it. Actor Identity, Trusted Approval, RAG, and Backends other than Git are extensions after this flow is established.

```text
Knowledge Governance
        ↓
Knowledge Management Protocol
        ↓
Agent Skills
        ↓
Notion | Obsidian | GitHub | Filesystem | Other
```

## Design principles

### 1. Human sovereignty

An agent does not decide a truth that cannot be settled from the basis. When there is a conflict, ambiguity, or lack of authority, it safely stops and presents the judgment material and options to a human.

### 2. State and history separation

Separate the document that represents the currently valid state from the change history document that represents the reason the state changed. The Git commit history can be supporting evidence but is not a substitute for the semantic change history.

### 3. Explicit source of truth

Define the responsibility and priority per document type. Do not manage the same fact independently in multiple places; the non-canonical side references the source of truth.

### 4. Lifecycle over CRUD

Treat knowledge not as simple create, reference, update, delete, but as a lifecycle of proposal, review, approval, activation, consolidation, replacement, deactivation, and archiving.

### 5. Archive is cold knowledge

Archiving is not deletion. It is excluded from ordinary exploration and judgment but is made referenceable in history investigation or an explicit request.

### 6. Continuous curation

Duplication curation is done on a relatively short cycle, and deactivation of old content takes a cycle of roughly one to two months as an initial hypothesis. The cycle is adjusted based on the change frequency and false-detection rate in real operation.

### 7. Retrieval is subordinate

Full-text search, metadata search, RAG, and vector search are means of exploration, not mechanisms that decide truth. A search index is always a derived artifact that can be regenerated from the source of truth.

### 8. Backend portability

Do not make the protocol's conformance depend on the product features of Notion, Obsidian, GitHub, and the like. When the foundation does not have a required capability, absorb the difference with supplementary metadata or an adapter.

### 9. Self-hosting

Use `dialogue-knowledge` in Dialogue's own development, and record decisions that were formed in conversation with the same Protocol. Treat missing records, false detections, conflicts, and operational burden as real-use Evidence for Product improvement.

## Initial deliverables

1. Knowledge Governance specification
   - Roles, authority, deciding subjects, approval, escalation on conflict
2. Knowledge Management Protocol specification
   - Document types, metadata, state transitions, source-of-truth rules, change history, consolidation, archiving
3. Core Agent Skill
   - Foundation-independent exploration, judgment, editing, and verification flow
4. Backend adapters or specialized skills
   - Filesystem/Git as the first reference implementation candidates, verifying portability to other foundations
5. Knowledge Curator workflow
   - Detection of duplication, contradiction, broken references, and staleness, and curation proposals
6. Conformance tests
   - Scenario-based verification that skills and foundations follow the protocol

## Outside initial scope

- Development of a proprietary document SaaS
- A design that makes a vector database the source of truth
- Unconditional automatic approval by agents
- Restoration of decision history using only the Git commit log
- Simultaneous support for all existing document foundations

## Scenarios to validate first

1. An agent can identify the currently valid design and answer with its basis.
2. It can update a state document in line with an approved change and leave an independent change history.
3. When two active documents contradict, it can escalate to a human without choosing arbitrarily.
4. It can detect duplicate descriptions and present a consolidation proposal into the source of truth and the affected scope.
5. It can archive an old document, excluding it from ordinary search while making it referenceable in history investigation.
6. It can execute the same protocol on at least two kinds of document foundations.

## Open design questions

- The minimal set of document types and required metadata
- State transitions and the exploration priority per state
- Whether to record change history per document, per fact, or per change set
- The conflict detection method for simultaneous updates and the necessity of optimistic locking
- A portable evidence format that represents human approval
- Safe thresholds for duplication determination and staleness determination
- The responsibility boundary between the Core Skill and foundation-specific Skills
- The test format for evaluating protocol conformance

## Initial roadmap

1. Create the glossary and the threat/failure model.
2. Define the roles, authority, and decision rules of Governance.
3. Define the document model, state machine, operations, and consistency constraints of the Protocol.
4. Create conformance tests from representative scenarios.
5. Implement reference skills for Filesystem/Git.
6. Evaluate in real use, and port to another document foundation to verify the boundaries.
