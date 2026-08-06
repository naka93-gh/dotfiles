## Git

- Git操作（commit/push/branch等）はユーザーが行う。Claudeは実行しない
- Claudeはコミットメッセージの案を出すところまで

## コミットメッセージ

- Conventional Commits: `type: 説明`。typeは英語、説明は日本語
- type: feat/fix/refactor/perf/test/docs/build/chore
- 破壊的変更は`type!:`（例: `refactor!: CLI引数整理`）
- 件名は「何をしたか」を簡潔に
