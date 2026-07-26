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
rsync -a --exclude '.git' ~/kaggle/kaggle-template/ ~/kaggle/<new-project-name>/
cd ~/kaggle/<new-project-name>
```

コピー後にやること:

```bash
# skills を使って setup をする

$kaggle-setup <competition_url>
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

## Kaggle Notebook のセッション制限メモ

2026-07-26 時点で把握しておきたい点:

- GPU 利用枠は週次 quota 制です。
- Kaggle の公式 docs では、GPU は `週 30 時間、または需要とリソース状況に応じてそれ以上` と案内されています。
- interactive session は、操作しないまま放置すると `60 分` の idle timeout で切れます。
- Kaggle の competition page では、Notebook 実行時間の上限として `CPU/GPU は 12 時間`、`TPU は 9 時間` と書かれていることがあります。

運用上の注意:

- VS Code から接続していても、元の Kaggle Notebook session が切れると接続は使えなくなります。
- GPU を使わないときは accelerator を切るか session を止めるほうが quota の無駄が少ないです。
- ブラウザを閉じる前に session を明示的に stop すると、最大で 60 分ぶんの無駄な消費を避けやすいです。
- 長い学習は interactive 接続前提にせず、`kaggle kernels push` で batch 実行するほうが安定します。

確認先:

- GPU quota や idle timeout は Kaggle docs を見る
- 実行時間上限は参加中 competition の page / rules / evaluation notes も確認する

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
- [Kaggle docs: Efficient GPU Usage Tips](https://www.kaggle.com/docs/efficient-gpu-usage)
