---
id: CHANGE-0011
type: change_record
title: 検証ツールとProduct SkillスクリプトをRubyからPythonへ全面移行する
status: applied
scope:
  project: dialogue
  domain: governance
  subject: protocol-conformance
revision: 1
created_at: "2026-07-17T22:55:37+09:00"
updated_at: "2026-07-17T22:55:37+09:00"
created_by: agent:claude
updated_by: agent:claude
related:
  - CONFORMANCE-001
  - STATE-MVP-GIT-E2E-VALIDATION-001
  - CHANGE-0010
extensions:
  approval_source: direct_user_instruction
  toolchain: python-uv
  change_set_id: CHANGESET-0011
change_class: C3
decision: approved
approvals:
  - approval_id: APPROVAL-0011
    actor_ref: person:project-owner
    decision: approved
    subject_revision: 1
    decided_at: "2026-07-17T22:55:37+09:00"
    conditions: []
    evidence: >-
      1でお願いします。またさらにRubyを完全排除まで進めたいです。
targets:
  - id: CONFORMANCE-001
    action: update
    before_revision: 4
    after_revision: 5
    result: applied
    error: null
  - id: STATE-MVP-GIT-E2E-VALIDATION-001
    action: update
    before_revision: 1
    after_revision: 2
    result: applied
    error: null
reason: >-
  検証スタックをPython/uvへ統一し、環境再現性を確保するため、Ruby実装の検証スクリプトと
  Product Skillスクリプトを廃止してPythonの参照実装に置き換える
applied_at: "2026-07-17T22:55:37+09:00"
applied_by: agent:claude
---

# 検証ツールとProduct SkillスクリプトをRubyからPythonへ全面移行する

## Applied changes

- 参照オラクル`check-conformance.rb`を廃止し、`scripts/check_conformance.py`を唯一のConformanceランナーとした。
- `validate-repository.rb`を`scripts/validate_repository.py`へ移植した。
- Product Skillの`scripts/resolve-source`をRubyからPython（PyYAML依存）へ書き換えた。
- 検証ハーネスをpytestに一本化し、Ruby/Pythonパリティテストを撤去した。
- CIからRubyツールチェーンを除去し、uvのみで検証する構成にした。
- `CONFORMANCE-001`（参照オラクルとコマンド）と`STATE-MVP-GIT-E2E-VALIDATION-001`（test_file・再現手順）を現状へ更新した。

## Rationale

`.knowledge.yml`によるGit Knowledge Repository discoveryとConformance検証はProduct v1の主導線である。検証・スクリプトのRuby実装は環境依存が固定されておらず、uvによるPython環境で再現性を担保する方針に統一する。Conformance YAMLは言語中立の契約のままで、ランナー言語のみ変更する。入力の意味と期待結果は弱めていない。

## Impact

- リポジトリからRuby実行系への依存が消え、検証はPython 3 + uvで完結する。
- Product Skillの`resolve-source`はPython 3とPyYAMLを必要とする。
- Conformanceケース、Protocol仕様の安全判断、必須観測結果は不変。
