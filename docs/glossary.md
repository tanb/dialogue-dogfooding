---
id: GLOSSARY-001
type: state
title: Dialogue Glossary
status: active
scope:
  project: dialogue
  domain: governance
  subject: glossary
revision: 4
created_at: "2026-07-16T00:00:00+09:00"
updated_at: "2026-07-21T12:00:00+09:00"
created_by: agent:codex
updated_by: agent:claude
related:
  - PROPOSAL-0001
  - PROPOSAL-0020
  - CHANGE-0020
  - STATE-MAINTENANCE-CYCLE-001
  - PROPOSAL-0024
  - CHANGE-0024
  - STATE-CONFIDENTIALITY-BOUNDARY-001
canonical_for: dialogue/governance/glossary
owners:
  - person:project-owner
extensions:
  document_kind: reference
  created_time_precision: date
---

# Dialogue Glossary

## Normative terms

In this project's specifications, the following terms are used with normative strength.

- **MUST (required)**: A requirement that a conforming implementation or operation always satisfies
- **MUST NOT (prohibited)**: Something that a conforming implementation or operation must not do
- **SHOULD (recommended)**: A requirement that may be deviated from only with a legitimate reason, which can be explained
- **SHOULD NOT (not recommended)**: Something that may be done only with a legitimate reason, which can be explained
- **MAY (optional)**: Something that an implementation or operation may choose

Even when written in English alone, the contextual strength follows the normative term in parentheses.

## Knowledge model

### Knowledge

Meaningful information used for the judgment or action of project participants. It is not merely stored text; it carries an applicable scope, state, basis, and responsible subject.

### Knowledge Item

The smallest managed unit of knowledge that can be independently identified, referenced, and state-managed. In implementation, it can be a single document, a single page, or a structured section within a document.

### Claim

A single statement whose truth or validity can be evaluated. The same Knowledge Item may contain multiple Claims.

### Fact

A Claim that can be confirmed by observation or a trustworthy basis. Future plans, proposals, preferences, and unapproved judgments are not called Facts.

### Decision

A policy that a human with authority has settled by adopting it from among multiple possibilities. A Decision differs from a fact, but after approval it can become normative knowledge of the project.

### Evidence

Referenceable information that supports a Claim, change, or state determination. It includes source code, approval records, measurement results, contracts, and external specifications.

### Provenance

Information that allows tracing by whom, when, and through which basis or change a piece of knowledge was created.

## Roles of documents

### State Document

A document that describes the currently valid state of a target. In principle it is an update type, and does not accumulate the entire past history into its body.

### Change Record

An independent document that records, for a semantic change of knowledge, the before, after, reason, basis, impact, and deciding subject. It is a protocol artifact separate from the Git commit history.

### Proposal

A change candidate that has not yet been approved. A Proposal is not treated as the source of truth for the current state.

### Source of Truth

The Knowledge Item that is referenced first when judging the current state for a specific target and applicable scope. Being the source of truth must be determinable by an explicit rule or metadata.

### Derived Artifact

A summary, search index, Embedding, cache, dashboard, and the like that can be regenerated from the source of truth. A derived artifact must not be made the source of truth on its own.

## States

### Draft

A state that is in the middle of creation and is not yet the target of review or approval.

### Proposed

A state that has been presented as a change candidate and is awaiting a judgment.

### Active

A state that is normally used for current judgment and action within a defined applicable scope.

### Superseded

A state whose role has been replaced by a successor Knowledge Item. It must hold a reference to the successor.

### Inactive

A state that is not used for current ordinary work but is not yet fixed as a historical resource. It can be the target of re-evaluation or re-activation.

### Archived

Cold Knowledge that has been excluded from ordinary retrieval and judgment. It does not mean deleted, and can be referenced in an explicit history investigation.

### Rejected

A state in which a proposal was not adopted. It is not used as the current state and is used for investigating the rejection reason.

### Approved

A state in which a human with authority has approved a Proposal or Change Record, but it does not yet mean that application to the target State Document is complete.

### Applied

