---
id: CHANGE-0020
type: change_record
title: Adopt the continuous knowledge-maintenance cycle as a mandatory regulation and bundle a deterministic checker
status: applied
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
  - PROPOSAL-0020
  - STATE-MAINTENANCE-CYCLE-001
  - GLOSSARY-001
  - GOVERNANCE-001
extensions:
  approval_source: direct_user_instruction
  operation: change_governance
  change_set_id: CHANGESET-0020
proposal_ref: PROPOSAL-0020
change_class: C4
decision: approved
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
    evidence: >-
      "2ですね。先ほどあげた６項目はknowledgeを長期管理するために必須の規約になります。なので、これを同梱しなければ
      ユーザーはskill(dialogue-knowledge)を使用してドキュメントを管理できません。" followed by the instruction to
      record the decision in the Knowledge Repository.
targets:
  - id: STATE-MAINTENANCE-CYCLE-001
    action: create
    before_revision: 0
    after_revision: 1
    result: applied
    error: null
  - id: GLOSSARY-001
    action: update
    before_revision: 2
    after_revision: 3
    result: applied
    error: null
reason: >-
  Codify the six-target continuous maintenance cycle as a mandatory regulation and enforce it with a
  CI-independent deterministic checker bundled in the distributed Skill, so a Knowledge Repository can be
  kept consistent with the Skill alone.
applied_at: "2026-07-18T07:00:00+09:00"
applied_by: agent:claude
---

# Adopt the continuous knowledge-maintenance cycle and bundle a deterministic checker

## Applied changes

### Governance state (this Knowledge Repository)
- `STATE-MAINTENANCE-CYCLE-001` (new): the canonical maintenance-cycle policy — six detection targets, two severity tiers (blocking canonical conflict / review for the rest), correction-within-authority bounds, and the bundled checker as the enforcement mechanism.
- `GLOSSARY-001` rev2→3: extended the Knowledge Curator role from four detection targets to all six mechanical targets (adding missing Change Records and derived-artifact drift) and named the bundled checker, aligning the glossary with the new state.

### Product deliverables (distribution — dialogue PR #19)
- `skills/dialogue-knowledge/scripts/check-maintenance` (new): a deterministic checker for the six targets. Exit 2 on a `conflict` (two Active States sharing one `canonical_for`, fail-closed); exit 0 with `review` findings for duplicate, broken reference, missing Change Record, staleness, and derived drift. Only structural links (`proposal_ref`, `extensions.change_record`, successor refs) are broken-reference checked; the free-form `related` list is not. PyYAML dependency, CI-independent.
- `skills/dialogue-knowledge/SKILL.md`: the "Maintain knowledge continuously" section enumerates the six targets and runs the checker (mirroring "Reconcile authority"); blocking = stop and escalate, review = maintenance item.
- `README.md`: points maintainers at both `check-authority` and `check-maintenance`.
- `tests/test_maintenance_check.py` (new): pins the contract for all six categories and both severity tiers. Added the `MAINTENANCE_CHECKER` path to `tests/dialogue_support.py`.

## Rationale

The maintenance cycle previously lived only in the protocol (`GOVERNANCE-001` §4.5, §13) and `AGENTS.md`, never in the Skill an agent loads, and had no mechanical enforcement. Prose alone leaves "detect these on a cycle" unenforced. Following the Authority gap detection precedent (CHANGE-0017), detection is normalized and bundled as a deterministic, CI-independent checker so it does not depend on whether the user runs CI.

## Impact

- A Knowledge Repository the Skill manages can be reconciled for maintenance decay with `python3 skills/dialogue-knowledge/scripts/check-maintenance --document-root <root>`, independent of CI.
- An unresolvable canonical conflict fails closed and halts; the other five categories surface without stopping the system.
- Only mechanically decidable violations are reported; semantic staleness, semantic conflict, and external derived drift still require human confirmation.
- The checker runs clean on this Knowledge Repository at the time of application (46 documents, 0 blocking, 0 review).
