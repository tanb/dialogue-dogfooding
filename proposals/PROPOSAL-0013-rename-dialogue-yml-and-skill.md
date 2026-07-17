---
id: PROPOSAL-0013
type: proposal
title: Rename the config file to .dialogue.yml and the Core Skill to dialogue-knowledge
status: approved
scope:
  project: dialogue
  domain: product
  subject: product-scope-v1
revision: 1
created_at: "2026-07-18T00:47:00+09:00"
updated_at: "2026-07-18T00:47:00+09:00"
created_by: agent:claude
updated_by: person:project-owner
related:
  - STATE-PRODUCT-SCOPE-001
  - STATE-PRODUCT-DIRECTION-001
  - CHANGE-0013
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:rename-dialogue-yml-2026-07-18
  approved_subject_revision: 2
  change_record: CHANGE-0013
  naming_principle: entry-points-branded-domain-vocabulary-descriptive
  approvals:
    - approval_id: APPROVAL-0013
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 2
      decided_at: "2026-07-18T00:47:00+09:00"
      conditions:
        - Keep the domain vocabulary "knowledge" as descriptive and rename only the entry points
        - Preserve the old names in historical Proposals/Change Records as a record
        - Reserve bare "dialogue" as the Skill family name and make the Core Skill dialogue-knowledge
change_class: C4
proposed_by: agent:claude
targets:
  - id: STATE-PRODUCT-SCOPE-001
    action: update
    expected_revision: 2
requested_changes:
  - field: config-filename
    before: .knowledge.yml
    after: .dialogue.yml
  - field: core-skill-name
    before: manage-project-knowledge
    after: dialogue-knowledge
reason: >-
  Align the entry points (the config file and the Core Skill) with the product name Dialogue to improve
  memorability and ease of instruction for users. The runtime files are already consistent as
  .dialogue.lock / .dialogue-transaction.json, so this also resolves the inconsistency of the config file
  being the odd one out as .knowledge.yml.
evidence_refs:
  - conversation:rename-dialogue-yml-2026-07-18
  - STATE-PRODUCT-SCOPE-001
impact: >-
  The config file name and Core Skill name of the v1 deliverable change (a breaking change). Since no
  external users yet exist and this is self-dogfooding only, we do a hard rename without dual support.
  The domain vocabulary "knowledge" and the schema file knowledge.schema.json remain unchanged.
---

# Align the config file and Core Skill with the product name

## Decision

The user finalized the following.

- Rename the config file `.knowledge.yml` to `.dialogue.yml`.
- Rename the Core Skill `manage-project-knowledge` to `dialogue-knowledge`.
- Reserve bare `dialogue` as the Skill family name, and in the future line up `dialogue-git` / `dialogue-conformance` and so on. This prepares for the charter's planned proliferation of a Core Skill plus backend-specific Skills.

## Naming principle

Align the entry points (config file and Skill name) with the product brand, while keeping the domain vocabulary (Knowledge Repository, knowledge root, knowledge-governance) and `knowledge.schema.json` descriptive.

## Approval evidence

User's finalizing statements during the conversation (excerpts):

- "I want to make .knowledge.yml into .dialogue.yml. Aligning it with the product name dialogue makes it easier for users to use. Let's change the skill name to match as well, and I feel a shorter name is easier to use."
- "If we can consider this itself to be a skill named dialogue, then dialogue seems good. If there are multiple skills within dialogue, we have to separate the names."
- "Please go with that." (In response to the policy of making the Core Skill `dialogue-knowledge` and reserving `dialogue` as the family name.)
