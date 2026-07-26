# AGENTS.md

## Competition

- Name: `{{competition_name}}`
- URL: `{{competition_url}}`
- Goal: `{{competition_goal}}`

## First Step

作業を始める前に、まず以下を確認すること。

1. `docs/overview.md` を読んでコンペ概要を理解する
2. competition page を見て、目的・評価指標・提出形式・期限を確認する
3. `README.md` を見て、必要な Kaggle CLI コマンドと VS Code 接続手順を確認する
4. `data/` の中身を確認して、どのファイルから見るべきか整理する

## Working Rules

- まずコンペ概要を理解してから実装に入る
- コンペ固有の要点は `docs/overview.md` にまとめる
- データは基本的に `data/` 配下へ置く
- 提出ファイルや中間生成物は `output/` 配下へ置く
- Kaggle に push する Notebook は `kernel-metadata.json` と同じディレクトリに置く
- API キーや個人設定はリポジトリに commit しない
