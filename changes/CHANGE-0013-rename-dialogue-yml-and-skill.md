---
id: CHANGE-0013
type: change_record
title: Rename the configuration file to .dialogue.yml and the Core Skill to dialogue-knowledge
status: applied
scope:
  project: dialogue
  domain: product
  subject: product-scope-v1
revision: 1
created_at: "2026-07-18T00:47:00+09:00"
updated_at: "2026-07-18T00:47:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - PROPOSAL-0013
  - STATE-PRODUCT-SCOPE-001
  - STATE-PRODUCT-DIRECTION-001
extensions:
  approval_source: direct_user_instruction
  naming_principle: entry-points-branded-domain-vocabulary-descriptive
  change_set_id: CHANGESET-0013
proposal_ref: PROPOSAL-0013
change_class: C4
decision: approved
approvals:
  - approval_id: APPROVAL-0013
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 2
    decided_at: "2026-07-18T00:47:00+09:00"
    conditions:
      - Keep the domain vocabulary "knowledge" as descriptive and rename only the entry points
      - Preserve the old names in historical Proposals/Change Records as records
    evidence: >-
      Please go with that. (In response to the policy of renaming the Core Skill to
      dialogue-knowledge while preserving "dialogue" as the family name.)
targets:
  - id: STATE-PRODUCT-SCOPE-001
    action: update
    before_revision: 2
    after_revision: 3
    result: applied
    error: null
reason: >-
  Align the entry points with the product name Dialogue to improve memorability and ease
  of instruction. This also restores naming consistency with the runtime files
  (.dialogue.lock / .dialogue-transaction.json).
applied_at: "2026-07-18T00:47:00+09:00"
applied_by: agent:claude
---

# Align the configuration file and Core Skill with the product name

## Applied changes

### Renames
- Root configuration `.knowledge.yml` → `.dialogue.yml`
- Installation template `product/templates/.knowledge.yml` → `product/templates/.dialogue.yml`
- Core Skill directory `product/skills/manage-project-knowledge/` → `product/skills/dialogue-knowledge/` (updated `name: dialogue-knowledge`, the `$dialogue-knowledge` in `agents/openai.yaml`, and the display name)

### Follow-on updates to identifiers (product deliverables, feature code, active current-state docs)
- Changed the default file name and rejection message in `resolve-source` to `.dialogue.yml`
- `README.md` / `product/README.md` / `AGENTS.md` / `development/README.md` / `development/knowledge/AGENTS.md`
- pytest (`test_knowledge_source.py` / `test_knowledge_git_e2e.py` / `test_skill_activation.py` / `dialogue_support.py`)
- active State: `STATE-PRODUCT-SCOPE-001` (rev2→3), `product-direction-v1`, `project-charter`, `self-hosting`, `mvp-git-e2e-validation`
- Changed the `title` in `product/config/knowledge.schema.json` to `.dialogue.yml` (the file name `knowledge.schema.json` is left as is)

### Left as is (intentional)
- The domain vocabulary "knowledge" (Knowledge Repository / knowledge root / knowledge-governance / knowledge-management-protocol)
- The schema file name `knowledge.schema.json` and its `$id`
- The old names in historical Proposals / Change Records and the archived `filesystem-reference-implementation.md` (retained as records of past decisions)

## Rationale

Bringing the entry points (configuration file and Core Skill) closer to the product brand improves memorability and the ease of instructions like "use the dialogue-knowledge skill." The runtime files were already aligned under the `.dialogue` prefix, and this resolves the inconsistency where only the configuration file stood apart. The domain vocabulary is preserved with priority on descriptiveness, avoiding the ambiguity in documents that excessive branding would cause.

## Impact

- A breaking change that alters the v1 deliverable's configuration file name and Core Skill name. Because no external users exist, no dual support is provided; this is a hard rename.
- `.dialogue.yml` is validated by the unchanged `knowledge.schema.json` (consistent with leaving the domain vocabulary as is).
- Toward the future multiple skills (Core + backend-specific) that the charter plans, `dialogue` is preserved as the family name.
