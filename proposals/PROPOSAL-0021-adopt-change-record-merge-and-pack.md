---
id: PROPOSAL-0021
type: proposal
title: Adopt Change Record Merge and lossless Pack
status: approved
scope:
  project: dialogue
  domain: governance
  subject: change-history
revision: 2
created_at: "2026-07-18T21:30:00+09:00"
updated_at: "2026-07-18T21:30:00+09:00"
created_by: agent:claude
updated_by: person:project-owner
related:
  - STATE-PRODUCT-SCOPE-001
  - PROTOCOL-001
  - CHANGE-0022
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:current-user-instruction
  change_record: CHANGE-0022
  approved_subject_revision: 1
  approvals:
    - approval_id: APPROVAL-0021
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 1
      decided_at: "2026-07-18T21:30:00+09:00"
      conditions: []
change_class: C3
proposed_by: agent:claude
targets:
  - id: STATE-PRODUCT-SCOPE-001
    action: update
    expected_revision: 4
  - id: PROTOCOL-001
    action: update
    expected_revision: 4
requested_changes:
  - field: protocol.change-record.merge
    before: A divergence on the same canonical target has no defined reconciliation
    after: Reconcile divergent Change Records with an append-only Merge (merge_of / reconciles), at least C3, without renumbering or overwriting
  - field: protocol.adapter.pack
    before: Change Record files accumulate without bound and the readable sequence can overflow its digits
    after: Pack a sealed, all-terminal partition losslessly into a pack file plus manifest; the readable sequence resets per partition
  - field: dialogue-yml.history.pack
    before: No history configuration
    after: Select Pack granularity via history.pack (strategy none|time|count), chosen at bootstrap, with an explicit none recording a deliberate opt-out
reason: Keep a long-lived, many-author Knowledge Repository from accumulating unbounded Change Record files or overflowing readable sequence numbers, while preserving the append-only ledger as the canonical record
evidence_refs:
  - https://github.com/tanb/dialogue/pull/21
  - protocol/knowledge-management-protocol.md
  - schemas/change-record.schema.json
  - schemas/pack-manifest.schema.json
  - skills/dialogue-history/SKILL.md
impact: Adds an optional, backward-compatible history-maintenance capability (a new dialogue-history Skill, additive schema fields, and .dialogue.yml history.pack). Governance, the Authority Registry, and the lifecycle state machine are unchanged
---

# Adopt Change Record Merge and lossless Pack

## Decision

Across this conversation the project owner settled the design for long-lived change history:

- The readable per-record number is a cosmetic, per-partition ordering hint (the Django-migration model), not an identity.
- Divergent Change Records on the same canonical target are reconciled by an append-only **Merge** rather than by renumbering or rebasing.
- Old history is compacted only by **lossless Pack**, never a lossy squash, so the Change Record set stays the canonical ledger.
- Pack granularity is chosen at **bootstrap** and recorded explicitly in `.dialogue.yml` `history.pack`; declining writes an explicit `strategy: none`.

The user's instruction to reflect these decisions into the Knowledge Repository is recorded as the Human Approval for this C3 change.
