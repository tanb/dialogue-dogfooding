---
id: PROPOSAL-0020
type: proposal
title: Adopt the continuous knowledge-maintenance cycle as a mandatory regulation and bundle a deterministic checker
status: approved
scope:
  project: dialogue
  domain: governance
  subject: maintenance-cycle
revision: 1
created_at: "2026-07-18T07:00:00+09:00"
updated_at: "2026-07-18T07:00:00+09:00"
created_by: agent:claude
updated_by: person:project-owner
related:
  - GOVERNANCE-001
  - GLOSSARY-001
  - STATE-MAINTENANCE-CYCLE-001
  - CHANGE-0020
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:knowledge-maintenance-cycle-2026-07-18
  change_record: CHANGE-0020
  operation: change_governance
  approvals:
    - approval_id: APPROVAL-0020
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 0
      decided_at: "2026-07-18T07:00:00+09:00"
      conditions:
        - Bundle detection as a deterministic checker the Skill can run without depending on CI, like check-authority
        - Fail closed only on an unresolvable canonical conflict; surface the other five categories as review items
        - The checker reports mechanical candidates only and never fabricates a semantic verdict
change_class: C4
proposed_by: agent:claude
targets:
  - id: STATE-MAINTENANCE-CYCLE-001
    action: create
    expected_revision: 0
  - id: GLOSSARY-001
    action: update
    expected_revision: 2
requested_changes:
  - field: maintenance-cycle-regulation
    before: The maintenance cycle (detect and correct staleness, duplicates, conflicts, broken references) lived only in the protocol and AGENTS.md, never in the distributed Skill, with no mechanical enforcement
    after: Adopt the six-target maintenance cycle as a mandatory regulation with a canonical State document, bundled as a deterministic checker in the distributed Skill
  - field: detection-checker
    before: No maintenance checker; "detect these on a cycle" was prose-only and unenforced
    after: Bundle skills/dialogue-knowledge/scripts/check-maintenance. Blocking (exit 2) on a canonical conflict, review (exit 0) for the other five categories, CI-independent
  - field: glossary-curator-scope
    before: The Knowledge Curator role lists four detection targets (duplication, conflict, broken references, staleness)
    after: The Knowledge Curator role covers all six mechanical targets, including missing Change Records and derived-artifact drift, and names the bundled checker
reason: >-
  The six maintenance targets are required to manage knowledge over the long term. Without a bundled,
  CI-independent checker a user cannot actually keep a Knowledge Repository consistent with the Skill
  alone. Codify the cycle as a mandatory regulation and enforce it deterministically, mirroring the
  Authority gap detection precedent (CHANGE-0017).
evidence_refs:
  - conversation:knowledge-maintenance-cycle-2026-07-18
  - GOVERNANCE-001
  - GLOSSARY-001
impact: >-
  Any Knowledge Repository the Skill manages can be reconciled for maintenance decay without CI. An
  unresolvable canonical conflict fails closed and halts; the other five categories surface as maintenance
  items and do not stop the system. Only mechanically decidable violations are reported, so semantic
  staleness and semantic conflict still require human confirmation.
---

# Adopt the continuous knowledge-maintenance cycle and bundle a deterministic checker

## Decision

By the user's judgment, the continuous maintenance cycle is a mandatory regulation for long-term knowledge management, and it must be bundled into the distributed `dialogue-knowledge` Skill so a user can manage documents with the Skill alone.

1. **Regulation**: Adopt the six-target maintenance cycle (conflict, duplicate, broken reference, missing Change Record, staleness, derived-artifact drift) as current governance state (`STATE-MAINTENANCE-CYCLE-001`).
2. **Deterministic checker**: Bundle `skills/dialogue-knowledge/scripts/check-maintenance`. Blocking (exit 2) on a canonical conflict (fail-closed); review (exit 0) for the other five categories. CI-independent, PyYAML dependency, on the same footing as `check-authority`.
3. **Glossary alignment**: Extend the Knowledge Curator role from four to all six mechanical targets so the glossary does not conflict with the new state.

## Approval evidence

- "2ですね。先ほどあげた６項目はknowledgeを長期管理するために必須の規約になります。なので、これを同梱しなければユーザーはskill(dialogue-knowledge)を使用してドキュメントを管理できません。" (choosing the bundled deterministic checker and declaring the six targets a mandatory regulation).
- "チェッカー同梱をまずPRにコミットしてください。その後で、Knowledge Repo に決定として記録してください。" (instruction to record this decision in the Knowledge Repository).
