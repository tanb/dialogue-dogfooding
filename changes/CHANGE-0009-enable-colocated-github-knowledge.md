---
id: CHANGE-0009
type: change_record
title: Enable a co-located Knowledge source on private GitHub
status: applied
scope:
  project: dialogue
  domain: development
  subject: self-hosting
revision: 1
created_at: "2026-07-16T04:39:53+09:00"
updated_at: "2026-07-16T04:39:53+09:00"
created_by: agent:codex
updated_by: agent:codex
related:
  - PROPOSAL-0009
  - STATE-SELF-HOSTING-001
extensions:
  adapter: git-github
  approval_source: direct_user_instruction
  source_topology: co-located
  repository_visibility: private
change_set_id: CHANGESET-0009
proposal_ref: PROPOSAL-0009
change_class: C4
decision: approved
approvals:
  - approval_id: APPROVAL-0009
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 1
    decided_at: "2026-07-16T04:39:53+09:00"
    conditions:
      - Make the GitHub Repository private
      - Use tanb as the GitHub owner
targets:
  - id: PROPOSAL-0009
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
  - id: STATE-SELF-HOSTING-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
reason: Continuously dogfood Knowledge discovery and conversational Decision Capture with Dialogue's own Git workflow
applied_at: "2026-07-16T04:39:53+09:00"
applied_by: agent:codex
---

# Enable a co-located Knowledge source on private GitHub

## Applied changes

- Created `tanb/dialogue` on GitHub as a Private Repository.
- Configured the Git remote, `main`, and `development/knowledge` in `.knowledge.yml`.
- Defined the discovery and change procedures at the Knowledge root.
- Updated the Self-hosting State from bootstrap to active.

## Verification evidence

- GitHub API: `nameWithOwner=tanb/dialogue`
- GitHub API: `visibility=PRIVATE`
- Git remote: `origin=https://github.com/tanb/dialogue.git`
