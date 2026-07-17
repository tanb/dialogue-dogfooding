---
id: CHANGE-0014
type: change_record
title: Rename the self-hosting Knowledge root to development/dogfooding
status: applied
scope:
  project: dialogue
  domain: development
  subject: self-hosting
revision: 1
created_at: "2026-07-18T01:10:00+09:00"
updated_at: "2026-07-18T01:10:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - PROPOSAL-0014
  - STATE-SELF-HOSTING-001
extensions:
  approval_source: direct_user_instruction
  change_set_id: CHANGESET-0014
proposal_ref: PROPOSAL-0014
change_class: C4
decision: approved
approvals:
  - approval_id: APPROVAL-0014
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 2
    decided_at: "2026-07-18T01:10:00+09:00"
    conditions:
      - Align source.path in .dialogue.yml with development/dogfooding
      - Preserve the old path development/knowledge in historical Proposals/Change Records as records
    evidence: >-
      I want to change the development/knowledge directory to development/dogfooding,
      and set source.path in .dialogue.yml to development/dogfooding. It is fine to stack
      this directly onto #11.
targets:
  - id: STATE-SELF-HOSTING-001
    action: update
    before_revision: 2
    after_revision: 3
    result: applied
    error: null
reason: >-
  To make the self-hosting configuration explicit in the name, rename the Knowledge root
  path to development/dogfooding and have .dialogue.yml's source.path and the verification
  scan path follow suit.
applied_at: "2026-07-18T01:10:00+09:00"
applied_by: agent:claude
---

# Rename the Knowledge root to development/dogfooding

## Applied changes

### Rename
- Directory `development/knowledge/` → `development/dogfooding/` (moved together with docs / proposals / changes / governance / AGENTS.md)

### Follow-on updates (feature / current)
- `source.path` in root `.dialogue.yml`: `development/knowledge` → `development/dogfooding`
- Changed the document scan path in `development/scripts/validate_repository.py` to `development/dogfooding`
- `AGENTS.md` (the Read first path and the co-located root description)
- `development/README.md` (the layout and self-hosting descriptions, relative `knowledge/` → `dogfooding/`)
- The `document_root == development/dogfooding` assertion in pytest `test_knowledge_source.py`
- active State `STATE-SELF-HOSTING-001` (rev2→3, updated the Knowledge root path)

### Left as is (intentional)
- The domain vocabulary "knowledge" (Knowledge Repository / knowledge root / knowledge-management-protocol / knowledge.schema.json)
- Historical Proposals / Change Records (CHANGE-0009 / PROPOSAL-0007,0008,0009 / CHANGE-0013) and the archived doc's old path `development/knowledge` (retained as records of past decisions)

## Rationale

This directory is the concrete instance of dogfooding, where Dialogue's own decision-making is managed with Dialogue's protocol. The name `dogfooding` makes the self-hosting configuration explicit and distinguishes it from the general concept "knowledge." Only the root location changes; the protocol and domain vocabulary are unchanged.

## Impact

- `.dialogue.yml` points to `development/dogfooding`, and `validate_repository.py` verification-scans that same directory.
- Breaking, but because there are zero external users (self-hosting only), no dual support is needed.
- Historical records retain the old path `development/knowledge`, and only the current canonical record `STATE-SELF-HOSTING-001` was updated to the new path.
