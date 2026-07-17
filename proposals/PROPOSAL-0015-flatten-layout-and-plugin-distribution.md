---
id: PROPOSAL-0015
type: proposal
title: Flatten the layout and make it distributable as a Claude Code plugin
status: approved
scope:
  project: dialogue
  domain: product
  subject: product-scope-v1
revision: 1
created_at: "2026-07-18T02:30:00+09:00"
updated_at: "2026-07-18T02:30:00+09:00"
created_by: agent:claude
updated_by: person:project-owner
related:
  - STATE-PRODUCT-SCOPE-001
  - STATE-SELF-HOSTING-001
  - CHANGE-0015
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:flatten-modern-layout-2026-07-18
  approved_subject_revision: 3
  change_record: CHANGE-0015
  reference: github:mattpocock/skills
  approvals:
    - approval_id: APPROVAL-0015
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 3
      decided_at: "2026-07-18T02:30:00+09:00"
      conditions:
        - Dissolve product/ and development/ and place the deliverables at the top level
        - The distribution boundary is declared by the .claude-plugin manifest
        - Add LICENSE (MIT) in the same PR
change_class: C4
proposed_by: agent:claude
targets:
  - id: STATE-PRODUCT-SCOPE-001
    action: update
    expected_revision: 3
  - id: STATE-SELF-HOSTING-001
    action: update
    expected_revision: 3
requested_changes:
  - field: repository-layout
    before: A split into product/ and development/. skills lives under product/skills
    after: skills/protocol/schemas/templates/dogfooding/scripts/tests at the top level. pyproject.toml at the root
  - field: distribution
    before: No distribution mechanism (directory convention only)
    after: Distribute as a Claude Code plugin via .claude-plugin (marketplace.json + plugin.json, source ./). Also supports skills.sh
  - field: acceptance-6
    before: Directory-boundary separation of Product and Development
    after: The boundary between deliverables and internal assets is declared by the .claude-plugin manifest
reason: >-
  Make the structure easy to distribute and modern. product/ is uncommon and redundant, so dissolve it
  and surface skills at the top level. Following mattpocock/skills, make it installable via .claude-plugin.
evidence_refs:
  - conversation:flatten-modern-layout-2026-07-18
  - github:mattpocock/skills
  - STATE-PRODUCT-SCOPE-001
impact: >-
  The directory placement of the deliverables changes, and via .claude-plugin it becomes installable from
  /plugin marketplace add tanb/dialogue. The product/development separation is redefined as "the manifest
  declares the distribution boundary." The meaning of the protocol contract, schemas, and rejection
  messages is unchanged.
---

# Flatten the layout and make it distributable as a plugin

## Decision

The user finalized the following.

- Dissolve `product/` and `development/`, and place `skills/` `protocol/` `schemas/` `templates/` `dogfooding/` `scripts/` `tests/` at the top level. Put `pyproject.toml` at the root (Python convention).
- Following `mattpocock/skills`, add `.claude-plugin/` (`marketplace.json` + `plugin.json`, `source: "./"`) and make it distributable as a Claude Code plugin. Also support skills.sh's `npx skills add`.
- Add `LICENSE` (MIT) in the same PR.

## Rationale

`product/` is not used in typical repositories and is redundant. Surfacing skills at the top level follows the modern trend. The core of ease of distribution is the `.claude-plugin` manifest, and with `source: "./"` the `skills/` directory is auto-discovered (confirmed in the official spec). The product/development separation philosophy is preserved in the form of "the manifest declares the distribution boundary."

## Approval evidence

- "Even so, it would be better to put skills at the top level. Because the product directory is not a directory used in typical repositories, and moreover it is redundant."
- "Completely flat (recommended)" "A standalone PR after merging the stack (recommended)" (finalizing the scope and timing).
- "Since it's already merged up to #12, I'd like you to restructure it. After that, add the LICENSE and submit it in a single PR."
