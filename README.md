# casebrief-lite

小さな修正（バグ修正、数ファイルの機能追加、仕様の微調整）について、**テスト観点**と**設計の入り口**を 1 画面ぶん出す Claude Code の skill です。

## 出力

1. **変更の要約**: 何を・なぜ、影響範囲と波及先、既存テスト
2. **設計の入り口**: 推奨の方針と代案、触る場所、判断が分かれる点
3. **テスト観点**: 5〜7 個が目安、最大 10 個。各観点に具体例（条件 → 期待）、技法、層（unit / integration / e2e / 手動）、優先度
4. **仮定と確認事項**: 仕様に無い期待は仮定として書き、依存する観点の番号を付ける

## 使い方

```text
/casebrief-lite                  # 未コミットの差分と未追跡ファイル
/casebrief-lite main...          # コミット範囲
/casebrief-lite feature/x        # ブランチ（既定ブランチとの差分）
/casebrief-lite #123             # PR
/casebrief-lite issue 45         # Issue（まだコードが無い修正）
/casebrief-lite 一覧の並び順を更新日時の降順に変えたい
```

skill は利用者が呼んだ時だけ動きます（`disable-model-invocation: true`）。「テスト設計を作って」と頼んだ時に、casebrief の代わりに誤って起動しないようにするためです。

## インストール

plugin として入れる場合:

```text
/plugin marketplace add mozuq-lab/casebrief-lite
/plugin install casebrief-lite@casebrief-lite
```

plugin の skill は `/casebrief-lite:casebrief-lite` の名前でも呼べます。

個人 skill として入れる場合（このリポジトリの直下で実行）:

```bash
mkdir -p ~/.claude/skills
ln -s "$(pwd)/skills/casebrief-lite" ~/.claude/skills/casebrief-lite
```

このリポジトリで試す時は `.claude/skills/casebrief-lite`（`skills/casebrief-lite` へのシンボリックリンク）が使われます。

## 構成

| パス                                             | 内容                                                |
| ------------------------------------------------ | --------------------------------------------------- |
| `skills/casebrief-lite/SKILL.md`                 | 手順、出力の型、casebrief 向け source.md の書き出し |
| `skills/casebrief-lite/references/viewpoints.md` | 観点（層を問わないもの、画面のもの）と技法メモ      |
