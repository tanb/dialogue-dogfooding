---
id: CHANGE-0019
type: change_record
title: Update the Knowledge Repository visibility to public
status: applied
scope:
  project: dialogue
  domain: development
  subject: self-hosting
revision: 1
created_at: "2026-07-18T06:00:00+09:00"
updated_at: "2026-07-18T06:00:00+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - PROPOSAL-0019
  - STATE-SELF-HOSTING-001
extensions:
  approval_source: direct_user_instruction
change_set_id: CHANGESET-0019
proposal_ref: PROPOSAL-0019
change_class: C3
decision: approved
approvals:
  - approval_id: APPROVAL-0019
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 5
    decided_at: "2026-07-18T06:00:00+09:00"
    conditions:
      - Describe the repository without a visibility adjective in product-facing prose
    evidence: >-
      tanb/dialogue-dogfooding has become a public repository, so should the
      wording be changed a little? (chosen: drop the visibility adjective)
targets:
  - id: STATE-SELF-HOSTING-001
    action: update
    before_revision: 5
    after_revision: 6
    result: applied
    error: null
reason: >-
  The Knowledge Repository tanb/dialogue-dogfooding is now public; sync the recorded
  self-hosting visibility to the current fact and remove the stale "Private" wording.
applied_at: "2026-07-18T06:00:00+09:00"
applied_by: agent:claude
---

# Update the Knowledge Repository visibility to public

## Applied changes

- `STATE-SELF-HOSTING-001` rev5->6: `repository_visibility` private -> public; the "Repository visibility" status line set to public; the prose "independent Private Knowledge Repository" changed to "independent Knowledge Repository".
- Product repository (applied in a separate PR on tanb/dialogue): removed the "Private" adjective in `README.md` and `AGENTS.md` ("a separate Knowledge Repository").

## Rationale

The owner made `tanb/dialogue-dogfooding` public, so the recorded visibility "private" was stale. Sync the self-hosting state to the fact. In product-facing prose, describe the repository without a visibility adjective so it does not go stale again.

## Impact

- The recorded Knowledge Repository visibility is public.
- Historical records (CHANGE-0018 and earlier) keep the visibility that was accurate at the time and are not rewritten.
