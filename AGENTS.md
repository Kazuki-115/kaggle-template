# AGENTS.md

このディレクトリは Kaggle コンペ開始時のテンプレートとして使う。

## 目的

- Kaggle CLI の操作を毎回調べ直さない
- Notebook の pull / push / submit 手順をすぐ参照できる
- ローカル作業と Kaggle GPU 作業を切り替えやすくする

## 作業ルール

- まず `README.md` を見て、CLI 操作と接続手順を確認する
- データは基本的に `data/` 配下へ置く
- Kaggle に push する Notebook は `kernel-metadata.json` と同じディレクトリに置く
- API キーや個人設定はリポジトリに commit しない

## 最初にやること

1. Kaggle CLI が入っているか確認する
2. `kaggle.json` または `KAGGLE_CONFIG_DIR` を設定する
3. 対象コンペのデータを `data/` に落とす
4. 必要なら Notebook を pull してローカルで編集する

## 将来の拡張候補

- `notebooks/` を作る
- `src/` を作る
- `Makefile` か `justfile` で定番コマンドをまとめる
- `kernel-metadata.json` の雛形を置く
