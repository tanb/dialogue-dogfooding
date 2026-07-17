# Dialogue Knowledge Guide

このディレクトリは`.dialogue.yml`が指定するDialogueのKnowledge rootである。

## Document layout

- `docs/`: 現在状態、仕様補助、検証結果
- `governance/`: Authority Registryと運用上の権限
- `proposals/`: 未決定または承認対象の意味変更
- `changes/`: 適用済み変更の意味上の履歴

## Read protocol

1. 対象scopeのActiveなStateとAuthority Registryを確認する。
2. Proposalを現在状態として扱わない。
3. 変更経緯が必要な場合だけ関連Change Recordを読む。
4. Archivedな知識は明示的な履歴調査以外で使用しない。
5. 一意な正本を解決できなければ更新せずエスカレーションする。

## Write protocol

1. 書込み前にremoteの`main`を同期し、対象revisionを再確認する。
2. 確定した意味変更ではStateと独立したChange Recordを更新する。
3. C3またはC4はHuman Approvalの対象とrevisionを記録する。
4. AppliedなChange Recordを後から上書きしない。訂正は新しい変更として記録する。
5. `cd development && uv run python scripts/validate_repository.py`で検証してからpushする。
