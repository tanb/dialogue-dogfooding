---
id: PROPOSAL-0019
type: proposal
title: Update the Knowledge Repository visibility to public
status: approved
scope:
  project: dialogue
  domain: development
  subject: self-hosting
revision: 1
created_at: "2026-07-18T06:00:00+09:00"
updated_at: "2026-07-18T06:00:00+09:00"
created_by: agent:claude
updated_by: person:project-owner
related:
  - STATE-SELF-HOSTING-001
  - CHANGE-0018
  - CHANGE-0019
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:dogfooding-repo-public-2026-07-18
  approved_subject_revision: 5
  change_record: CHANGE-0019
  approvals:
    - approval_id: APPROVAL-0019
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 5
      decided_at: "2026-07-18T06:00:00+09:00"
      conditions:
        - Describe the repository without a visibility adjective in product-facing prose
change_class: C3
proposed_by: agent:claude
targets:
  - id: STATE-SELF-HOSTING-001
    action: update
    expected_revision: 5
requested_changes:
  - field: repository-visibility
    before: private
    after: public
reason: >-
  The owner made tanb/dialogue-dogfooding a public repository, so the recorded
  visibility "private" is no longer accurate. Sync the self-hosting state to the
  current fact.
evidence_refs:
  - conversation:dogfooding-repo-public-2026-07-18
  - github:tanb/dialogue-dogfooding
impact: >-
  STATE-SELF-HOSTING-001 records the Knowledge Repository visibility as public.
  Product-facing prose (README, AGENTS) describes it without a visibility adjective
  so the wording does not go stale again. Historical records (CHANGE-0018 etc.)
  keep the visibility that was accurate at the time.
---

# Update the Knowledge Repository visibility to public

## Decision

The owner made the Knowledge Repository `tanb/dialogue-dogfooding` public. Update `STATE-SELF-HOSTING-001` so the recorded `repository_visibility` is `public`, and drop the "Private" adjective from the self-hosting prose. In the product repository's README and AGENTS, describe it as a separate Knowledge Repository without a visibility adjective, so the wording stays accurate if visibility changes again.

## Approval evidence

- "tanb/dialogue-dogfooding has become a public repository, so should the wording be changed a little?"
- Chosen option: drop the visibility adjective.
