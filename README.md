# kaggle-template

Kaggle コンペをローカルと Kaggle Notebook の両方で回しやすくするための最小テンプレートです。

この README は `kaggle` CLI がすでに使えて、`kaggle.json` も準備済みである前提で、毎回忘れやすい最低限コマンドだけをすぐ見返せるようにしています。

## 想定ディレクトリ

```text
.
├── AGENTS.md
├── README.md
├── output/
│   └── .gitkeep
├── src/
│   └── a.ipynb
└── data/
    └── .gitkeep
```

## このテンプレートから新規ディレクトリを作る

ひな形としてコピーして使う:

```bash
cp -R ~/kaggle/kaggle-template ~/kaggle/<new-project-name>
cd ~/kaggle/<new-project-name>
```

コピー後にやること:

```bash
# 必要なら git 初期化
git init

# 対象コンペのデータ取得
kaggle competitions download -c <competition-name> -p data/
```

## 使うコマンド

```bash
# コンペや一覧確認
kaggle competitions list
 
# コンペデータ取得
kaggle competitions download -c <competition-name> -p data/


# 既存 Notebook を pull
# `-m` 付きで metadata も一緒に取る
kaggle kernels pull <owner>/<kernel-name> -m


# ローカル Notebook を Kaggle に push
# Notebook と kernel-metadata.json を同じディレクトリに置く
kaggle kernels push -p .

# Notebook の実行状態を見る
kaggle kernels status <owner>/<kernel-name>

# submission を送る
kaggle competitions submit -c <competition-name> -f <submission-file> -m "message"


# zip 展開
unzip data/<downloaded-file>.zip -d data/
```




## Kaggle の GPU 環境に VS Code から接続する

2025-05-13 公開の参考記事では、Kaggle Notebook の `Kaggle Jupyter Server` を VS Code / Cursor から直接使う流れが紹介されています。

手順:

1. Kaggle で Notebook を新規作成する。
2. `Accelerator` で GPU を選ぶ。
3. Notebook セッションを起動する。
4. `Kaggle Jupyter Server` から `VSCode Compatible URL` をコピーする。
5. VS Code で任意の `.ipynb` を開く。
6. `Select Another Kernel...` → `Existing Jupyter Server...` を選ぶ。
7. コピーした URL を貼り、Kaggle 側の Python Kernel を選ぶ。

接続確認の定番:

```python
!nvidia-smi
```

ローカル PC に GPU がなくても、Kaggle 側の GPU セッションで実行できます。

## メモ

- この README は `kaggle` CLI と `kaggle.json` の準備が終わっている前提です。
- `kaggle kernels push` は `kernel-metadata.json` 前提です。
- `kaggle competitions submit` は Notebook の push とは別操作です。
- `data/` はローカル作業用の置き場として使い、必要に応じて `.gitignore` で中身を無視します。
- `output/` は submission ファイルや中間生成物の置き場として使います。
- VS Code 接続は Kaggle Notebook 側で Jupyter Server セッションが起動している必要があります。

## 参考

- [〖Kaggle API〗 VSCode で Kaggle する](https://zenn.dev/yuto_mo/articles/5c5311a83892b2)
- [Kaggle の Notebook 環境を VS Code (Cursor) で触りたい](https://zenn.dev/prgckwb/articles/kaggle-vscode-link)
