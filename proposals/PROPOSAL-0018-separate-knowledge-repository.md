---
id: PROPOSAL-0018
type: proposal
title: Separate Knowledge from the product repository into the independent dialogue-dogfooding
status: approved
scope:
  project: dialogue
  domain: development
  subject: self-hosting
revision: 1
created_at: "2026-07-18T05:00:00+09:00"
updated_at: "2026-07-18T05:00:00+09:00"
created_by: agent:claude
updated_by: person:project-owner
related:
  - STATE-SELF-HOSTING-001
  - PROPOSAL-0009
  - CHANGE-0009
  - CHANGE-0018
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:separate-knowledge-repo-2026-07-18
  approved_subject_revision: 4
  change_record: CHANGE-0018
  supersedes: CHANGE-0009
  approvals:
    - approval_id: APPROVAL-0018
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 4
      decided_at: "2026-07-18T05:00:00+09:00"
      conditions:
        - The Knowledge root is the top level (path .) of the new Repository
        - The product repository tanb/dialogue holds deliverables only and includes no internal governance instance
change_class: C4
proposed_by: agent:claude
targets:
  - id: STATE-SELF-HOSTING-001
    action: update
    expected_revision: 4
requested_changes:
  - field: source-topology
    before: co-located
    after: separate-repository
  - field: knowledge-source
    before:
      url: https://github.com/tanb/dialogue.git
      path: dogfooding
    after:
      url: https://github.com/tanb/dialogue-dogfooding.git
      path: .
reason: >-
  Because Dialogue is distributed as an entire repository via skills.sh and .claude-plugin, a co-located
  configuration would distribute Dialogue's internal governance instance (all governed documents of
  dogfooding and the uid binding in the Authority Registry) to all users. Separate the Knowledge into the
  independent private repository tanb/dialogue-dogfooding, and make the product repository deliverables-only.
  This also dogfoods Dialogue's primary use case itself (a Knowledge Repository independent from the project).
evidence_refs:
  - conversation:separate-knowledge-repo-2026-07-18
  - github:tanb/dialogue-dogfooding
impact: >-
  The product repository tanb/dialogue becomes only the deliverables (Skill/protocol/schemas/templates) plus
  scripts/tests, and does not distribute the internal governance instance. Dialogue's Knowledge moves to the
  top level of tanb/dialogue-dogfooding, and .dialogue.yml points to it. The co-located adoption of CHANGE-0009
  is superseded here.
---

# Separate Knowledge into an independent Repository

## Decision

Dialogue is distributed to users as an **entire repository** via either skills.sh (`npx skills add`) or `.claude-plugin`. In a co-located configuration, Dialogue's internal governance instance (all governed documents in `dogfooding/` and the `uid:501` binding in the Authority Registry) would be handed to every user.

By the user's judgment, separate the Knowledge into the top level (path `.`) of the independent private repository `tanb/dialogue-dogfooding`, and make the product repository `tanb/dialogue` deliverables-only. Supersede the relevant judgment of CHANGE-0009 (co-located adoption).

## Approval evidence

- "When distributed as a skill, this repository might be distributed to users as-is. Considering that, I'm starting to think it would be better not to do dogfooding in this repository."
- "I've created https://github.com/tanb/dialogue-dogfooding. You may specify its top level as the path." "Please go with A."
