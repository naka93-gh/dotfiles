## TypeScript
- `strict` を有効化。`any` を避け、型を省略しない
- import スタイル:
  - プロジェクト内モジュール（値）は名前空間 import: `import * as format from "./format"`
  - ライブラリは名前付き import: `import { Component } from "@angular/core"`
  - 型のみは `import type`: `import type { User } from "./types"`
  - 関数は名前空間で修飾し短い名前にする（`format.fileSize`、`format.formatFileSize` としない）
- フォーマット/Lint はプロジェクト設定（Biome / ESLint + Prettier 等）に従う
