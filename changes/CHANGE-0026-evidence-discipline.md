---
id: CHANGE-0026
type: change_record
title: Adopt evidence discipline (F) as a mandatory read/write practice
status: applied
scope:
  project: dialogue
  domain: governance
  subject: knowledge-practices
revision: 1
created_at: "2026-07-21T14:00:00+09:00"
updated_at: "2026-07-21T14:00:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - PROPOSAL-0026
  - STATE-KNOWLEDGE-PRACTICES-001
  - FAILURE-MODEL-001
  - GLOSSARY-001
  - GOVERNANCE-001
  - STATE-CONFIDENTIALITY-BOUNDARY-001
extensions:
  approval_source: direct_user_instruction
  operation: change_governance
  change_set_id: CHANGESET-0026
proposal_ref: PROPOSAL-0026
change_class: C4
decision: approved
approvals:
  - approval_id: APPROVAL-0026
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 0
    decided_at: "2026-07-21T14:00:00+09:00"
    conditions:
      - Operationalize the existing Fact/Claim/Evidence distinction and governance principle 5 at write time; add no new rule
      - Frame it for the target context — a shared record written and read by a mix of humans and multiple agents
      - Bundle no deterministic checker; verifiability of a basis is a semantic judgment
      - Add F19 distinct from F13 (instruction injection) and position it as prevention of F11 (broken provenance)
    evidence: >-
      The user's assessment that F is necessary for collaborative documentation among humans and multiple AI
      agents, and the instruction to proceed on PR #24 with the same change set.
targets:
  - id: STATE-KNOWLEDGE-PRACTICES-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: FAILURE-MODEL-001
    action: update
    before_revision: 5
    after_revision: 6
    result: applied
    error: null
  - id: GLOSSARY-001
    action: update
    before_revision: 5
    after_revision: 6
    result: applied
    error: null
reason: >-
  Codify evidence discipline (F) as the fourth agent read/write practice: distinguish verifiable evidence
  from claims, verify references, refuse fabricated or laundered bases, and link a re-checkable approval
  trail. It makes the existing Fact/Claim/Evidence distinction and principle 5 effective at write time, in
  the collaborative context of a shared record written and read by humans and multiple agents.
applied_at: "2026-07-21T14:00:00+09:00"
applied_by: agent:claude
---

# Adopt evidence discipline (F)

## Applied changes

### Governance state (this Knowledge Repository)
- `STATE-KNOWLEDGE-PRACTICES-001` rev1->2: added practice F (Attach only verifiable evidence), framed for the mix-of-humans-and-agents context; updated the Decision from three to four disciplines and added an evaluation signal.
- `FAILURE-MODEL-001` rev5->6: added F19 (Fabricated or unverifiable evidence), distinct from F13, positioned as prevention of F11 at its source.
- `GLOSSARY-001` rev5->6: strengthened Evidence with a verifiability requirement and added Evidence Laundering.

### Product deliverables (distribution — dialogue PR #24, branch tanb/agent-readwrite-practices)
- `skills/dialogue-knowledge/SKILL.md`: Edit step 4 now requires attaching only verifiable evidence and distinguishing it from claims; the closing paragraph forbids laundering another actor's unverified claim into evidence and requires a re-checkable approval trail (F19).

## Rationale

Dialogue exists for a shared record written and read by a mix of humans and multiple agents (Governance §1), where one actor acts on what another wrote. Verifiable evidence is what lets a later reader — especially a human approver — re-check rather than rubber-stamp, and it blocks the multi-agent failure where an unconfirmed claim is laundered into apparent fact. F operationalizes the existing Fact/Claim/Evidence distinction and principle 5 at write time, following the confidentiality and read/write-practice precedents (CHANGE-0024, CHANGE-0025). No checker is bundled, because verifiability of a basis is a semantic judgment.

## Consistency with existing knowledge

- Adds no new governance rule and no lifecycle transition; it strengthens the glossary Fact/Claim/Evidence distinction and Governance principle 5 at the moment of writing.
- F19 is distinct from F13 (instruction injection concerns a document body issuing commands; F19 concerns an unfounded basis presented as evidence) and prevents F11 (broken provenance) at its source.
- Consistent with the confidentiality boundary and disposition/hold practices: Backend and humans hold final authority, the agent observes discipline, seams stay optional, no checker is bundled.

## Impact

- A write-time evidence discipline that works today with no schema change.
- No new governance rule or lifecycle transition; governance scope is unchanged.
- No deterministic checker is bundled; F19 is a behavioral obligation, with the human approver's ability to re-verify as the real safeguard.
- check-maintenance and check-authority run clean on this Knowledge Repository at the time of application.
