---
id: CHANGE-0018
type: change_record
title: Knowledgeを製品リポジトリから独立したdialogue-dogfoodingへ分離する
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
      - Knowledge rootは新Repositoryのトップレベル（path .）とする
      - 製品リポジトリtanb/dialogueは配布物のみとし内部統治インスタンスを含めない
    evidence: >-
      https://github.com/tanb/dialogue-dogfoodingをつくってあります。
      こちらのトップレベルをpathに指定してよいです。Aでおねがいします。
targets:
  - id: STATE-SELF-HOSTING-001
    action: update
    before_revision: 4
    after_revision: 5
    result: applied
    error: null
reason: >-
  配布物にDialogue内部の統治インスタンスを含めないため、Knowledgeを独立Private Repository
  tanb/dialogue-dogfooding へ分離し、.dialogue.ymlをそのトップレベルへ向ける。
applied_at: "2026-07-18T05:00:00+09:00"
applied_by: agent:claude
---

# Knowledgeを独立Repositoryへ分離する

## Applied changes

### 知識リポジトリ（tanb/dialogue-dogfooding）
- `dogfooding/`配下の全governed文書（docs / proposals / changes / governance / AGENTS.md）をトップレベルへ移送。
- `STATE-SELF-HOSTING-001` rev4→5：source topology を co-located → separate-repository、remote を `tanb/dialogue-dogfooding.git`、Knowledge root を `.` へ。

### 製品リポジトリ（tanb/dialogue、別PRで適用）
- `dogfooding/`を削除。
- `.dialogue.yml`を `url: https://github.com/tanb/dialogue-dogfooding.git`、`path: .` へ。
- `protocol/knowledge-governance.md`・`protocol/protocol-conformance.md`の`related`から、知識リポジトリへ移った id（PROPOSAL-0017/CHANGE-0017/CHANGE-0011）を除去。
- `scripts/validate_repository.py`：`validate_documents()`のスキャンを`protocol/*.md`のみに、`validate_authority()`（自己スキャン）を撤去。
- `tests/test_knowledge_source.py`のdocument_root assertionを`.`へ。
- `AGENTS.md`・`README.md`の`dogfooding/`参照を独立Repository前提へ更新。

## Rationale

skills.shと.claude-pluginはリポジトリ丸ごとを配布するため、co-locatedではDialogue内部の統治インスタンスが全ユーザーへ渡る。分離により製品を配布物のみにし、同時にDialogueの主用途（独立Knowledge Repository）をDogfoodingする。

## Impact

- 配布物にDialogue内部の統治インスタンス（43文書＋uid束縛）が含まれなくなる。
- DialogueのDogfoodingは「製品のSkill／check-authorityを、この独立Knowledge Repositoryに対して回す」形になり、ユーザーと同じ使い方になる。
- CHANGE-0009のco-located採用をsupersede。歴史的記録は保持。
