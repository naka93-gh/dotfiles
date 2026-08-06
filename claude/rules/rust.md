---
paths:
  - "**/*.rs"
---

## Rust
- 変更後に `cargo fmt` と `cargo clippy` を実行する
- release プロファイルは `opt-level = "s"` + `lto = true` + `codegen-units = 1` + `strip = true` を既定にする（サイズ半減・速度劣化なし。`opt-level = "z"` は速度劣化が大きく不採用）
- CLI は clap、エラーは thiserror、シリアライズは serde を既定とし、既存プロジェクトの流儀に合わせる
- 公開 API の型は明示する
- 1ファイルの行数目安は実装行で数える（`#[cfg(test)]` のテストは別カウント。テスト込みなら 500〜600 まで許容）
