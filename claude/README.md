# Claude Code 設定

Claude Code（`~/.claude`）向けの設定・ルール・スキルを管理する。

## 構成

| パス            | 説明                                                                  |
| --------------- | --------------------------------------------------------------------- |
| `CLAUDE.md`     | 全プロジェクト共通の方針（言語非依存）                                |
| `rules/`        | 言語固有のルール（`typescript.md` / `rust.md` / `sql.md`）            |
| `skills/`       | 自作スキル（ワークフロー）                                            |
| `settings.json` | Claude Code のグローバル設定（permissions / model / plugins / theme） |

`rules/` は必要なプロジェクトで参照する。`CLAUDE.md` / `skills/` / `settings.json` はホームへ symlink して有効化する。
端末固有の値や機密は `~/.claude/settings.local.json`（gitignore 対象・Claude Code が別管理）へ置き、ここでは管理しない。

## セットアップ

リポジトリのパスを `DOTFILES` に設定して以下を実行する。

```sh
DOTFILES="$HOME/Projects/personal/dotfiles"

mkdir -p "$HOME/.claude"
ln -sf "$DOTFILES/claude/CLAUDE.md"     "$HOME/.claude/CLAUDE.md"
ln -sf "$DOTFILES/claude/skills"        "$HOME/.claude/skills"
ln -sf "$DOTFILES/claude/settings.json" "$HOME/.claude/settings.json"
```

> [!NOTE]
> `ln -sf` はリンク先の既存ファイル/ディレクトリを上書きする。
> 特に `~/.claude/skills` に既存の自作スキルがあるときは、先に `claude/skills/` へ移してから貼り直す。

> [!NOTE]
> `settings.json` は Claude Code 自身が書き換える（`/config` 等）。書き込み方式によっては symlink が実体ファイルに戻りリンクが切れることがある。
> 設定変更後に管理対象から外れていたら、上の `ln -sf` を再実行して貼り直す。

| リンク元（リポジトリ） | リンク先                  |
| ---------------------- | ------------------------- |
| `claude/CLAUDE.md`     | `~/.claude/CLAUDE.md`     |
| `claude/skills`        | `~/.claude/skills`        |
| `claude/settings.json` | `~/.claude/settings.json` |
