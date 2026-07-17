---
id: PROPOSAL-0009
type: proposal
title: Private GitHubでco-located Knowledge sourceを有効化する
status: approved
scope:
  project: dialogue
  domain: development
  subject: self-hosting
revision: 2
created_at: "2026-07-16T04:39:53+09:00"
updated_at: "2026-07-16T04:39:53+09:00"
created_by: agent:codex
updated_by: person:project-owner
related:
  - STATE-SELF-HOSTING-001
  - STATE-PRODUCT-SCOPE-001
  - PROPOSAL-0008
  - CHANGE-0009
extensions:
  approval_source: direct_user_instruction
  approval_evidence: conversation:private-github-request
  approved_subject_revision: 1
  change_record: CHANGE-0009
  approvals:
    - approval_id: APPROVAL-0009
      actor_ref: person:project-owner
      decision: approved
      subject_revision: 1
      decided_at: "2026-07-16T04:39:53+09:00"
      conditions:
        - GitHub Repositoryをprivateにする
        - GitHub ownerにtanbを使用する
change_class: C4
proposed_by: agent:codex
targets:
  - id: STATE-SELF-HOSTING-001
    action: update
    expected_revision: 1
requested_changes:
  - field: knowledge-source
    before:
      status: pending-remote
      url: null
      path: development/knowledge
    after:
      status: active
      url: https://github.com/tanb/dialogue.git
      ref: main
      path: development/knowledge
  - field: source-topology
    before: bootstrap-filesystem
    after: co-located-git
  - field: repository-visibility
    before: not-created
    after: private
reason: Dialogue自身のGit workflowでKnowledge discoveryと会話Decision Captureを継続的にDogfoodingする
evidence_refs:
  - conversation:private-github-request
  - .knowledge.yml
  - github:tanb/dialogue
impact: DialogueのコードとKnowledgeは同じPrivate remoteを共有し、Knowledge操作はmainのdevelopment/knowledgeへ限定される
---

# Private GitHubでco-located Knowledge sourceを有効化する

## Decision

ユーザーはGitHubの`tanb` ownerを使用し、DialogueをPrivate Repositoryとして開発する方針を明示した。直前に検討したco-located構成に基づき、同Repositoryの`development/knowledge/`をKnowledge rootとして採用する。
