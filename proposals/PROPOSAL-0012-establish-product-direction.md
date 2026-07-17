---
id: PROPOSAL-0012
type: proposal
title: Canonicalize Product Direction v1 (single source of truth for decisions, Anti-rot, next step, and North Star)
status: approved
scope:
  project: dialogue
  domain: product
  subject: product-direction-v1
revision: 1
created_at: "2026-07-17T23:59:31+09:00"
updated_at: "2026-07-17T23:59:31+09:00"
created_by: agent:claude
updated_by: person:project-owner
related:
  - STATE-PRODUCT-DIRECTION-001
  - STATE-PRODUCT-SCOPE-001
  - PROJECT-CHARTER-001
  - CHANGE-0012
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:office-hours-2026-07-17
  approved_subject_revision: 0
  change_record: CHANGE-0012
  session: office-hours-2026-07-17
  approvals:
    - approval_id: APPROVAL-0012
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 0
      decided_at: "2026-07-17T23:59:31+09:00"
      conditions:
        - Treat the Turbovec search layer as a derived read accelerator, not the canonical record
        - This direction does not change the scope contract of STATE-PRODUCT-SCOPE-001
change_class: C3
proposed_by: agent:claude
targets:
  - id: STATE-PRODUCT-DIRECTION-001
    action: create
    expected_revision: 0
requested_changes:
  - field: thesis
    before: null
    after: Decided facts should live in one place (a single source of truth for decisions)
  - field: pillars
    before: null
    after:
      - governance-single-source-plus-human-escalation
      - anti-rot-staleness-and-duplication-detection-with-agent-cleanup
  - field: positioning
    before: null
    after:
      primary_differentiation: vs-agent-memory
      promotional_headline: Nothing is as sloppy as human document management / Dialogue is a Governance Protocol for agents
  - field: next-step
    before: null
    after: collision-and-rot-demo
  - field: north-star
    before: null
    after:
      concept: turbovec-backed-mcp-fast-canonical-search
      constraint: derivative-read-accelerator-not-canonical
      scope: post-v1
reason: >-
  Canonicalize the product direction, positioning, next step, and North Star that the user finalized
  during office hours (2026-07-17), so that agents and humans going forward can make decisions grounded
  in the same direction.
evidence_refs:
  - conversation:office-hours-2026-07-17
  - STATE-PRODUCT-SCOPE-001
impact: >-
  The scope contract and acceptance criteria of Product v1 are unchanged. This canonicalizes, for the
  first time, Anti-rot's "continuous cleanup by agents" as a product promise, and records the Turbovec
  MCP as an out-of-v1-scope derived-layer North Star.
---

# Canonicalize Product Direction v1

## Decision

In the office-hours session, the user finalized the following.

- Thesis: "Decided facts should live in one place." Dialogue is the single source of truth for decisions.
- Add to the killer differentiation the Anti-rot promise of detecting staleness and duplication and having agents clean them up.
- The primary differentiation is versus agent memory; the promotional headline is versus wikis.
- The next step is Approach A (a demo that showcases collisions and rot).
- Record fast canonical search via a Turbovec-backed MCP as the North Star. However, treat it as a derived read accelerator rather than the canonical record, and keep it out of v1 scope.

## Approval evidence

User's finalizing statements during the conversation (excerpts):

- "I want to convey the philosophy that decided facts should live in one place."
- "In Dialogue we make a promise to detect staleness and duplication of information and have agents clean it up. I think this leads to the killer differentiation, or the deciding factor of 'this is what I wanted.'"
- "I'd like to proceed with A. In fact, going forward I think we could prepare an MCP integrated with Turbovec so that fast canonical search becomes possible (omitted), and I believe that could become killer content."
- "Let's go with A. And please document what we decided in this discussion using the manage-project-knowledge skill."
