# Tsumiki - AI駆動開発支援フレームワーク

TsumikiはAI駆動開発のためのフレームワークです。要件定義から実装まで、AIを活用した効率的な開発プロセスを提供します。

基本的にClaude Codeをサポートしますが、それ以外のツールでも使用できます。[Claude Code以外のツールでtsumikiを使用する](#claude-code以外のツールでtsumikiを使用する) を参照してください。

## インストール

Tsumikiを使用するには、次のClaude Code Pluginコマンドでインストールしてください：

```bash
/plugin marketplace add https://github.com/classmethod/tsumiki.git
/plugin install tsumiki@tsumiki 
```

このコマンドを実行すると、TsumikiのClaude Codeスラッシュコマンドとエージェントが自動的にインストールされます。

**注意**: コマンドは `/tsumiki:` プレフィックス付きで実行します（例：`/tsumiki:kairo-requirements`）。

## 概要

Tsumikiは以下の2つのコマンドで構成されています：

- **kairo** - 要件定義から実装までの包括的な開発フロー
- **tdd** - テスト駆動開発（TDD）の個別実行

### Kairoコマンド

Kairoは要件定義から実装までの開発プロセスを自動化・支援します。以下の開発フローを支援します：

1. **要件定義** - 概要から詳細な要件定義書を生成
2. **設計** - 技術設計文書を自動生成
3. **タスク分割** - 実装タスクを適切に分割・順序付け
4. **TDD実装** - テスト駆動開発による品質の高い実装

## 利用可能なコマンド

- `init-tech-stack` - 技術スタックの特定

### Kairoコマンド（包括的開発フロー）
- `kairo-requirements` - 要件定義
- `kairo-design` - 設計文書生成
- `kairo-tasks` - タスク分割
- `kairo-implement` - 実装実行

### TDDコマンド（個別実行）
- `tdd-requirements` - TDD要件定義
- `tdd-testcases` - テストケース作成
- `tdd-red` - テスト実装（Red）
- `tdd-green` - 最小実装（Green）
- `tdd-refactor` - リファクタリング
- `tdd-verify-complete` - TDD完了確認

### リバースエンジニアリングコマンド

- `rev-tasks` - 既存コードから機能単位でタスク一覧を逆生成
- `rev-design` - 既存コードから設計文書を逆生成
- `rev-specs` - 既存コードからテスト仕様書を逆生成
- `rev-requirements` - 既存コードから要件定義書を逆生成

## クイックスタート

**注意**: Claude Code Pluginでインストールした場合は、各コマンドの先頭に `tsumiki:` を付けてください（例：`/tsumiki:kairo-requirements`）。

### 包括的な開発フロー

```bash
# 1. 技術スタック初期化
/tsumiki:init-tech-stack

# 2. 要件定義
/tsumiki:kairo-requirements

# 3. 設計
/tsumiki:kairo-design

# 4. タスク分割
/tsumiki:kairo-tasks

# 5. 実装
/tsumiki:kairo-implement
```

### 個別TDDプロセス

```bash
/tsumiki:tdd-requirements
/tsumiki:tdd-testcases
/tsumiki:tdd-red
/tsumiki:tdd-green
/tsumiki:tdd-refactor
/tsumiki:tdd-verify-complete
```

### リバースエンジニアリング

```bash
# 1. 既存コードからタスク構造を分析
/tsumiki:rev-tasks

# 2. 設計文書の逆生成（タスク分析後推奨）
/tsumiki:rev-design

# 3. テスト仕様書の逆生成（設計文書後推奨）
/tsumiki:rev-specs

# 4. 要件定義書の逆生成（全分析完了後推奨）
/tsumiki:rev-requirements
```

## Claude Code以外のツールでtsumikiを使用する

[rulesync](https://github.com/dyoshikawa/rulesync)を組み合わせて使用することで、Claude Code以外のツールでもtsumikiのコマンドを使用できます。

プロジェクトルートで以下のコマンドを実行します。

```
npx -y rulesync init
npx -y rulesync config --init
npx -y rulesync import \
  --targets claudecode \
  --features commands,subagents

# Gemini CLIのカスタムスラッシュコマンドを出力する場合は以下のようになります。
# （`--targets` には `claudecode`, `geminicli`, `roo` の指定が可能です）
npx -y rulesync generate \
  --targets geminicli \
  --features commands

# カスタムスラッシュコマンドの仕様が存在しない（または仕様的な制限のある）AIコーディングツールでも、 `--experimental-simulate-commands` フラグによりいくつかのツールではコマンドファイルを出力できます。
# Cursorのカスタムスラッシュコマンドを出力する場合は以下のようになります。
# （`--targets` には `cursor`, `copilot`, `codexcli` の指定が可能です）
npx -y rulesync generate \
  --targets cursor \
  --features commands
  --experimental-simulate-commands
```

詳しくは[rulesync](https://github.com/dyoshikawa/rulesync)のREADMEを参照してください。

## 詳細なマニュアル

使用方法の詳細、ディレクトリ構造、ワークフロー例、トラブルシューティングについては [MANUAL.md](./MANUAL.md) を参照してください。
