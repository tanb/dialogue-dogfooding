---
id: STATE-CONFIDENTIALITY-BOUNDARY-001
type: state
title: Agent Confidentiality Boundary Handling
status: active
scope:
  project: dialogue
  domain: governance
  subject: confidentiality-boundary
revision: 1
created_at: "2026-07-21T12:00:00+09:00"
updated_at: "2026-07-21T12:00:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - GOVERNANCE-001
  - GLOSSARY-001
  - FAILURE-MODEL-001
  - PROPOSAL-0024
  - CHANGE-0024
canonical_for: dialogue/governance/confidentiality-boundary
owners:
  - person:project-owner
extensions:
  document_kind: operating-policy
  activation_status: active
---

# Agent Confidentiality Boundary Handling

## Decision

Shared knowledge may hold confidential content — secrets, credentials, or PII (personally identifiable information such as names, contact details, identifiers, or health and financial data). Access control, encryption at rest, and retention are enforced by the Knowledge Backend and Adapter. The agent has a **separate, non-delegable responsibility**: it must not become the path that carries confidential content outside that boundary.

This is a division of responsibility, not a duplication. The Backend **enforces** the boundary; the agent **observes and respects** it and must never enforce it itself nor work around it. A robust Backend cannot close this gap on its own, because the agent emits text into chat, summaries, Derived Artifacts, and the provenance fields of governed documents — output paths the Backend does not control.

## Boundary practice

The distributed `dialogue-knowledge` Skill carries this as a mandatory behavioral practice ("Handle confidential knowledge at the boundary"):

1. **Classify before use.** If a Knowledge Item declares a sensitivity label (for example `extensions.sensitivity` of `public`, `internal`, or `confidential`), treat that label as its handling class. If no label is declared, judge conservatively from content: treat anything containing a secret or PII as confidential.
2. **Need-to-know before presenting.** Do not surface confidential content beyond the audience and scope the task requires. Confirm the actor's read scope before quoting it. If the Backend denies the read, do not seek an alternate path; escalate.
3. **Never copy secrets into new records.** Do not transcribe PII or secrets into a Change Record `reason`, a Proposal's evidence, a commit message, or any other governed or derived field. Reference the confidential source by id or pointer, never by value. Provenance fields are broadly readable and are a common leak path.
4. **Redact in summaries and derived artifacts.** When summarizing confidential knowledge or generating a Derived Artifact (index, cache, summary), redact the confidential values and keep only the pointer to the source of truth.
5. **Escalate on uncertainty.** If it cannot be determined whether content is confidential, or whether the audience is authorized, stop and escalate rather than guess. An operation that may affect privacy or confidentiality is an escalation condition (`FAILURE-MODEL-001` F17).

## No mechanical checker

Unlike the maintenance cycle (`STATE-MAINTENANCE-CYCLE-001`) and Authority gap detection, confidentiality handling ships **without** a bundled deterministic checker. Mechanical PII or secret detection is heuristic: it produces both false negatives (missed secrets) and false positives, and a checker that reports "clean" would create false assurance that undermines the practice. Detection here is a behavioral obligation of the agent, consistent with the principle that a bundled checker reports only mechanically decidable candidates and never fabricates a semantic verdict.

## Relationship to the Backend

- Access control, encryption at rest, availability, and retention/disposition **execution** remain Backend and Adapter responsibilities. The agent does not re-implement them.
- The seam between the two planes is a machine-readable signal the Backend may expose and the agent observes — a `sensitivity` label is the first such signal. Adding it to the managed-document schema is an **optional, forward-compatible** enhancement; this practice functions today without it by falling back to conservative content-based judgment.
- The agent must not widen a Backend permission: being able to read or edit on the Backend does not grant authority to expose confidential content.

## Evaluation signals

- The number of times confidential content was referenced by pointer instead of transcribed by value into a governed or derived field
- The number of confidentiality escalations raised when authorization or sensitivity was uncertain, versus silent exposures caught after the fact
- The number of Derived Artifacts generated with confidential values redacted
- Adoption of an explicit `sensitivity` label in Knowledge Repositories, reducing reliance on content-based inference
