---
id: CHANGE-0025
type: change_record
title: Adopt agent read/write practices (search-before-create, vocabulary consistency, currency verification, disposition and hold)
status: applied
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
  - PROPOSAL-0025
  - STATE-KNOWLEDGE-PRACTICES-001
  - STATE-DISPOSITION-HOLD-001
  - FAILURE-MODEL-001
  - GLOSSARY-001
  - GOVERNANCE-001
  - STATE-CONFIDENTIALITY-BOUNDARY-001
extensions:
  approval_source: direct_user_instruction
  operation: change_governance
  change_set_id: CHANGESET-0025
proposal_ref: PROPOSAL-0025
change_class: C4
decision: approved
approvals:
  - approval_id: APPROVAL-0025
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 0
    decided_at: "2026-07-21T13:00:00+09:00"
    conditions:
      - Operationalize existing governance rules at read/write points; add no new rule and change no lifecycle transition
      - Keep seams (controlled vocabulary, retention/legal-hold signal) optional and forward-compatible, mirroring the sensitivity label
      - Bundle no deterministic checker; each practice is a semantic judgment, with existing check-maintenance targets as the after-the-fact safety net
      - Reconcile with governance §2, protocol §7.6/§7.8/§4.2/§11, and F4 explicitly so no contradiction is introduced
    evidence: >-
      Selection of perspectives B, C, D, E to draft into the Skills and record in the Knowledge Repository,
      a request to confirm no contradiction with existing knowledge before updating, then approval of the
      reconciled change set with the instruction to proceed.
targets:
  - id: STATE-KNOWLEDGE-PRACTICES-001
    action: create
    before_revision: 0
    after_revision: 1
    result: applied
    error: null
  - id: STATE-DISPOSITION-HOLD-001
    action: create
    before_revision: 0
    after_revision: 1
    result: applied
    error: null
  - id: FAILURE-MODEL-001
    action: update
    before_revision: 4
    after_revision: 5
    result: applied
    error: null
  - id: GLOSSARY-001
    action: update
    before_revision: 4
    after_revision: 5
    result: applied
    error: null
reason: >-
  Codify four agent read/write disciplines that make existing governance rules effective at the moment of
  use: search before create (B), vocabulary consistency (C), currency verification (E), and disposition and
  hold recognition (D). Each operationalizes an existing rule rather than adding one; the Backend enforces
  and the agent observes; seams are optional; no checker is bundled.
applied_at: "2026-07-21T13:00:00+09:00"
applied_by: agent:claude
---

# Adopt agent read/write practices

## Applied changes

### Governance state (this Knowledge Repository)
- `STATE-KNOWLEDGE-PRACTICES-001` (new): canonical policy for B (search before create), C (vocabulary consistency), and E (currency verification), each mapped to the existing rule it operationalizes (§7.5/F3, §4.2, §11/F4/F10/F14).
- `STATE-DISPOSITION-HOLD-001` (new): canonical policy for D (disposition and legal-hold recognition), with an explicit reconciliation against governance §2, protocol §7.6/§12/§7.8, and invariant 10.
- `FAILURE-MODEL-001` rev4→5: added F18 (Premature or held disposition), distinct from F4 (staleness).
- `GLOSSARY-001` rev4→5: added Disposition, Retention, Legal Hold, and Currency.

### Product deliverables (distribution — dialogue branch tanb/agent-readwrite-practices)
- `skills/dialogue-knowledge/SKILL.md`:
  - Read section: added a read-time currency-verification paragraph (E).
  - Edit section: step 2 now requires searching for an existing Active State before creating (B); new step 3 requires choosing scope terms from existing vocabulary and proposing consolidation of fragmentation (C).
  - New "Recognize retention and hold before disposition" section (D): propose not execute, honor a declared hold, keep disposition reversible and referable.
- `skills/dialogue-history/SKILL.md`: Pack step 3 now treats a legal hold as an additional block on the terminal-only seal precondition, never a relaxation (D).

## Rationale

Separating agent practice from document-system governance surfaced four read/write disciplines that make existing rules effective at the point of use. Following the confidentiality-boundary precedent (CHANGE-0024), each is a behavioral practice — Backend enforces, agent observes — with optional forward-compatible seams and no bundled checker, because each is a semantic judgment for which a mechanical "clean" result would create false assurance.

## Consistency with existing knowledge

Verified before applying, and recorded in the two new States:
- Governance §2 scope is unchanged: retention and legal preservation remain additional policies whose definition and enforcement stay out of Core; the agent only observes them.
- D specializes the existing §7.6/§12 obligation to verify retention requirements before archiving, bridging §7.6 and §2.
- The Pack hold-block adds to §7.8's terminal-only seal precondition; it does not relax it.
- E applies governance §11 Truth Resolution at read time; it adds no new resolution rule.
- F18 is distinct from F4 (retention/hold vs staleness) and reinforces invariant 10 (deletion is never the implementation of Archive).

## Impact

- A Knowledge Repository the Skill manages gains four mandatory read/write practices that work today with no schema change, falling back to conservative behavior when no controlled-vocabulary or retention/hold signal is declared.
- Adding a controlled vocabulary or an `extensions.legal_hold` / retention signal is a forward-compatible enhancement (a deferred seam), not a precondition.
- No new governance rule or lifecycle transition is introduced; governance §2 scope is unchanged.
- No deterministic checker is bundled; F18 and the four practices are behavioral obligations, with the existing check-maintenance targets as the after-the-fact safety net.
- check-maintenance and check-authority run clean on this Knowledge Repository at the time of application.
