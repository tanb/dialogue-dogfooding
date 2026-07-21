---
id: STATE-DISPOSITION-HOLD-001
type: state
title: Disposition and Legal Hold Recognition
status: active
scope:
  project: dialogue
  domain: governance
  subject: disposition-hold
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
  - STATE-KNOWLEDGE-PRACTICES-001
  - PROPOSAL-0025
  - CHANGE-0025
canonical_for: dialogue/governance/disposition-hold
owners:
  - person:project-owner
extensions:
  document_kind: operating-policy
  activation_status: active
---

# Disposition and Legal Hold Recognition

## Decision

Deactivating, archiving, and destroying knowledge are governed acts, not cleanup an agent performs on its own. The Backend and additional policies **define and enforce** retention periods, legal holds, and destruction. The agent's separate, non-delegable responsibility is to **observe** those signals, **propose** disposition, and **hold back** when a hold applies. This is the same Backend-enforces / agent-observes division as confidentiality (`STATE-CONFIDENTIALITY-BOUNDARY-001`).

## Practice (D)

The distributed `dialogue-knowledge` Skill ("Recognize retention and hold before disposition") and `dialogue-history` Skill (Pack) carry this as a mandatory practice:

1. **Propose, do not execute.** Treat deactivation, archiving, and deletion as changes an agent proposes and a human decides. Age alone is never a sufficient reason.
2. **Honor a hold.** If a Knowledge Item declares a retention or legal-hold signal, do not deactivate, archive, or Pack it while the hold is active; halt and escalate. If no signal is declared, follow the ordinary lifecycle checks and do not infer a hold that was never recorded.
3. **Keep disposition reversible and referable.** Archiving is not deletion: preserve the id, provenance, Change Record, and successor references so the item stays resolvable in an explicit historical investigation.

## Consistency with existing knowledge

This practice adds no new lifecycle transition and relaxes no existing rule. It is reconciled with the current specification as follows.

- **Governance §2 scope is unchanged.** Retention periods and legal preservation obligations remain *additional policies*; their **definition and enforcement** are out of Core scope. This practice governs only how the agent **observes** them, so it does not move §2's boundary.
- **It specializes an existing Core obligation.** The Knowledge Management Protocol §7.6 and Governance §12 already require verifying *retention requirements* and referenceability before `Inactive → Archived`. This practice specifies how the agent meets that obligation — propose, honor holds, keep referable — and bridges the gap between §7.6's "confirm retention requirements" and §2's "retention is an additional policy".
- **Pack seal is strengthened, not weakened.** A hold is an **additional** block on Pack's seal precondition (Knowledge Management Protocol §7.8), which already requires every record in a partition to be terminal. A held record blocks sealing even when terminal; the terminal requirement itself is untouched.
- **It reinforces safety invariant 10.** Deletion is never the implementation of Archive; disposition stays reversible and referable.

## Seam and checker

A declared retention or legal-hold signal (for example `extensions.legal_hold`, or a retention marker) is an **optional, forward-compatible seam**, mirroring the sensitivity label. When absent, the ordinary lifecycle checks still apply and the agent does not fabricate a hold. As with confidentiality, **no deterministic checker is bundled**: whether disposition is warranted, and whether a hold applies in the absence of an explicit signal, are semantic judgments that a mechanical "clean" result would wrongly reassure.

## Evaluation signals

- The number of disposition actions raised as proposals for human decision versus executed autonomously
- The number of Pack or Archive operations correctly withheld because a hold was active
- The number of Archived items that remained resolvable in an explicit historical investigation
- Adoption of an explicit retention or legal-hold signal in Knowledge Repositories
