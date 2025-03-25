# LiveTree

LiveTree は、**リアルタイムでディレクトリ構造を管理・編集できる CLI & Web ツール** です。  
実際のフォルダと同期し、ツリー構造を可視化。CLI と Web UI の両方から操作可能。  
フォルダやファイルにコメントを付与し、ディレクトリの役割を明確にすることもできます。  

さらに、今後のアップデートでは **処理の流れを可視化するビジュアライザー機能** を導入予定。  
**ディレクトリ管理 × コード解析 × 可視化** を統合し、より直感的な開発環境を提供します。

---

## **特長**
### **ディレクトリ管理機能**
- **リアルタイム同期** - 実際のフォルダと常にリンク
- **CLI & Web UI 両対応** - ターミナル操作とブラウザ UI の両方をサポート
- **コメント機能** - フォルダやファイルに説明を付与
- **直感的な管理** - フォルダ構成を把握しやすいツリービュー
- **Git との統合（予定）** - ブランチごとの構成差分を可視化

### **ビジュアライザー機能（開発予定）**
- **関数・メソッドの依存関係を可視化**
- **データフロー（MVC / API / DB）の流れを直感的に表示**
- **D3.js を活用した動的なグラフ描画**
- **ボタン切り替えでディレクトリ構成と処理フローをスムーズに切り替え**
- **Git の diff を視覚化（予定）**

---

## **インストール**

### **1. 依存関係のインストール**
LiveTree は **Python + FastAPI** で構成されています。以下の依存関係をインストールしてください。

```
pip install fastapi uvicorn watchdog
```

また、**Web UI を使用する場合は Node.js のインストールが必要** です。

```
npm install
```

---

## **使い方**

### **1. CLI モード**
指定したディレクトリをリアルタイムで監視し、ツリー構造を表示。

```
python server/main.py [監視ディレクトリ]
```

ディレクトリの変更をリアルタイムで反映。

---

### **2. Web UI モード**
ブラウザからディレクトリ構造を管理・編集。

```
# バックエンド起動
cd server
python main.py

# フロントエンド起動
cd web
npm run dev
```

ブラウザで `http://localhost:3000` にアクセスすると、リアルタイムでディレクトリ構造を編集できます。

---

## **今後のアップデート予定**
### **📌 1. ビジュアライザー機能の追加**
LiveTree は単なるディレクトリ管理ツールにとどまらず、**コードの依存関係や処理フローを視覚化するツールへ進化** します。

#### **🔹 関数の呼び出し関係を可視化**
関数がどこで使われているかを解析し、**D3.js を活用して視覚的に追跡** 可能に。

```
# 解析イメージ（Mermaid 形式）
graph TD;
    index.js -->|calls| utils.js;
    utils.js -->|calls| api.js;
    api.js -->|fetches| database;
```

#### **🔹 データフローの可視化**
MVC や API 連携の流れを図式化し、**処理の流れを直感的に理解できる** ようにします。

```
graph TD;
    UserRequest --> Controller;
    Controller --> Service;
    Service --> Database;
    Database --> Service;
    Service --> Controller;
    Controller --> Response;
```

#### **🔹 Web UI に「ビジュアライザー」モードを追加**
ディレクトリツリーと処理フローを**ボタン1つで切り替え**可能に。

---

### **📌 2. Git との統合**
- **ブランチ間のディレクトリ構成の差分を可視化**
- **Git の `diff` を視覚的に確認できる UI を追加**

---

## **ライセンス**
MIT License


## 技術スタック

| レイヤ | 技術 | 理由 |
|--------|------|------|
| フロントエンド | React + Vite | 高速ビルドと柔軟なUI構築。D3.jsとの相性が良く、開発体験が優れている。 |
| スタイリング | Tailwind CSS | ユーティリティベースでカスタマイズ性が高く、構造の可視化に適する。 |
| 状態管理 | Zustand | シンプルかつ軽量で、ツリービューやビジュアライズの状態管理に向く。 |
| データビジュアライズ | D3.js | ノード・エッジの自由な表現が可能で、処理フローの可視化に最適。 |
| バックエンド | FastAPI (Python) | 高速な非同期API設計が可能で、CLIとの親和性も高い。 |
| ファイル監視 | watchdog | クロスプラットフォーム対応で、ファイル構造のリアルタイム検知に適する。 |
| コード解析 (TS/JS) | ts-morph | TypeScript AST を高レベルで扱える。依存関係解析に使用。 |
| コード解析 (Python) | ast | Python標準ライブラリで構文解析が可能。MVPに十分。 |
| 通信 | WebSocket | クライアントとバックエンドのリアルタイム同期に使用。 |
| ドキュメント可視化 (補助) | Mermaid.js | 処理の流れを軽量に表現する用途に便利（将来的に使用）。 |

---

## 要件・実装予定フロー

### フェーズ 1: ディレクトリ管理ツール（MVP）

#### 機能
- ローカルのディレクトリ構造をリアルタイムに監視
- CLI / Web UI どちらからも操作可能
- フォルダ・ファイルの作成、削除、移動
- コメント（説明）を `.dir_comments.json` に保存・同期
- Web UI にツリー構造を可視化表示

#### 実装の流れ
1. FastAPI による WebSocket サーバの構築（watchdog 連携）
2. React + Zustand で構造ツリーの状態を管理
3. Tailwind CSS でUI設計（ツリービュー、編集欄）
4. CLIベース操作機能の整備（`live-tree` コマンド想定）

