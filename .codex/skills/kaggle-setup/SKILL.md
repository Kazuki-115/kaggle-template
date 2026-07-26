---
name: kaggle-setup
description: ユーザーが Kaggle のコンペ URL や名前を渡して、そのコンペ用の初期セットアップを進めたいときに使う。AGENTS.md、docs/overview.md、docs/data.md を作成し、overview page と data page の要点をローカルに整理する。
---

# Kaggle Setup

Kaggle コンペ用の初期セットアップとして、`AGENTS.md`、`docs/overview.md`、`docs/data.md` を作成する。

## 使うタイミング

次のときに使う。

- ユーザーが Kaggle のコンペ URL を渡したとき
- コンペを始める前に repo の初期ドキュメントを埋めたいとき
- コンペ概要をローカルのドキュメントにまとめたいとき
- データページの内容もざっくりローカルに残したいとき
- `AGENTS.md` や repo の初期ドキュメントを埋めたいとき

`README.md` の CLI メモだけを更新したい場合には使わない。

## 手順

1. コンペの識別子を次の優先順で特定する。
   - ユーザーが渡した Kaggle competition URL
   - ユーザーが渡した competition slug
2. URL も slug も無ければ、まずユーザーに Kaggle competition URL を渡すよう求める。
3. 受け取った URL をもとに、まず `AGENTS.md` の先頭文、`Goal`、`Links` を埋める。
4. Kaggle の overview page を見て、少なくとも以下を集め、`docs/overview.md` にまとめる。
   - コンペ名
   - 目的の一文要約
   - Description
   - Evaluation
   - Timeline
5. Kaggle の data page を見て、少なくとも以下を集め、`docs/data.md` にまとめる。
   - data page に書かれているファイル一覧
   - data page の説明文からわかる範囲で各ファイルの中身の概要
   - target や提出に関係する列やファイル
   - simulator / SDK の有無

## 出力ルール

- `docs/overview.md` と `docs/data.md` は短く、見返しやすく書く。
- Kaggle の overview page にある見出しを優先して整理する。
- Data の詳細は `docs/data.md` に寄せ、`docs/overview.md` はコンペ全体の要約に留める。
- 推測で埋めず、確認できない項目は `TBD` と書く。
- Kaggle competition URL が無いまま作業を進めない。
- データを勝手にダウンロードしない。`kaggle competitions download` や類似操作は、この skill の処理に含めない。
- `docs/overview.md` は `Description`、`Evaluation`、`Timeline`、`Links` を基本にする。
- `docs/data.md` では、data page の説明文から読み取れる範囲で、まずファイル一覧を書き、可能なら各ファイルの役割や中身を一行で添える。
- `docs/data.md` の見出しは data page の実態に合わせて増減してよい。
- `AGENTS.md` にはコンペ名が入った先頭文、`Goal`、`Links` を残し、何のコンペかと `Competition` / `Overview` / `Data` / `Code` / `Discussion` をすぐ参照できる状態にする。
- 既存ファイルの細かい更新方針はこの skill に持たせず、その場の Codex が判断する。

## リソース

- テンプレート: `references/overview-template.md`
