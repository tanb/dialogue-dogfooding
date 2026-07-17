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

The MVP mechanism of discovering the Git Knowledge Repository from `.dialogue.yml`, referencing, editing, creating a Change Record, pushing, and re-fetching from a separate checkout succeeded on a local temporary Git remote.

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

In a separate scenario, two checkouts were created from the same `main`, and it was also confirmed that after one pushed, the other's stale push was rejected as a non-fast-forward.

## Observations

- The Resolver returned the Git URL, the `main` ref, and the `knowledge` document root.
- After the clone, `remote.origin.url` matched the configured URL.
- A State with `status: active` and `revision: 1` could be read.
- The State was updated to `revision: 2`, and a Change Record with the before/after and reason was added.
- The commit could be pushed to the bare remote.
- The updated State, Change Record, and commit message could be confirmed from a separate clone.
- No Knowledge document was generated on the Project Repository side.
- A push from a stale checkout was rejected, and the latest commit of the remote was preserved.

## Test result

```text
test_knowledge_git_e2e.py: 2 passed
```

## Not yet validated

- Authentication and permissions of real hosting services such as GitHub and GitLab
- SSH agent, credential helper, and the response on token revocation
- Network disconnection, rate limit, and large-capacity Repository
- An independent forward test that a real Agent performs given only the Skill
- Semantic edit conflicts among multiple people and merge operations

## Reproduction

```sh
cd development && uv run pytest tests/test_knowledge_git_e2e.py
```
