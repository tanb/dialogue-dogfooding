---
id: CHANGE-0021
type: change_record
title: Settle the maintenance-cycle fail-closed boundary at the canonical conflict only
status: applied
scope:
  project: dialogue
  domain: governance
  subject: maintenance-cycle
revision: 1
created_at: "2026-07-18T08:00:00+09:00"
updated_at: "2026-07-18T08:00:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - STATE-MAINTENANCE-CYCLE-001
  - PROPOSAL-0020
  - CHANGE-0020
extensions:
  approval_source: existing_decision
  operation: update_state
  change_set_id: CHANGESET-0021
proposal_ref: PROPOSAL-0020
change_class: C2
decision: applied
targets:
  - id: STATE-MAINTENANCE-CYCLE-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
reason: >-
  Synchronize STATE-MAINTENANCE-CYCLE-001 to an already-approved decision. APPROVAL-0020 (in PROPOSAL-0020
  and CHANGE-0020) approved the maintenance cycle under the condition "Fail closed only on an unresolvable
  canonical conflict; surface the other five categories as review items." The user confirmed this is a
  settled decision, so record the fail-closed boundary explicitly in the State body. No new policy choice
  is introduced; this binds the State to existing Evidence.
applied_at: "2026-07-18T08:00:00+09:00"
applied_by: agent:claude
---

# Settle the maintenance-cycle fail-closed boundary

## Applied changes

- `STATE-MAINTENANCE-CYCLE-001` rev1→2: added a settled-decision statement to the Severity section — only a canonical `conflict` is blocking; the other five categories remain review items and must not be escalated to blocking without a new governance decision.

## Rationale

This is an evidence-bound synchronization (C2), not a new decision. The boundary was already approved as a condition of `APPROVAL-0020` when the maintenance cycle was adopted (`PROPOSAL-0020` / `CHANGE-0020`). The user confirmed it as settled ("fail-closed は canonical 衝突のみにとどめます" and the instruction to record it in the Knowledge Repository), so the State document is updated to state the boundary explicitly rather than leaving it implicit in an approval condition.

## Impact

- The implemented checker (`skills/dialogue-knowledge/scripts/check-maintenance`), the Skill prose, and this State now agree that blocking is limited to a canonical conflict.
- Escalating any of the five review categories to blocking later requires a new governance decision, not a silent code change.
- No behavior change to the checker; this only makes the settled boundary canonical in the Knowledge Repository.
