---
id: STATE-MAINTENANCE-CYCLE-001
type: state
title: Dialogue Knowledge Maintenance Cycle
status: active
scope:
  project: dialogue
  domain: governance
  subject: maintenance-cycle
revision: 1
created_at: "2026-07-18T07:00:00+09:00"
updated_at: "2026-07-18T07:00:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - GOVERNANCE-001
  - GLOSSARY-001
  - FAILURE-MODEL-001
  - PROPOSAL-0020
  - CHANGE-0020
canonical_for: dialogue/governance/maintenance-cycle
owners:
  - person:project-owner
extensions:
  document_kind: operating-policy
  activation_status: active
---

# Dialogue Knowledge Maintenance Cycle

## Decision

Detecting and correcting the decay of shared knowledge is a **mandatory part of managing knowledge over the long term**, not optional cleanup. A user cannot manage knowledge with the `dialogue-knowledge` Skill alone unless the Skill can mechanically detect this decay. Therefore the maintenance cycle is bundled into the distributed Skill as a deterministic checker, on the same footing as Authority gap detection.

The cycle runs during maintenance passes and opportunistically whenever an agent reads or edits shared knowledge. It does not depend on the project running CI.

## Detection targets

The cycle detects six maintenance targets, aligned with the glossary and the Knowledge Curator role:

1. **Conflict** — two or more Active State documents claim the same `canonical_for`; the source of truth is unresolvable.
2. **Duplicate** — two or more Active State documents share the same scope under different ids.
3. **Broken reference** — a structural link that must resolve inside the Knowledge root (`proposal_ref`, `extensions.change_record`, a successor ref) points at an id that does not exist.
4. **Missing Change Record** — an approved or applied C3/C4 Proposal has no Change Record linking back to it, so a semantic change lacks traceable provenance.
5. **Staleness** — a Proposal left pending that no Active State references (an abandoned pending change). Age alone is never a sufficient condition.
6. **Derived-artifact drift** — a Derived Artifact (RAG index, cache, summary) whose recorded source revision lags the current revision of its source.

## Severity

Two tiers, mirroring the hard/soft split of Authority gap detection:

- **Blocking (fail-closed)** — a `conflict` makes truth-resolution unsafe. Stop, treat neither document as the source of truth, and escalate to a human. The bundled checker exits non-zero.
- **Review** — duplicate, broken reference, missing Change Record, staleness, and derived-artifact drift are surfaced as maintenance items. They never halt the system.

## Correction within authority

- An agent may autonomously detect these targets and draft Proposals, Change Records, and escalation packages for consolidation, deactivation, archiving, or re-validation.
- Regenerating a Derived Artifact from the canonical record is a C0 operation an agent may perform directly; correcting the canonical record it drifted from is not.
- An agent must not finalize a semantic change, resolve a conflict, deactivate, or archive without the write authority and explicit delegation the edit workflow requires. Deactivation and archiving conditions must be objective, recoverable, and auditable.
- The checker reports mechanical candidates only. It never decides semantic staleness, semantic conflict, or external derived-artifact drift on its own; a human confirms those before action.

## Mechanical enforcement

Detection ships as a deterministic, CI-independent checker in the distributed Skill:

```sh
python3 skills/dialogue-knowledge/scripts/check-maintenance --document-root <knowledge-root>
```

The Skill's "Maintain knowledge continuously" procedure runs it at each read, edit, and maintenance point. Only structural links that must resolve locally are checked for broken references; the free-form `related` list may point at governing protocol ids that live in the product repository and is not flagged.

## Evaluation signals

- The number of unresolvable canonical conflicts caught before they corrupted a decision
- The number of maintenance items surfaced versus corrected per pass
- The number of false detections that treated a legitimate external reference as broken
- The number of stale or abandoned Proposals re-validated, advanced, or withdrawn
- The lag between a source revision change and regeneration of its Derived Artifacts
