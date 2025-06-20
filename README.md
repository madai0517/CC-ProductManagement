# 🤖 Claude Agents

tmuxを使ったClaude Code間のマルチエージェント協働システム

![Version](https://img.shields.io/badge/version-2.0.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Node](https://img.shields.io/badge/node-%3E%3D14.0.0-brightgreen)

## 📌 概要

複数のClaude Codeインスタンスが連携して、現実的なビジネスシナリオでコラボレーションできるシステムです。

### 🎯 主な特徴

- **5つのビジネスシナリオ**: 戦略会議、開発チーム、市場分析など
- **簡単セットアップ**: 5分で起動可能
- **リアルタイム通信**: tmuxベースのエージェント間メッセージング
- **拡張可能**: カスタムシナリオを簡単に作成

## 🚀 クイックスタート

```bash
# リポジトリをクローン
git clone https://github.com/madai0517/Claude-Code-Agent.git
cd Claude-Code-Agent

# 依存関係インストール & グローバルコマンド登録
npm install
npm link

# 使用開始
claude-agents init --scenario business-strategy
claude-agents start
```

## 📋 必要環境

- Node.js ≥ 14.0.0
- tmux
- [Claude Code](https://claude.ai/code)

### インストール方法

```bash
# macOS
brew install node tmux

# Ubuntu/Debian
sudo apt update && sudo apt install nodejs npm tmux
```

## 🎭 利用可能なシナリオ

| シナリオ | 説明 | エージェント数 |
|---------|------|--------------|
| `business-strategy` | CEO、CTO、CFO、CMOによる戦略会議 | 6 |
| `collaborative-coding` | 開発チームの協働コーディング | 6 |
| `market-analysis` | 市場調査と競合分析 | 6 |
| `product-development` | プロダクト開発チーム | 5 |
| `hello-world` | 基本的なデモ | 5 |

## 💻 基本的な使い方

### 主要コマンド

```bash
# プロジェクト初期化
claude-agents init

# エージェント起動
claude-agents start <scenario-name>

# メッセージ送信
claude-agents send <agent-name> "メッセージ"

# 状態確認
claude-agents status

# シナリオ一覧
claude-agents list
```

### エージェント間通信の例

```bash
# CEOから戦略会議を開始
claude-agents send ceo "AI投資戦略について議論を開始します"

# 各専門家への指示
claude-agents send cto "技術的実現可能性を評価してください"
claude-agents send cfo "財務インパクトを分析してください"
```

## 🛠️ カスタムシナリオ作成

対話式ウィザードで簡単に作成できます：

```bash
claude-agents create-scenario
```

## 📖 詳細ドキュメント

詳しい情報は以下を参照してください：

- 🚀 [詳細なクイックスタート](.claude/quickstart.md)
- 📚 [開発者ガイド](.claude/development.md)
- 🏗️ [システムアーキテクチャ](.claude/architecture.md)
- 📋 [コマンドリファレンス](.claude/commands.md)
- 🎯 [シナリオ管理](.claude/scenarios.md)
- 🔧 [トラブルシューティング](.claude/troubleshooting.md)