A state in which an approved Change Set has been reflected onto the target and verification of the post-conditions is also complete.

### Withdrawn

A state in which the proposer or an Actor with authority has withdrawn a Proposal before a judgment. It is distinguished from rejection.

### Failed

A state in which the application or post-verification of a Change Set did not complete, and recovery or a human judgment is required.

## Consistency

### Duplicate

A state in which the same Claim is maintained independently in multiple places. A mere citation or a reference to the source of truth is not regarded as a duplicate.

### Conflict

A state in which, for the same target and applicable scope, multiple Claims that cannot hold simultaneously exist as valid candidates.

### Ambiguity

A state in which, with only the available information, the target, meaning, state, applicable scope, or priority cannot be uniquely settled.

### Staleness

A state in which there is reasonable doubt about the current validity of a Knowledge Item due to the passage of time or changes in surrounding circumstances. Being old alone is not a determining condition of Staleness.

### Knowledge Drift

The phenomenon in which the content of the source of truth, implementation, operation, and derived artifacts diverges over time.

### Broken Reference

A state in which the target referenced by a Knowledge Item cannot be resolved, or does not match the intended target.

## Subjects and authority

### Actor

A human, agent, or automated process that performs an operation on the protocol.

### Human Authority

A human who holds the final decision-making power over semantic changes, conflict resolution, and exception approval within a defined scope.

### Knowledge Steward

A human who manages the operation of the knowledge structure, quality, lifecycle, and source-of-truth rules. May be the same person as the Human Authority.

### Agent

An AI subject that, following the granted authority and skills, performs retrieval, proposal, update, verification, and curation of knowledge. Its authority is determined by explicit delegation, not by capability.

### Knowledge Curator

A role that detects the six maintenance targets — duplication, conflict, broken references, staleness, missing Change Records, and derived-artifact drift — and proposes consolidation, re-validation, or state changes. An agent or a human can take charge of it. Detection is provided as a bundled, CI-independent deterministic checker (`skills/dialogue-knowledge/scripts/check-maintenance`); see `STATE-MAINTENANCE-CYCLE-001`.

### Approval

The act by which a human with authority permits, in an identifiable form, the target, change content, and applicable scope.

### Delegation

The Human Authority granting authority to another Actor for limited operations, targets, periods, and conditions.

### Escalation

The procedure in which an agent judges that it cannot safely continue processing and asks the Human Authority for a decision, attaching the basis, conflict, impact, and options.

## Confidentiality

### Confidential Content

Content whose disclosure must be limited: a secret, a credential, or PII. It may appear inside any Knowledge Item. The Backend enforces its access control; the agent must not carry it outside that boundary through chat, provenance fields, or Derived Artifacts. See `STATE-CONFIDENTIALITY-BOUNDARY-001`.

### PII (Personally Identifiable Information)

Information that identifies a specific individual on its own or in combination — for example a name, contact detail, government or account identifier, or health and financial data. A category of Confidential Content.

### Sensitivity Label

A machine-readable signal on a Knowledge Item (for example `extensions.sensitivity` of `public`, `internal`, or `confidential`) that declares its handling class. It is the seam between Backend enforcement and agent observation. It is optional: when absent, the agent judges sensitivity conservatively from content.

### Need-to-know

The rule that Confidential Content is surfaced only to the audience and scope a task actually requires, not to everyone technically able to read it.

### Redaction

Removing or masking confidential values from a summary, a Derived Artifact, or a governed field while keeping a pointer to the source of truth, so the record remains useful without carrying the confidential value.

## Foundation

### Knowledge Backend

A service or medium that stores, retrieves, and updates Knowledge Items. It includes Notion, Obsidian, GitHub, a filesystem, and so on.

### Adapter

An implementation that translates the common operations on the protocol into the operations of a specific Knowledge Backend.

### Repository

A logical storage area that manages Knowledge Items as a set. It is not limited to a Git repository.

### Retrieval Index

Derived data that speeds up full-text search, metadata search, vector search, and the like. For the final determination of current validity and authority, the source of truth is re-confirmed.
