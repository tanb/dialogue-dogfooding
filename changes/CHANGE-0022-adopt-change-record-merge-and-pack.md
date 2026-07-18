---
id: CHANGE-0022
type: change_record
title: Adopt Change Record Merge and lossless Pack
status: applied
scope:
  project: dialogue
  domain: governance
  subject: change-history
revision: 1
created_at: "2026-07-18T21:30:00+09:00"
updated_at: "2026-07-18T21:30:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - PROPOSAL-0021
  - STATE-PRODUCT-SCOPE-001
  - PROTOCOL-001
extensions:
  adapter: manual-git
  approval_source: direct_user_instruction
  product_pr: "https://github.com/tanb/dialogue/pull/21"
  validation_cases: 19
change_set_id: CHANGESET-0022
proposal_ref: PROPOSAL-0021
change_class: C3
decision: approved
approvals:
  - approval_id: APPROVAL-0021
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 1
    decided_at: "2026-07-18T21:30:00+09:00"
    conditions: []
targets:
  - id: PROPOSAL-0021
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: STATE-PRODUCT-SCOPE-001
    action: update
    before_revision: 4
    after_revision: 5
    result: applied
    error: null
  - id: PROTOCOL-001
    action: update
    before_revision: 4
    after_revision: 5
    result: applied
    error: null
reason: Keep long-lived history bounded and readable-number-safe while preserving the append-only ledger as the canonical record
applied_at: "2026-07-18T21:30:00+09:00"
applied_by: agent:claude
---

# Adopt Change Record Merge and lossless Pack

## Applied changes

- Protocol: added Merge (section 5.3.1) — an append-only Change Record with `merge_of` / `reconciles` that reconciles divergent revisions of the same canonical target, at least C3, without renumbering.
- Protocol: added Pack (section 7.8) — a lossless Adapter capability that relocates a sealed, all-terminal partition into a pack file plus manifest; the readable sequence resets per partition.
- Schema: `change-record` gains `merge_of` and per-target `reconciles` (C3+ enforced for merges); a new `pack-manifest` schema requires a content hash and a terminal status per entry.
- Config: `.dialogue.yml` gains `history.pack` (`strategy: none|time|count`), validated by `resolve-source` and chosen at bootstrap; an explicit `none` records a deliberate opt-out.
- Skill: added `dialogue-history` for the change-history plane (Merge, Pack, bootstrap config), shipped alongside `dialogue-knowledge`.
- Product Scope v1 updated to list the `history.pack` contract, the `dialogue-history` deliverable, and history maintenance in scope.

## Verification evidence

```text
7 JSON schemas parsed; local refs resolved
19 conformance cases passed
42 passed (pytest)
```

## Residual limits

- Pack file layout and manifest emission are Adapter responsibilities; the reference Git flow performs Pack manually.
- Merge detection surfaces a divergence; the reconciled meaning remains a Human decision and is not automated.
- Pack conformance is Adapter-level (`required: false`), not part of Core conformance.
