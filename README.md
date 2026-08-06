# dotfiles

dotfiles管理リポジトリ。

## Managed Files

| ファイル               | 説明                             |
| ---------------------- | -------------------------------- |
| `claude/`              | Claude Code 設定・ルール・スキル |
| `git/ignore`           | git の global excludes           |
| `vscode/settings.json` | VSCode ユーザー設定              |

シンボリックリンクの対応:

| リンク元（リポジトリ） | リンク先                                                           |
| ---------------------- | ------------------------------------------------------------------ |
| `claude/`              | `~/.claude/` 配下3点（[`claude/README.md`](claude/README.md) 参照） |
| `git/ignore`           | `~/.config/git/ignore`                                             |

`vscode/settings.json` はパスが OS 依存のため symlink せず手動配置する。

## セットアップ

- **Claude Code** … [`claude/README.md`](claude/README.md) を参照
- **git** … 下記を実行する。`~/.config/git/ignore` は git が既定で読む global excludes なので `core.excludesfile` の設定は不要
- **VSCode** … `vscode/settings.json` を `~/Library/Application Support/Code/User/settings.json` へ手動でコピーする

```sh
DOTFILES="$HOME/Projects/personal/dotfiles"

mkdir -p "$HOME/.config/git"
ln -sf "$DOTFILES/git/ignore" "$HOME/.config/git/ignore"
```

## 前提

作業端末は個人・業務ともに Mac。Windows 向けの差分は管理しない。

`vscode/settings.json` は `editor.fontFamily` に Operator Mono を指定しているため、未インストールの端末ではフォント指定のみ効かない。

### 必須拡張機能

- `Catppuccin.catppuccin-vsc` — カラーテーマ
- `Catppuccin.catppuccin-vsc-icons` — アイコンテーマ
- `esbenp.prettier-vscode` — フォーマッター
- `dbaeumer.vscode-eslint` — ESLint
