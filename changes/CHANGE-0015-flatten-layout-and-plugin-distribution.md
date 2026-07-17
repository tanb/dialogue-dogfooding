---
id: CHANGE-0015
type: change_record
title: Flatten the layout and make it distributable as a Claude Code plugin
status: applied
scope:
  project: dialogue
  domain: product
  subject: product-scope-v1
revision: 1
created_at: "2026-07-18T02:30:00+09:00"
updated_at: "2026-07-18T02:30:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - PROPOSAL-0015
  - STATE-PRODUCT-SCOPE-001
  - STATE-SELF-HOSTING-001
extensions:
  approval_source: direct_user_instruction
  reference: github:mattpocock/skills
  change_set_id: CHANGESET-0015
proposal_ref: PROPOSAL-0015
change_class: C4
decision: approved
approvals:
  - approval_id: APPROVAL-0015
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 3
    decided_at: "2026-07-18T02:30:00+09:00"
    conditions:
      - Dissolve product/ and development/ and place the deliverables directly at the top level
      - The distribution boundary is declared by the .claude-plugin manifest
      - Add LICENSE (MIT) in the same PR
    evidence: >-
      Since everything up to #12 is already merged, I would like you to restructure it.
      After that, add the LICENSE and submit it as a single PR.
targets:
  - id: STATE-PRODUCT-SCOPE-001
    action: update
    before_revision: 3
    after_revision: 4
    result: applied
    error: null
  - id: STATE-SELF-HOSTING-001
    action: update
    before_revision: 3
    after_revision: 4
    result: applied
    error: null
reason: >-
  To make the layout easy to distribute and modern, dissolve product/ and development/ and
  place the deliverables directly at the top level, and make it distributable as a Claude Code
  plugin via .claude-plugin.
applied_at: "2026-07-18T02:30:00+09:00"
applied_by: agent:claude
---

# Flatten the layout and make it plugin-distributable

## Applied changes

### Flattening the directories (dissolving product/ and development/)
- `product/skills/dialogue-knowledge/` → `skills/dialogue-knowledge/`
- `product/protocol/*.md` → `protocol/`
- `product/config/knowledge.schema.json` + `product/protocol/schemas/*.json` → `schemas/` (consolidated)
- `product/templates/.dialogue.yml` → `templates/.dialogue.yml`
- `development/dogfooding/` → `dogfooding/`
- `development/scripts/` → `scripts/`, `development/tests/` → `tests/`
- `development/{pyproject.toml,uv.lock,.python-version}` → root
- Deleted the stale `product/README.md` / `development/README.md`

### Distribution mechanism
- `.claude-plugin/marketplace.json` (name/owner/plugins[{ name:"dialogue", source:"./" }])
- `.claude-plugin/plugin.json` (name:"dialogue", version, license:MIT …)
- With `source: "./"`, `skills/dialogue-knowledge/SKILL.md` is auto-discovered
- Added `LICENSE` (MIT)

### Follow-on updates
- `source.path` in `.dialogue.yml`: `dogfooding`
- `scripts/validate_repository.py` (ROOT hierarchy, the globs for schema/protocol/dogfooding/tests/skills)
- `scripts/check_conformance.py` (ROOT hierarchy, cases glob)
- `tests/dialogue_support.py` (REPO_ROOT hierarchy, RESOLVER), `tests/test_skill_activation.py`, `tests/test_knowledge_source.py`
- `.github/workflows/ci.yml` (removed `working-directory: development`, run from root)
- All paths in `AGENTS.md` / `README.md` / `protocol/protocol-conformance.md`, and the `$id` in `schemas/knowledge.schema.json`

### Governance
- `STATE-PRODUCT-SCOPE-001` rev3→4: redefined the distribution boundary (acceptance criterion #6), updated the layout and distribution path

## Rationale

`product/` is non-idiomatic and redundant. Surfacing skills directly at the top level follows the modern trend. The core of distribution ease is `.claude-plugin`, and the separation philosophy of product/development is preserved in the form of "the manifest declares the distribution boundary."

## Impact

- Distributable via `/plugin marketplace add tanb/dialogue` → `/plugin install dialogue@dialogue`, and via `npx skills add tanb/dialogue`.
- Verification runs from root with `uv run python scripts/validate_repository.py` / `uv run pytest`.
- The meaning of the protocol contract, schemas, and safety judgments is unchanged. The old paths in historical Proposals/Change Records are retained as records.
