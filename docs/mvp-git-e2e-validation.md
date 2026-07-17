---
id: STATE-MVP-GIT-E2E-VALIDATION-001
type: state
title: MVP Git Knowledge Repository E2E Validation
status: active
scope:
  project: dialogue
  domain: validation
  subject: mvp-git-e2e
revision: 2
created_at: "2026-07-16T04:09:27+09:00"
updated_at: "2026-07-17T22:55:37+09:00"
created_by: agent:codex
updated_by: agent:claude
related:
  - STATE-PRODUCT-SCOPE-001
  - PROPOSAL-0006
  - CHANGE-0006
  - CHANGE-0011
canonical_for: dialogue/validation/mvp-git-e2e
owners:
  - person:project-owner
extensions:
  verdict: passed
  environment: local-temporary-git
  test_file: tests/test_knowledge_git_e2e.py
---

# MVP Git Knowledge Repository E2E Validation

## Verdict

`.dialogue.yml`からGit Knowledge Repositoryを発見し、参照、編集、Change Record作成、push、別checkoutでの再取得までのMVP機構は、ローカル一時Git remote上で成功した。

## Executed scenario

```text
Project/.dialogue.yml
→ resolve-source
→ local bare Git remote
→ Agent checkout
→ Active State read
→ State revision update + Change Record creation
→ commit + push
→ independent verifier clone
→ updated knowledge and commit verification
```

別シナリオで二つのcheckoutを同じ`main`から作成し、一方のpush後に他方の古いpushがnon-fast-forwardとして拒否されることも確認した。

## Observations

- ResolverはGit URL、`main` ref、`knowledge` document rootを返した。
- Clone後の`remote.origin.url`は設定URLと一致した。
- `status: active`、`revision: 1`のStateを読み取れた。
- Stateを`revision: 2`へ更新し、変更前後と理由を持つChange Recordを追加した。
- Commitをbare remoteへpushできた。
- 別cloneから更新State、Change Record、commit messageを確認できた。
- Project Repository側へKnowledge文書は生成されなかった。
- Stale checkoutからのpushは拒否され、remoteの最新commitは維持された。

## Test result

```text
test_knowledge_git_e2e.py: 2 passed
```

## Not yet validated

- GitHub、GitLabなど実ホスティングサービスの認証と権限
- SSH agent、credential helper、token失効時の応答
- ネットワーク切断、rate limit、大容量Repository
- 実AgentがSkillだけを与えられて行う独立forward test
- 複数人の意味上の編集競合とmerge運用

## Reproduction

```sh
cd development && uv run pytest tests/test_knowledge_git_e2e.py
```
