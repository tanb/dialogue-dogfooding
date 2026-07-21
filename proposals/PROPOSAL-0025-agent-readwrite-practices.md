---
id: PROPOSAL-0025
type: proposal
title: Adopt agent read/write practices (search-before-create, vocabulary consistency, currency verification, disposition and hold)
status: approved
scope:
  project: dialogue
  domain: governance
  subject: knowledge-practices
revision: 1
created_at: "2026-07-21T13:00:00+09:00"
updated_at: "2026-07-21T13:00:00+09:00"
created_by: agent:claude
updated_by: person:project-owner
related:
  - GOVERNANCE-001
  - GLOSSARY-001
  - FAILURE-MODEL-001
  - STATE-KNOWLEDGE-PRACTICES-001
  - STATE-DISPOSITION-HOLD-001
  - STATE-CONFIDENTIALITY-BOUNDARY-001
  - CHANGE-0025
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:agent-readwrite-practices-2026-07-21
  change_record: CHANGE-0025
  operation: change_governance
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
change_class: C4
proposed_by: agent:claude
targets:
  - id: STATE-KNOWLEDGE-PRACTICES-001
    action: create
    expected_revision: 0
  - id: STATE-DISPOSITION-HOLD-001
    action: create
    expected_revision: 0
  - id: FAILURE-MODEL-001
    action: update
    expected_revision: 4
  - id: GLOSSARY-001
    action: update
    expected_revision: 4
requested_changes:
  - field: search-before-create
    before: The Edit workflow identified an existing canonical target but did not require searching for an existing Active State before creating a new Item; duplication was only detected after the fact by the maintenance cycle
    after: The Skill searches for an existing Active State with the same canonical_for or scope before creating, and updates or consolidates instead of duplicating, preventing F3 at its source (STATE-KNOWLEDGE-PRACTICES-001 B)
  - field: vocabulary-consistency
    before: scope domain/subject were free-form with no guidance, so synonyms could fragment a subject across near-identical names and silently defeat scope-based canonicality (protocol §4.2)
    after: The Skill chooses scope terms from the vocabulary the repository already uses, searches before coining a term, and proposes consolidation of fragmentation; a controlled vocabulary is an optional seam (STATE-KNOWLEDGE-PRACTICES-001 C)
  - field: currency-verification
    before: The read workflow preferred Active documents but did not require verifying currency and provenance before using knowledge to answer or act; Truth Resolution (governance §11) was applied mainly at edit time
    after: The Skill verifies currency against Change Records, re-confirms Derived Artifacts against the canonical record, and escalates an unresolved basis before answering — applying governance §11 at read time (STATE-KNOWLEDGE-PRACTICES-001 E)
  - field: disposition-and-hold
    before: Disposition guidance was limited to "age alone is not sufficient"; there was no practice for observing retention/legal-hold signals, proposing rather than executing disposition, or blocking Pack/Archive under a hold
    after: The dialogue-knowledge and dialogue-history Skills observe retention/hold signals, propose disposition for human decision, and withhold Archive/Pack under an active hold; a hold is an additional block on the Pack seal precondition, not a relaxation (STATE-DISPOSITION-HOLD-001, F18)
  - field: failure-model
    before: The failure model had no failure for disposition performed without confirming retention or against an active hold
    after: Add F18 (Premature or held disposition), distinct from F4 (staleness), reconciled with §7.6/§7.8 and invariant 10
reason: >-
  Separating what the agent must practice from what the document system governs surfaced four read/write
  disciplines (B search-before-create, C vocabulary consistency, E currency verification, D disposition and
  hold recognition) that make existing governance rules effective at the moment an agent reads or writes.
  Each operationalizes an existing rule rather than adding a new one, mirroring the confidentiality-boundary
  precedent (CHANGE-0024): Backend enforces, agent observes; seams are optional and forward-compatible; no
  checker is bundled because each is a semantic judgment.
evidence_refs:
  - conversation:agent-readwrite-practices-2026-07-21
  - GOVERNANCE-001
  - FAILURE-MODEL-001
  - STATE-CONFIDENTIALITY-BOUNDARY-001
impact: >-
  Any Knowledge Repository the Skill manages gains four mandatory read/write practices that work today with
  no schema change, falling back to conservative behavior when no controlled-vocabulary or retention/hold
  signal is declared. No new governance rule or lifecycle transition is introduced; governance §2 scope is
  unchanged (retention/legal remain additional policies whose definition and enforcement stay out of Core).
  No deterministic checker is bundled, so heuristic detection creates no false assurance.
---

# Adopt agent read/write practices

## Decision

By the user's judgment, four agent read/write disciplines are adopted as mandatory practices of the distributed Skills, each operationalizing an existing governance rule at the point of use:

1. **B — Search before create** (`STATE-KNOWLEDGE-PRACTICES-001`): prevent F3 duplication at its source.
2. **C — Vocabulary consistency** (`STATE-KNOWLEDGE-PRACTICES-001`): keep scope terms consistent so §4.2 canonicality holds.
3. **E — Currency verification** (`STATE-KNOWLEDGE-PRACTICES-001`): apply governance §11 Truth Resolution at read time.
4. **D — Disposition and hold recognition** (`STATE-DISPOSITION-HOLD-001`, `FAILURE-MODEL-001` F18): observe retention/hold, propose not execute, withhold Pack/Archive under a hold.

Seams (controlled vocabulary, retention/legal-hold signal) are optional and forward-compatible, mirroring the sensitivity label. No deterministic checker is bundled.

## Consistency reconciliation

- Governance §2 scope unchanged: retention/legal definition and enforcement remain additional policies; the agent only observes.
- D specializes the existing §7.6/§12 obligation to verify retention requirements; it bridges §7.6 and §2 without moving either.
- The Pack hold-block is an addition to §7.8's terminal-only seal precondition, never a relaxation.
- E strengthens the read-time application of F4/F10/F14 and does not create a new resolution rule.
- F18 is distinct from F4 (retention/hold vs staleness) and reinforces invariant 10.

## Approval evidence

- Selection of perspectives B, C, D, E to draft into the Skills and record in the Knowledge Repository.
- A request to confirm there is no contradiction with existing knowledge before updating, followed by approval of the reconciled change set with the instruction to proceed.
