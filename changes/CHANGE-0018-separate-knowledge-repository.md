---
id: CHANGE-0018
type: change_record
title: Separate the Knowledge into the independent dialogue-dogfooding repository, apart from the product repository
status: applied
scope:
  project: dialogue
  domain: development
  subject: self-hosting
revision: 1
created_at: "2026-07-18T05:00:00+09:00"
updated_at: "2026-07-18T05:00:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - PROPOSAL-0018
  - STATE-SELF-HOSTING-001
  - CHANGE-0009
extensions:
  approval_source: direct_user_instruction
  supersedes: CHANGE-0009
  change_set_id: CHANGESET-0018
proposal_ref: PROPOSAL-0018
change_class: C4
decision: approved
approvals:
  - approval_id: APPROVAL-0018
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 4
    decided_at: "2026-07-18T05:00:00+09:00"
    conditions:
      - Make the Knowledge root the top level (path .) of the new Repository
      - Keep the product repository tanb/dialogue as deliverables only, excluding the internal governance instance
    evidence: >-
      I have created https://github.com/tanb/dialogue-dogfooding. It is fine to specify
      the top level of this repository as the path. Please go with A.
targets:
  - id: STATE-SELF-HOSTING-001
    action: update
    before_revision: 4
    after_revision: 5
    result: applied
    error: null
reason: >-
  So that the deliverables do not include Dialogue's internal governance instance, separate the
  Knowledge into the independent Private Repository tanb/dialogue-dogfooding, and point
  .dialogue.yml at its top level.
applied_at: "2026-07-18T05:00:00+09:00"
applied_by: agent:claude
---

# Separate the Knowledge into an independent Repository

## Applied changes

### Knowledge repository (tanb/dialogue-dogfooding)
- Moved all governed documents under `dogfooding/` (docs / proposals / changes / governance / AGENTS.md) to the top level.
- `STATE-SELF-HOSTING-001` rev4→5: changed the source topology from co-located to separate-repository, the remote to `tanb/dialogue-dogfooding.git`, and the Knowledge root to `.`.

### Product repository (tanb/dialogue, applied in a separate PR)
- Deleted `dogfooding/`.
- Changed `.dialogue.yml` to `url: https://github.com/tanb/dialogue-dogfooding.git`, `path: .`.
- Removed the ids that moved to the knowledge repository (PROPOSAL-0017/CHANGE-0017/CHANGE-0011) from the `related` of `protocol/knowledge-governance.md` and `protocol/protocol-conformance.md`.
- `scripts/validate_repository.py`: narrowed the scan of `validate_documents()` to `protocol/*.md` only, and removed `validate_authority()` (the self-scan).
- Changed the document_root assertion in `tests/test_knowledge_source.py` to `.`.
- Updated the `dogfooding/` references in `AGENTS.md` and `README.md` to assume the independent Repository.

## Rationale

Because skills.sh and .claude-plugin distribute the entire repository, in a co-located setup Dialogue's internal governance instance would be handed to every user. Separation makes the product deliverables only, while at the same time dogfooding Dialogue's primary use case (an independent Knowledge Repository).

## Impact

- The deliverables no longer include Dialogue's internal governance instance (43 documents plus the uid binding).
- Dialogue's dogfooding becomes "running the product's Skill / check-authority against this independent Knowledge Repository," matching how users use it.
- Supersedes the co-located adoption of CHANGE-0009. Historical records are retained.
