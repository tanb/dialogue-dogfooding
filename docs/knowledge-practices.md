---
id: STATE-KNOWLEDGE-PRACTICES-001
type: state
title: Agent Read and Write Practices
status: active
scope:
  project: dialogue
  domain: governance
  subject: knowledge-practices
revision: 1
created_at: "2026-07-21T13:00:00+09:00"
updated_at: "2026-07-21T13:00:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - GOVERNANCE-001
  - GLOSSARY-001
  - FAILURE-MODEL-001
  - STATE-CONFIDENTIALITY-BOUNDARY-001
  - PROPOSAL-0025
  - CHANGE-0025
canonical_for: dialogue/governance/knowledge-practices
owners:
  - person:project-owner
extensions:
  document_kind: operating-policy
  activation_status: active
---

# Agent Read and Write Practices

## Decision

Three read-and-write disciplines are mandatory practices of the distributed `dialogue-knowledge` Skill. Each operationalizes an existing governance rule at the point where an agent actually reads or writes, rather than adding new rules. None ships a deterministic checker, because each is a semantic judgment; the existing `check-maintenance` targets are the mechanical safety net after the fact.

## B. Search before create (prevent duplication at its source)

Before creating a new Knowledge Item, search for an existing Active State with the same `canonical_for` or scope. If one exists, update or consolidate it instead of creating a duplicate.

- This **prevents** the F3 (Duplicate ownership) failure at its source; it does not replace the after-the-fact Duplicate detection in the maintenance cycle (`STATE-MAINTENANCE-CYCLE-001`), which remains the safety net.
- It aligns with Consolidate (Knowledge Management Protocol §7.5) and the Knowledge Curator role (`GOVERNANCE-001` §4.5).

## C. Consistent classification and vocabulary

Choose the `scope` domain and subject from the vocabulary the repository already uses.

- Search existing scopes before coining a new term. Avoid synonyms that fragment one subject across near-identical names, and propose consolidation when such fragmentation is found.
- This supports the protocol rule that canonicality, authority, and conflicts are evaluated within scopes that are identical or in a containment relationship (Knowledge Management Protocol §4.2). Fragmented vocabulary silently defeats that evaluation.
- A repository-declared controlled vocabulary is an optional, forward-compatible seam, mirroring the sensitivity label. Until one is declared, "match the existing usage" is the behavioral rule. Semantic fragmentation is heuristic, so no checker is bundled.

## E. Verify currency before using knowledge

Before using knowledge to answer or act — not only when editing — verify it is current.

- Reconcile the Active source of truth against its Change Records for currency and provenance, re-confirm any Derived Artifact against the canonical record, and keep Archived items out of the basis.
- If the target cannot be uniquely resolved as current, treat it as unresolved and escalate rather than answering from a stale or ambiguous basis.
- This applies the Truth Resolution rules of Knowledge Governance (`GOVERNANCE-001` §11) and Resolve (Knowledge Management Protocol §7.1) **at read time**, not just at edit time. It does not create a new resolution rule; it strengthens the read-time application of failures F4 (stale active knowledge), F10 (archive leakage), and F14 (retrieval omission).

## Relationship to existing knowledge

These practices add no new governance rule and change no lifecycle transition. They are read/write disciplines that make existing rules effective at the moment of use. Disposition and hold recognition is a separate, lifecycle-facing practice recorded in `STATE-DISPOSITION-HOLD-001`.

## Evaluation signals

- The number of would-be duplicates avoided by updating or consolidating an existing State instead of creating a new one
- The number of new scope terms coined versus reused from existing vocabulary
- The number of stale-basis answers avoided by a read-time currency check, versus stale answers caught after the fact
