---
name: comment-cleanup-diff
description: 変更差分に含まれるコメントを、コメントルールとAIっぽい表現の観点で見直して直す。追加・変更したコメントと、コード変更で古くなった近くのコメントが対象。全体なら comment-cleanup を使う
disable-model-invocation: true
argument-hint: [base-branch]
allowed-tools: Bash(git *), Read, Edit, Grep, Glob
---

変更差分に関わるコメントを見直し、その場で直す。
体裁だけを点検する`format-check`と違い、コメントの要不要と表現まで書き換える。

## 基準

最初に`~/.claude/skills/comment-cleanup/criteria.md`を読み、その基準に従う。

## 対象の取得

引数`$ARGUMENTS`でbaseブランチを受け取れば`<base>...HEAD`と作業ツリーの差分を、無ければ作業ツリーの変更（staged・unstaged・untracked）を対象にする。

- !`git status --short`

規模を見てから読む。

```bash
git diff HEAD --stat            # 引数なし
git diff <base> --stat          # 引数あり
```

対象が無ければ「対象なし」と伝えて終了する。

## 見る範囲

- 差分で追加・変更されたコメント
- 変更したコードの近くにある既存のコメント 古くなっていないかを確かめる
  - 関数の中を変えたら、その関数の宣言コメントも見る
  - 型や関数の名前・挙動を変えたら、それを説明している他の場所のコメントも`Grep`で探す
- それ以外の既存コメントは、ルール違反に気づいても直さずに報告に回す

untrackedのファイルは全体が新規なので、ファイル内のコメントをすべて見る。

## 進め方

1. 差分をファイル単位で読み、前後のコードと一緒にコメントを判断する
2. 1（ルール準拠）と2（表現）を同じ読みで見直して直す
3. criteria.mdの「確認」を行う。コメント以外の差分の確認は、自分が加えた変更について行う（元からあるコード変更は除いて見る）
4. 「報告」の形でまとめる 見る範囲の外で気づいたものは別に挙げる