---

### フェーズ 2: 処理フロー可視化機能の導入（Visualizer）

#### 機能 A: 関数/メソッド依存関係のビジュアライズ
- AST（ts-morph / ast）を用いて呼び出し関係を解析
- 関数やモジュール同士の依存グラフを D3.js で描画
- ファイルクリックで関数をハイライト、呼び出し元/先を表示

#### 機能 B: データフローの可視化（MVC, API, DB）
- 処理の流れ（Controller → Service → Repository → DB）を視覚化
- ボタンで表示を切り替え（ツリー / 呼び出し関係 / データフロー）
- Mermaid.js による補助的出力にも対応（README等への貼り付け用途）

#### 実装の流れ
1. コード解析モジュールの設計（最初はTS限定、次にPython）
2. 関数/ファイル単位の依存マップをJSONで生成
3. D3.js によるビジュアライズビューの実装
4. 表示モード切替ボタンの導入（Directory / Dependency / Flow）

---

## 今後の拡張候補
- Git ブランチ間のディレクトリ構成比較・差分ビジュアライズ
- `.zip` で構成のエクスポート機能
- Mermaid.js 形式でREADMEに貼れる処理フロー出力
- Web UI のダークモード対応
- プロジェクトテンプレートからの初期構成生成

## インストール

### Python 側（バックエンド）

```
pip install fastapi uvicorn watchdog
```

### Node.js 側（フロントエンド）

```
cd web
npm install
```

---

## 起動方法

### バックエンド起動（ディレクトリ監視 + API）

```
cd server
python main.py
```

### フロントエンド起動（Web UI）

```
cd web
npm run dev
```

ブラウザで `http://localhost:3000` にアクセスすることで、ツリー構造がリアルタイムに表示・編集できます。

---

## フェーズ別の機能構成

### 🟩 フェーズ 1: ディレクトリ管理（MVP）

- [x] ローカルディレクトリの構造ツリーを表示
- [x] CLI での編集機能（作成・削除・移動）
- [x] Web UI からのツリー編集機能
- [x] `.dir_comments.json` による説明文の付加・保存
- [x] WebSocket によるリアルタイム反映
- [ ] フロント側でファイル/フォルダの追加・編集UI

---

### 🟨 フェーズ 2: Visualizer モード（構文解析 + 可視化）

#### モード A: 関数/メソッドの依存可視化
- ts-morph（TS）・ast（Python）による構文解析
- 関数呼び出し/参照関係を D3.js でビジュアライズ
- 関数をクリックして影響範囲を可視化

#### モード B: データフローの可視化（MVC構成など）
- REST API / Controller / Service / DB などの流れを図式化
- `Mermaid.js` やカスタム D3 レイアウトにより、構造を柔軟に表現

---

## 今後の拡張予定

- [ ] Git ブランチ間の構成差分ビジュアライズ
- [ ] `.zip` でプロジェクト構成の一括エクスポート
- [ ] Web UI 上でのファイル編集（コードエディタ統合）
- [ ] ファイル・関数単位でのラベル/タグ管理
- [ ] UIテーマのダークモード対応
- [ ] D3.js 描画部分のパフォーマンス最適化（仮想レンダリング）
- [ ] Web Worker を用いた構文解析処理の並列化
      
live-tree/
├── server/                         # バックエンド（FastAPI + Watchdog）
│   ├── main.py                    # エントリーポイント（API & WebSocket & 監視）
│   ├── file_watcher.py           # watchdog によるディレクトリ監視処理
│   ├── tree_builder.py           # ツリー構造構築ロジック
│   ├── comments_manager.py       # コメント読み書き（.dir_comments.json）
│   ├── websocket.py              # WebSocket接続管理
│   ├── analyzers/                # 処理フローの解析系（Phase 2）
│   │   ├── ts_analyzer.py        # ts-morphベースのTSコード依存解析
│   │   ├── py_analyzer.py        # astベースのPythonコード解析
│   │   └── flow_graph.py         # 共通グラフデータ構造生成
│   └── utils/                    # 汎用ユーティリティ
│       └── path_utils.py
│
├── web/                           # フロントエンド（React + D3.js + Zustand）
│   ├── index.html
│   ├── vite.config.ts
│   ├── src/
│   │   ├── main.tsx              # Reactエントリポイント
│   │   ├── App.tsx               # ルーティングとレイアウト
│   │   ├── stores/               # Zustandステート管理
│   │   ├── components/           # 共通UIコンポーネント
│   │   │   ├── DirectoryTree.tsx # ツリー構造の表示・編集
│   │   │   ├── CommentEditor.tsx # コメント編集UI
│   │   │   ├── GraphView.tsx     # D3での可視化ビュー（Phase 2）
│   │   │   └── ToggleButtons.tsx # Directory / Flow切替
│   │   ├── hooks/                # カスタムフック
│   │   ├── api/                  # バックエンド通信処理
│   │   │   └── websocket.ts
│   │   └── styles/               # Tailwind拡張 or グローバルCSS
│   │       └── globals.css
│   └── public/
│       └── favicon.svg
│
├── cli/                           # CLIコマンド（将来的に分離可能）
│   └── live_tree.py              # `live-tree` 実行時のエントリポイント
│
├── .dir_comments.json            # コメント情報を格納（プロジェクトルートに配置）
├── README.md
├── package.json
├── pyproject.toml                # Python依存管理（Poetry or pip）
└── .gitignore

