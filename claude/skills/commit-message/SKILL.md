---
name: commit-message
description: 現在の変更（staged 優先、なければ unstaged）からコミットメッセージ案を提示する。Claude は commit を実行せず、案だけを出す
user-invocable: true
allowed-tools: Bash(git *), Read
---

## 差分の取得

1. !`git status --short`
2. staged があれば優先:
   - !`git diff --cached --stat`
   - !`git diff --cached`
3. staged が空なら unstaged を対象に:
   - !`git diff --stat`
   - !`git diff`

差分がなければ「コミット対象なし」と伝えて終了する。

## スタイルの把握

!`git log --oneline -20 2>/dev/null || echo "(コミット履歴なし)"`

履歴があれば、リポジトリのコミットスタイル（プレフィックス、言語、粒度）を読み取り、それに合わせる。
例: `chore: ...` / `docs: ...` / `feat: ...` のような Conventional Commits 風か、自由形式か、日本語か英語か、など。

履歴が無い場合（初回コミット前など）はコケずに進める。共通ルールの Conventional Commits（`type: 説明`、type は英語・説明は日本語）を既定スタイルとして採用する。

## メッセージの方針

- 件名は何をしたかを 1 行で（リポジトリのスタイルに従う）
- 必要なら本文で Why を 1〜3 行
- 複数の論点が混ざっている場合は「分割した方がよい」と提案する
- staged が大きく分割可能なら、複数コミットへの分け方も併記する

## 出力フォーマット

1〜3 案を提示する。各案は次の形式:

```
### 案 N

<件名>

<本文 (必要なら)>
```

末尾に「なぜこの粒度・プレフィックスを選んだか」を 1 行添える。

## 実行しない

ユーザーが自分でコミットするため、Claude は `git commit` を呼ばない。案を提示するところまでで止める。
