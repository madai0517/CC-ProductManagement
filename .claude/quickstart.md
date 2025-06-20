# 🚀 クイックスタートガイド

このガイドでは、claude-agentsを初めて使う方向けに、詳細な手順を説明します。

## 📦 インストール詳細

### 前提条件の確認

```bash
# Node.jsバージョン確認
node --version  # v14.0.0以上が必要

# tmux確認
tmux -V  # tmuxがインストールされているか確認

# Claude Code確認
which claude  # Claude Codeがインストールされているか確認
```

### インストール手順

#### macOS
```bash
# Homebrewがない場合
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 必要ツールのインストール
brew install node tmux
```

#### Ubuntu/Debian
```bash
# システムアップデート
sudo apt update

# Node.jsとnpmのインストール
sudo apt install nodejs npm

# tmuxのインストール
sudo apt install tmux
```

#### Windows (WSL2)
```bash
# WSL2でUbuntuをインストール後、上記Ubuntu手順を実行
```

### Claude Codeのインストール

1. [claude.ai/code](https://claude.ai/code) にアクセス
2. お使いのOSに合わせてダウンロード
3. インストーラーの指示に従ってインストール
4. ターミナルで `claude` コマンドが使えることを確認

## 🎯 詳細な使用例

### Business Strategy シナリオの完全ガイド

#### 1. プロジェクトセットアップ

```bash
# 作業ディレクトリの作成
mkdir ~/my-ai-strategy && cd ~/my-ai-strategy

# claude-agentsの初期化
claude-agents init --scenario business-strategy
```

初期化時の出力例：
```
✨ claude-agents v2.0.0 初期化
🎭 シナリオ: Business Strategy Discussion
📁 設定ファイル生成: claude-agents.yaml
✅ 初期化完了！
```

#### 2. エージェントの起動

```bash
# tmuxセッションとエージェントを起動
claude-agents start
```

起動時の出力例：
```
🚀 Starting agents for scenario: business-strategy
✅ Created tmux session: strategy (4 panes)
✅ Created tmux session: analysis (2 panes)
✅ Generated agent mapping file

📋 次のステップ:
1. 各tmuxペインでClaude Codeを起動してください
2. 最初のペインで認証を完了してください
3. エージェントに初期指示を送信してください
```

#### 3. Claude Codeの起動

```bash
# 戦略チームセッションにアタッチ
tmux attach-session -t strategy
```

各ペインで以下を実行：
1. `Ctrl+b` → `1` でペイン1（CEO）に移動
2. `claude` と入力してEnter
3. 認証プロセスを完了
4. 他のペインでも同様に実行

#### 4. 戦略会議の開始

CEOペイン（左上）で以下を入力：
```
あなたはCEOです。AI技術への投資について戦略会議を開始します。
技術的実現可能性、財務影響、市場機会について各専門家の意見を求めてください。
```

#### 5. エージェント間の対話

別のターミナルウィンドウから：
```bash
# CTOに技術評価を依頼
claude-agents send cto "技術仕様の詳細レポートを作成してください"

# CFOに財務分析を依頼
claude-agents send cfo "3年間の投資計画を策定してください"

# 分析チームに市場調査を依頼
claude-agents send data_analyst "競合他社の分析データを提供してください"
```

### Collaborative Coding シナリオ

```bash
# 初期化
claude-agents init --scenario collaborative-coding

# 起動
claude-agents start

# 開発チームセッションにアタッチ
tmux attach-session -t development

# アーキテクトに設計を依頼
claude-agents send tech_lead "新機能のアーキテクチャを設計してください"

# フロントエンド開発者にUI実装を依頼
claude-agents send frontend_dev "ユーザーインターフェースを実装してください"
```

## 🎬 実践的なユースケース

### ケース1: 新製品開発会議

```bash
# Product Developmentシナリオで開始
claude-agents init --scenario product-development
claude-agents start

# プロダクトマネージャーから開始
tmux attach-session -t product_development
# PMペインで: "新しいAIアシスタント製品の開発を開始します..."

# 各専門家への指示
claude-agents send ux_designer "ユーザージャーニーマップを作成してください"
claude-agents send system_architect "スケーラブルなアーキテクチャを提案してください"
```

### ケース2: 市場分析プロジェクト

```bash
# Market Analysisシナリオ
claude-agents init --scenario market-analysis
claude-agents start

# 戦略コンサルタントから分析開始
claude-agents send strategic_consultant "AI市場の包括的分析を開始してください"
```

## 🔍 デバッグとトラブルシューティング

### 状態確認コマンド

```bash
# システム全体の状態
claude-agents status --all

# tmuxセッションの詳細
tmux list-sessions
tmux list-panes -t strategy

# エージェントマッピング確認
cat tmp/agent_mapping.json

# 送信ログ確認
tail -f logs/send_log.jsonl
```

### よくある問題の解決

#### tmuxセッションが見つからない
```bash
# セッションリセット
claude-agents reset
claude-agents start
```

#### エージェントが応答しない
```bash
# 特定のペインに直接アクセス
tmux send-keys -t strategy:1.2 "メッセージ" C-m
```

#### Claude Code認証エラー
```bash
# 手動で各ペインで認証
tmux attach-session -t strategy
# 各ペインで claude コマンドを実行
```

## 📚 次のステップ

- [カスタムシナリオ作成ガイド](.claude/custom-scenarios.md)
- [高度な設定オプション](.claude/architecture.md)
- [開発者向けAPI](.claude/development.md)

---

詳細な技術情報や高度な使い方については、[.claude/](.claude/)ディレクトリ内のドキュメントを参照してください。