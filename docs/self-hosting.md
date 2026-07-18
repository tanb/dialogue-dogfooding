---
id: STATE-SELF-HOSTING-001
type: state
title: Dialogue Self-hosting Policy
status: active
scope:
  project: dialogue
  domain: development
  subject: self-hosting
revision: 6
created_at: "2026-07-16T04:29:45+09:00"
updated_at: "2026-07-18T06:00:00+09:00"
created_by: agent:codex
updated_by: agent:claude
related:
  - PROJECT-CHARTER-001
  - STATE-PRODUCT-SCOPE-001
  - PROPOSAL-0008
  - CHANGE-0008
  - PROPOSAL-0009
  - CHANGE-0009
  - PROPOSAL-0014
  - CHANGE-0014
  - PROPOSAL-0015
  - CHANGE-0015
  - PROPOSAL-0018
  - CHANGE-0018
  - PROPOSAL-0019
  - CHANGE-0019
canonical_for: dialogue/development/self-hosting
owners:
  - person:project-owner
extensions:
  document_kind: operating-policy
  activation_status: active
  knowledge_source_status: active
  source_topology: separate-repository
  repository_visibility: public
---

# Dialogue Self-hosting Policy

## Decision

Dialogue uses `dialogue-knowledge` for its own development. It automatically detects persistent decisions that were formed in conversation and reflects them into the current state and a semantic Change Record.

The user does not need to specify the Skill name. However, the Agent distinguishes ideas under discussion from settled decisions, and when in doubt does not change Active knowledge and confirms with a human.

## Activation rules

1. Confirm the Active knowledge relevant to the work before making a decision.
2. At the conversation's task boundary, extract the settled persistent decisions.
3. Update State, Proposal, and Change Record only when there is clear approval.
4. Stop updating on a conflict, ambiguity, or sync failure.
5. In the work result, report the recorded Knowledge Items or the reason none were recorded.

## Runtime status

- Local Skill activation rule: active
- Implicit invocation metadata: active
- Semantic Decision Capture: active
- `.dialogue.yml`: active
- Knowledge Git Repository remote: `https://github.com/tanb/dialogue-dogfooding.git`
- Git ref: `main`
- Knowledge root: `.` (repository top level)
- Source topology: separate-repository
- Repository visibility: public

Dialogue's code repository `tanb/dialogue` points, via `.dialogue.yml`, to the independent Knowledge Repository `tanb/dialogue-dogfooding`. It treats the `main` top level of a dedicated checkout as the Knowledge root. This configuration dogfoods Dialogue's primary use case (a shared Knowledge Repository independent of the project) itself, and at the same time verifies the Repository separation of code and Knowledge. To avoid including Dialogue's internal governance instance in the deliverables (Skill / protocol / schemas / templates), the Knowledge is separated from the product repository.

## Evaluation signals

- The number of decisions that should have been recorded but were not
- The number of false detections that treated an idea under discussion as settled
- The number of additional confirmations needed for Decision Capture
- The number of conflicts and stale revisions detected
- The impact of Knowledge updates on working time
