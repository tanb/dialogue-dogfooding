---
id: CHANGE-0023
type: change_record
title: Finalize Merge and Pack after code review
status: applied
scope:
  project: dialogue
  domain: product
  subject: product-scope-v1
revision: 1
created_at: "2026-07-18T22:30:00+09:00"
updated_at: "2026-07-18T22:30:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - CHANGE-0022
  - PROPOSAL-0021
  - STATE-PRODUCT-SCOPE-001
  - PROTOCOL-001
extensions:
  adapter: manual-git
  supersedes_evidence_of: CHANGE-0022
  product_pr: "https://github.com/tanb/dialogue/pull/21"
  validation_cases: 20
change_set_id: CHANGESET-0023
proposal_ref: PROPOSAL-0021
change_class: C2
decision: approved
approvals: []
targets:
  - id: STATE-PRODUCT-SCOPE-001
    action: update
    before_revision: 5
    after_revision: 6
    result: applied
    error: null
reason: Record the review-driven finalization of PR #21 so the Knowledge does not remain stale against what shipped
applied_at: "2026-07-18T22:30:00+09:00"
applied_by: agent:claude
---

# Finalize Merge and Pack after code review

CHANGE-0022 was recorded when PR #21 was opened. A subsequent Fable 5 code review produced three fixes that landed in the same PR and the same PROTOCOL-001 revision 5. Because CHANGE-0022 is `applied` and immutable, this follow-on records the finalized state instead of overwriting it.

## Review-driven refinements (same PROTOCOL-001 rev 5)

- The declared `.dialogue.yml` JSON Schema (`schemas/knowledge.schema.json`) now accepts the `history.pack` block, mirroring `resolve-source`. At the time of CHANGE-0022 only the Python validator accepted it, so the shipped template and the repository's own `.dialogue.yml` were invalid against their own schema.
- The Merge conformance runner counts distinct `merge_of` ids, so a `merge_of` naming the same Change Record twice is rejected rather than treated as a valid Merge. Added regression case C-020.
- The section 6 Change Record lifecycle now shows `applied | rejected | failed → archived`, aligning the state machine with the pre-existing `change-record.schema.json` status enum, the section 7.8 Pack terminal set, `pack-manifest.schema.json`, the runner, and C-018.

## Corrected verification evidence

Supersedes the "Verification evidence" recorded in CHANGE-0022 (`19 conformance cases`, `42 passed`).

```text
7 JSON schemas parsed; local refs resolved
20 conformance cases passed
43 passed (pytest)
```

## Product Scope v1 update

Added acceptance criterion 7: `history.pack` is accepted or rejected consistently by both `resolve-source` and the declared `.dialogue.yml` JSON Schema.
