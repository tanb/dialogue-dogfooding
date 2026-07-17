---
id: PROPOSAL-0018
type: proposal
title: Knowledgeを製品リポジトリから独立したdialogue-dogfoodingへ分離する
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
        - Knowledge rootは新Repositoryのトップレベル（path .）とする
        - 製品リポジトリtanb/dialogueは配布物のみとし内部統治インスタンスを含めない
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
  Dialogueはskills.shおよび.claude-pluginでリポジトリ丸ごと配布されるため、co-located構成では
  Dialogue内部の統治インスタンス（dogfoodingの全governed文書とAuthority Registryのuid束縛）が
  全ユーザーに配布されてしまう。Knowledgeを独立Private Repository tanb/dialogue-dogfooding へ分離し、
  製品リポジトリを配布物のみにする。これはDialogueの主用途（プロジェクトから独立したKnowledge
  Repository）そのものをDogfoodingすることにもなる。
evidence_refs:
  - conversation:separate-knowledge-repo-2026-07-18
  - github:tanb/dialogue-dogfooding
impact: >-
  製品リポジトリtanb/dialogueは配布物（Skill/protocol/schemas/templates）とscripts/testsのみになり、
  内部統治インスタンスを配布しない。DialogueのKnowledgeはtanb/dialogue-dogfoodingのトップレベルに移り、
  .dialogue.ymlはそれを指す。CHANGE-0009のco-located採用はここでsupersedeする。
---

# Knowledgeを独立Repositoryへ分離する

## Decision

Dialogueはskills.sh（`npx skills add`）と`.claude-plugin`のいずれでも**リポジトリ丸ごと**がユーザーに配布される。co-located構成ではDialogue内部の統治インスタンス（`dogfooding/`の全governed文書、Authority Registryの`uid:501`束縛）が全ユーザーに渡ってしまう。

ユーザー判断により、Knowledgeを独立Private Repository `tanb/dialogue-dogfooding` のトップレベル（path `.`）へ分離し、製品リポジトリ`tanb/dialogue`を配布物のみにする。CHANGE-0009（co-located採用）の該当判断をsupersedeする。

## Approval evidence

- 「skillとして配布するときはこのレポジトリごとユーザーの手元に配布されるかもしれません。それをかんがえるとdogfoodingをこのレポジトリでやらない方がよいと思いはじめました。」
- 「https://github.com/tanb/dialogue-dogfoodingをつくってあります。こちらのトップレベルをpathに指定してよいです。」「Aでおねがいします。」
