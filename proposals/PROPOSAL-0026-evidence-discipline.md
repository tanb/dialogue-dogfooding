---
id: PROPOSAL-0026
type: proposal
title: Adopt evidence discipline (F) as a mandatory read/write practice
status: approved
scope:
  project: dialogue
  domain: governance
  subject: knowledge-practices
revision: 1
created_at: "2026-07-21T14:00:00+09:00"
updated_at: "2026-07-21T14:00:00+09:00"
created_by: agent:claude
updated_by: person:project-owner
related:
  - GOVERNANCE-001
  - GLOSSARY-001
  - FAILURE-MODEL-001
  - STATE-KNOWLEDGE-PRACTICES-001
  - STATE-CONFIDENTIALITY-BOUNDARY-001
  - CHANGE-0026
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:evidence-discipline-2026-07-21
  change_record: CHANGE-0026
  operation: change_governance
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
change_class: C4
proposed_by: agent:claude
targets:
  - id: STATE-KNOWLEDGE-PRACTICES-001
    action: update
    expected_revision: 1
  - id: FAILURE-MODEL-001
    action: update
    expected_revision: 5
  - id: GLOSSARY-001
    action: update
    expected_revision: 5
requested_changes:
  - field: evidence-discipline
    before: STATE-KNOWLEDGE-PRACTICES-001 held three disciplines (B/C/E). Evidence quality was implied by the glossary (Fact/Claim/Evidence) and evidence_refs, but no write-time practice required distinguishing verifiable evidence from claims, confirming references, or refusing fabricated or laundered bases
    after: Add practice F (Attach only verifiable evidence) to STATE-KNOWLEDGE-PRACTICES-001 (rev1->2) — distinguish evidence from claims, verify each reference, refuse unverifiable or fabricated bases, and do not launder another actor's unverified claim into evidence; link a re-checkable approval trail
  - field: failure-model
    before: The failure model had F11 (broken provenance) and F13 (instruction injection) but no failure for evidence that is fabricated, unverifiable, or laundered across actors
    after: Add F19 (Fabricated or unverifiable evidence), distinct from F13, positioned as prevention of F11 at its source
  - field: glossary
    before: Evidence was "referenceable information that supports a claim", with no verifiability requirement and no term for cross-actor laundering
    after: Strengthen Evidence with a verifiability requirement and add Evidence Laundering, aligned with F19 and practice F
reason: >-
  In a shared record written and read by a mix of humans and multiple agents, one actor acts on what another
  wrote. Verifiable evidence is what lets a later reader — especially a human approver — re-check rather than
  rubber-stamp, and it blocks the multi-agent failure where an unconfirmed claim is laundered into apparent
  fact. This is exactly the collaborative documentation context Dialogue exists for (Governance §1). F
  operationalizes the existing Fact/Claim/Evidence distinction and principle 5 at write time, mirroring the
  confidentiality and read/write-practice precedents (CHANGE-0024, CHANGE-0025): Backend/humans hold final
  authority, the agent observes discipline, no checker is bundled.
evidence_refs:
  - conversation:evidence-discipline-2026-07-21
  - GLOSSARY-001
  - GOVERNANCE-001
  - FAILURE-MODEL-001
impact: >-
  Any Knowledge Repository the Skill manages gains a write-time evidence discipline that works today with no
  schema change. No new governance rule or lifecycle transition is introduced; it strengthens the existing
  Fact/Claim/Evidence distinction and principle 5. F19 is distinct from F13 and prevents F11 at its source.
  No deterministic checker is bundled, because verifiability of a basis is a semantic judgment; the human
  approver's ability to re-verify is the real safeguard.
---

# Adopt evidence discipline (F)

## Decision

By the user's judgment, evidence discipline (F) is adopted as the fourth mandatory read/write practice, in the collaborative-documentation context of a shared record written and read by a mix of humans and multiple agents.

1. **Practice F** in `STATE-KNOWLEDGE-PRACTICES-001` (rev1->2): distinguish verifiable evidence from claims; verify each reference; refuse unverifiable or fabricated bases; do not launder another actor's unverified claim into evidence; link a re-checkable approval trail.
2. **F19** in `FAILURE-MODEL-001` (rev5->6): Fabricated or unverifiable evidence, distinct from F13, preventing F11 at its source.
3. **Glossary** (rev5->6): strengthen Evidence with a verifiability requirement and add Evidence Laundering.

No new rule or lifecycle transition; no bundled checker.

## Approval evidence

- The user's assessment that F is necessary in the context of collaborative documentation among humans and multiple AI agents, and the instruction to proceed on PR #24 with the same change set.
