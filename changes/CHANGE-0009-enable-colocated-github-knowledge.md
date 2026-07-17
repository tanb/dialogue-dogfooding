---
id: CHANGE-0009
type: change_record
title: Private GitHubでco-located Knowledge sourceを有効化する
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
      - GitHub Repositoryをprivateにする
      - GitHub ownerにtanbを使用する
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
reason: Dialogue自身のGit workflowでKnowledge discoveryと会話Decision Captureを継続的にDogfoodingする
applied_at: "2026-07-16T04:39:53+09:00"
applied_by: agent:codex
---

# Private GitHubでco-located Knowledge sourceを有効化する

## Applied changes

- GitHubに`tanb/dialogue`をPrivate Repositoryとして作成した。
- `.knowledge.yml`へGit remote、`main`、`development/knowledge`を設定した。
- Knowledge rootへ探索と変更手順を定義した。
- Self-hosting Stateをbootstrapからactiveへ更新した。

## Verification evidence

- GitHub API: `nameWithOwner=tanb/dialogue`
- GitHub API: `visibility=PRIVATE`
- Git remote: `origin=https://github.com/tanb/dialogue.git`
