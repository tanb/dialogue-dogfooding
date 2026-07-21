---
id: STATE-KNOWLEDGE-PRACTICES-001
type: state
title: Agent Read and Write Practices
status: active
scope:
  project: dialogue
  domain: governance
  subject: knowledge-practices
revision: 2
created_at: "2026-07-21T13:00:00+09:00"
updated_at: "2026-07-21T14:00:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - GOVERNANCE-001
  - GLOSSARY-001
  - FAILURE-MODEL-001
  - STATE-CONFIDENTIALITY-BOUNDARY-001
  - PROPOSAL-0025
  - CHANGE-0025
  - PROPOSAL-0026
  - CHANGE-0026
canonical_for: dialogue/governance/knowledge-practices
owners:
  - person:project-owner
extensions:
  document_kind: operating-policy
  activation_status: active
---

# Agent Read and Write Practices

## Decision

Four read-and-write disciplines are mandatory practices of the distributed `dialogue-knowledge` Skill. Each operationalizes an existing governance rule at the point where an agent actually reads or writes, rather than adding new rules. None ships a deterministic checker, because each is a semantic judgment; the existing `check-maintenance` targets are the mechanical safety net after the fact.

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

## F. Attach only verifiable evidence

When proposing or recording a change, attach only evidence you can verify, and keep it distinct from your own claims. This discipline matters most where it is needed here: a shared record written and read by a mix of humans and multiple agents, where one actor acts on what another wrote.

- Distinguish verifiable evidence (a reference that resolves, a measurement you can reproduce, an approval trail) from a claim (your own reasoning or assertion). Label the latter as a claim, not as evidence.
- Confirm each reference exists, is current, and actually supports the point before citing it. Never present an unverifiable or fabricated basis — a reference or measurement you cannot confirm — as evidence.
- Do not launder another actor's unverified claim into evidence. In a mix of humans and multiple agents, an unconfirmed assertion repeated across actors can acquire false authority; treat it as a claim until independently verified. This is the failure mode a multi-agent setting adds that a single author rarely hits.
- Link the human approval trail in a form that can be re-checked from the Change Record, so a later reader can re-verify the basis rather than trust it.

This prevents F11 (broken provenance) and F19 (fabricated or unverifiable evidence) at their source. It operationalizes the glossary distinction between Fact, Claim, and Evidence, and Governance principle 5 (traceable to rationale and deciding actor), at the moment an agent writes. As with the other practices, no checker is bundled: whether a basis truly supports a claim is a semantic judgment, and the human approver's ability to re-verify — rather than rubber-stamp — is the real safeguard.

## Relationship to existing knowledge

These practices add no new governance rule and change no lifecycle transition. They are read/write disciplines that make existing rules effective at the moment of use. Disposition and hold recognition is a separate, lifecycle-facing practice recorded in `STATE-DISPOSITION-HOLD-001`.

## Evaluation signals

- The number of would-be duplicates avoided by updating or consolidating an existing State instead of creating a new one
- The number of new scope terms coined versus reused from existing vocabulary
- The number of stale-basis answers avoided by a read-time currency check, versus stale answers caught after the fact
- The number of bases labeled as claims versus attached as evidence, and the number of unverifiable or fabricated references caught before they entered a Change Record
