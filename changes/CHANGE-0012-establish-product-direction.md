---
id: CHANGE-0012
type: change_record
title: Newly create Product Direction v1 as a canonical record
status: applied
scope:
  project: dialogue
  domain: product
  subject: product-direction-v1
revision: 1
created_at: "2026-07-17T23:59:31+09:00"
updated_at: "2026-07-17T23:59:31+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - PROPOSAL-0012
  - STATE-PRODUCT-DIRECTION-001
  - STATE-PRODUCT-SCOPE-001
extensions:
  approval_source: direct_user_instruction
  session: office-hours-2026-07-17
  change_set_id: CHANGESET-0012
proposal_ref: PROPOSAL-0012
change_class: C3
decision: approved
approvals:
  - approval_id: APPROVAL-0012
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 0
    decided_at: "2026-07-17T23:59:31+09:00"
    conditions:
      - Treat the Turbovec search layer not as a canonical record but as a derived read accelerator
      - This direction does not change the scope contract of STATE-PRODUCT-SCOPE-001
    evidence: >-
      Let's go with A. And please document what we decided in this discussion
      using the manage-project-knowledge skill.
targets:
  - id: STATE-PRODUCT-DIRECTION-001
    action: create
    before_revision: 0
    after_revision: 1
    result: applied
    error: null
reason: >-
  Record the product direction finalized in office-hours (Thesis, Two pillars, Positioning,
  next step, North Star) as an independent canonical State, so that the basis for subsequent
  judgments lives in a single place.
applied_at: "2026-07-17T23:59:31+09:00"
applied_by: agent:claude
---

# Newly create Product Direction v1 as a canonical record

## Applied changes

- Newly created `STATE-PRODUCT-DIRECTION-001` (`docs/product-direction-v1.md`) and made it the canonical record with `canonical_for: dialogue/product/direction-v1`.
- Recorded the Thesis "single source of truth for decisions", the Two pillars (Governance + Anti-rot), the Positioning against Agent memory and against wikis, the next step (Approach A: a conflict & rot demo), and the North Star (Turbovec MCP).

## Rationale

Git Knowledge discovery via `.knowledge.yml` and Human Escalation are the primary path of Product v1. The direction finalized in office-hours is a higher-level basis for judgment than the scope contract (`STATE-PRODUCT-SCOPE-001`), and it should live in an independent canonical State rather than in code or Git history. This is itself dogfooding of Dialogue's own Thesis.

## Impact

- The scope contract and acceptance criteria of Product v1 are unchanged.
- For the first time, Anti-rot's "continuous organization by Agents" is canonicalized as a product promise.
- The Turbovec MCP is recorded as a North Star for the derived layer outside the v1 scope, and it does not contradict the scope doc's exclusion of a Vector Database.
- `STATE-PRODUCT-SCOPE-001` was not updated by this change (referenced via `related` only).
