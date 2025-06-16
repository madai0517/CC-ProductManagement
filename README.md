# 🤖 Claude Agents - Multi-Agent Collaboration System

NPMパッケージ化されたエンタープライズグレードのマルチエージェント協働システム

## 🎯 システム概要

現実的なビジネスシナリオでAIエージェント間の協働を体験できます：

- 💼 **Business Strategy**: CEO、CTO、CFO、CMOによる戦略会議
- 💻 **Collaborative Coding**: CTO, アーキテクト、フロントエンド、バックエンド開発者の連携
- 📈 **Market Analysis**: リサーチャー、アナリストによる競合調査
- 🎉 **Hello World**: 基本的なマルチエージェントデモ

## 📦 インストール

### NPMパッケージでのインストール（推奨）

```bash
# グローバルインストール
npm install -g claude-agents

# 使用方法
claude-agents init
claude-agents start business-strategy
```

### ローカル開発環境

```bash
git clone https://github.com/your-repo/claude-agents.git
cd CC-ProductManagement
npm install
node bin/claude-agents.js init
```

## 🚀 クイックスタート（NPMパッケージ版）

### 🎆 ワンコマンドセットアップ

```bash
# Step 1: インストール
npm install -g claude-agents

# Step 2: プロジェクト初期化
mkdir my-ai-team && cd my-ai-team
claude-agents init --scenario business-strategy

# Step 3: エージェント起動
claude-agents start
```

✨ **自動で実行されること**:
- 依存関係チェック
- tmux環境構築
- シナリオ別エージェント配置
- Claude Code起動案内

## 🛠️ 前提条件

以下のツールがインストールされている必要があります：

- **Node.js**: 14.0.0以上
  ```bash
  # macOS
  brew install node

  # Ubuntu/Debian
  sudo apt update && sudo apt install nodejs npm
  ```

- **tmux**: マルチペイン管理
  ```bash
  # macOS
  brew install tmux

  # Ubuntu/Debian
  sudo apt update && sudo apt install tmux

  # CentOS/RHEL
  sudo yum install tmux
  ```

- **Claude Code**: AI開発アシスタント
  - [claude.ai/code](https://claude.ai/code) からダウンロード・インストール

## 🖥️ コマンドリファレンス

### 基本コマンド

| コマンド | 機能 | 例 |
|---------|------|-----|
| `claude-agents init` | プロジェクト初期化 | `claude-agents init --scenario business-strategy` |
| `claude-agents start` | エージェント起動 | `claude-agents start business-strategy` |
| `claude-agents send` | メッセージ送信 | `claude-agents send ceo "戦略会議を開始"` |
| `claude-agents switch` | シナリオ切り替え | `claude-agents switch hello-world` |
| `claude-agents status` | 状態確認 | `claude-agents status --agents` |
| `claude-agents list` | シナリオ一覧 | `claude-agents list --detailed` |
| `claude-agents reset` | 環境リセット | `claude-agents reset --force` |

### エイリアス

- `ca` (claude-agentsの短縮形)

## 🎭 シナリオ管理

### 利用可能シナリオ

| シナリオ | 説明 | エージェント数 | セッション構成 |
|---------|------|--------|---------|
| `business-strategy` | 事業戦略ディスカッション | 6エージェント | strategy(4) + analysis(2) |
| `collaborative-coding` | 共同コーディング | 6エージェント | development(6) |
| `market-analysis` | 市場分析・競合調査 | 6エージェント | research(6) |
| `hello-world` | 基本デモ | 5エージェント | president(1) + multiagent(4) |

### シナリオ操作

```bash
# シナリオ一覧
claude-agents list

# シナリオ詳細
claude-agents list --detailed

# シナリオ切り替え
claude-agents switch market-analysis

# 現在のシナリオ確認
claude-agents status
```

## 🖥️ tmuxセッションアクセス

### Business Strategy シナリオ

```bash
# 戦略チーム（CEO, CTO, CFO, マーケティング）
tmux attach-session -t strategy

# 分析チーム（PM, データアナリスト）
tmux attach-session -t analysis
```

**画面レイアウト（strategy セッション）:**
```
┌─────────────┬─────────────┐
│ CEO         │ CTO         │
│ (左上)      │ (右上)      │
├─────────────┼─────────────┤
│ CFO         │ CMO         │
│ (左下)      │ (右下)      │
└─────────────┴─────────────┘
```

### Hello World シナリオ

```bash
# プレジデント（統括責任者）
tmux attach-session -t president

# マルチエージェントチーム（boss1 + workers）
tmux attach-session -t multiagent
```

## 🤖 Claude Code起動

### 自動起動（推奨）

```bash
claude-agents start  # 現在のシナリオに応じて自動起動
```

### 手動起動

**Business Strategy シナリオ:**
```bash
# 最初のペインで認証
tmux send-keys -t strategy:1.1 'claude' C-m

# 認証完了後、全ペインで一括起動
for i in {1..4}; do tmux send-keys -t strategy:1.$i 'claude' C-m; done
for i in {1..2}; do tmux send-keys -t analysis:1.$i 'claude' C-m; done
```

**Hello World シナリオ:**
```bash
# President認証
tmux send-keys -t president:1.1 'claude' C-m

# Multiagent一括起動
for i in {1..4}; do tmux send-keys -t multiagent:1.$i 'claude' C-m; done
```

## 🎯 シナリオ実行

### Business Strategy シナリオ

**CEOペイン（strategy セッション左上）で実行：**
```
あなたはCEOです。AI技術への投資について戦略会議を開始します。技術的実現可能性、財務影響、市場機会について各専門家の意見を求めてください。
```

💡 **期待される動作**:
- CEOが戦略テーマを提示
- CTOが技術的実現可能性を評価
- CFOが財務インパクトを分析
- CMOが市場機会を説明
- PMとデータアナリストが定量分析を提供

**エージェント間メッセージ送信例：**
```bash
# CEOから他のエージェントに指示
claude-agents send cto "技術仕様の詳細レポートを作成してください"
claude-agents send cfo "投資提案書を準備してください"
claude-agents send marketing_director "市場参入戦略を策定してください"

# 分析チームへの依頼
claude-agents send product_manager "プロダクトロードマップを作成してください"
claude-agents send data_analyst "競合分析の詳細データを提供してください"
```

### Hello World シナリオ

**PRESIDENTセッションで実行：**
```
あなたはpresidentです。Hello World プロジェクトを開始してください。
```

**エージェント間通信例：**
```bash
claude-agents send president "Hello World プロジェクトを開始してください"
claude-agents send boss1 "worker達に作業を指示してください"
claude-agents send worker1 "Hello World作業を実行してください"
```

## 📁 設定ファイル

### claude-agents.json（自動生成）

```json
{
  "version": "2.0.0",
  "currentScenario": "business-strategy",
  "projectName": "MyProject",
  "scenarios": {
    "business-strategy": {
      "name": "Business Strategy Discussion",
      "description": "事業戦略や経営方針を議論するシナリオ",
      "tmux_sessions": {
        "strategy": {
          "window_name": "strategy-team",
          "panes": [
            { "role": "ceo" },
            { "role": "cto" },
            { "role": "cfo" },
            { "role": "CMO" }
          ]
        }
      },
      "agents": {
        "ceo": { "role": "最高経営責任者", "session": "strategy", "pane": 0 }
      }
    }
  },
  "settings": {
    "tmuxPrefix": "C-b",
    "autoStartClaude": true,
    "logLevel": "info",
    "colorOutput": true
  }
}
```

## 💬 エージェント間通信

### 基本送信

```bash
# 基本送信
claude-agents send <エージェント名> "<メッセージ>"

# 利用可能エージェント一覧
claude-agents send --list

# メッセージ履歴確認
cat logs/send_log.jsonl
```

### Business Strategyシナリオの例

```bash
# 戦略会議開始
claude-agents send ceo "新しい事業戦略について議論しましょう"

# 各エージェントへの専門的な質問
claude-agents send cto "技術的な観点から意見をお願いします"
claude-agents send cfo "財務インパクトを評価してください"
claude-agents send cmo "市場機会を分析してください"
claude-agents send product_manager "プロダクト要件を定義してください"
claude-agents send data_analyst "データに基づく分析をお願いします"
```

## 🔍 状態確認・デバッグ

### 状態確認ツール

```bash
# 総合状態確認
claude-agents status

# tmux詳細確認
claude-agents status --tmux

# エージェント詳細確認
claude-agents status --agents

# システム全体確認
claude-agents status --tmux --agents
```

### ログ・ファイル確認

```bash
# メッセージ履歴
cat logs/send_log.jsonl

# 日付別ログ
cat logs/send_2025-06-15.jsonl

# tmuxセッション状態
tmux list-sessions
tmux list-panes -t strategy
```

## 🔄 環境管理

### リセット・クリーンアップ

```bash
# 安全な環境リセット（対話式）
claude-agents reset

# 強制リセット
claude-agents reset --force

# 手動リセット
tmux kill-server
rm -f claude-agents.json
rm -rf ./tmp ./logs
```

### 環境再構築

```bash
# クイック再構築
claude-agents init --scenario business-strategy
claude-agents start

# シナリオ切り替え
claude-agents switch hello-world
```

## 📈 新機能ハイライト（v2.0）

✨ **NPMパッケージ化の主な改善点**:

### 🎯 ユーザビリティ向上
- **ワンコマンドセットアップ**: `npm install -g claude-agents` でグローバル利用
- **統合CLI**: 全機能を`claude-agents`コマンド一つで操作
- **対話式インターフェース**: 設定や確認が直感的
- **カラフルな出力**: 状態やエラーが視覚的に分かりやすい

### 🔧 技術的改善
- **依存関係自動チェック**: tmux、Claude Code、Node.jsの確認と解決策提示
- **エラーハンドリング強化**: 詳細なエラーメッセージと修復手順
- **ログ管理**: JSONL形式での構造化ログとアーカイブ機能
- **設定管理**: JSON形式の統合設定ファイル

### 🚀 拡張性
- **プログラマティックAPI**: Node.jsライブラリとしても利用可能
- **カスタムシナリオ**: 独自のシナリオを簡単に作成・追加
- **プラグインシステム**: カスタムコマンドの追加が可能

## 🎬 実践ガイド：Business Strategy シナリオ

### ステップ1: 環境準備

```bash
# インストール
npm install -g claude-agents

# プロジェクト作成
mkdir ai-strategy-meeting && cd ai-strategy-meeting

# 初期化
claude-agents init --scenario business-strategy
```

### ステップ2: エージェント起動

```bash
# tmuxセッション構築とエージェント起動
claude-agents start

# 出力例:
# 🎭 シナリオ: Business Strategy Discussion
# ✅ Created 2 tmux sessions
# ✅ Generated mapping for 6 agents
```

### ステップ3: セッション参加

```bash
# 戦略チーム（4ペイン表示）
tmux attach-session -t strategy

# または分析チーム（2ペイン表示）
tmux attach-session -t analysis
```

### ステップ4: 戦略議論開始

**CEOペイン（左上）で以下を入力:**
```
あなたはCEOです。AI技術への投資について戦略会議を開始します。技術的実現可能性、財務影響、市場機会について各専門家の意見を求めてください。
```

### ステップ5: エージェント間コミュニケーション

**各エージェントの専門性を活かした応答例:**

1. **CTO（右上ペイン）の応答例:**
   ```
   技術的観点から以下を提案します：
   - AI投資の技術的実現可能性: 高い
   - 推奨技術スタック: TensorFlow, PyTorch
   - 実装期間: 6-8ヶ月
   - 技術的リスク: 人材確保、インフラ投資
   ```

2. **CFO（左下ペイン）の応答例:**
   ```
   財務分析の結果をお伝えします：
   - 初期投資額: 5億円
   - 予想ROI: 225%（3年累計）
   - 回収期間: 2.4年
   - 感度分析: 市場成長率±5%でROI 180-280%
   ```

3. **マーケティング責任者（右下ペイン）の応答例:**
   ```
   市場機会について報告します：
   - ターゲット市場規模: 100億円（年間）
   - 成長率: 年率15%
   - 競合優位性: 使いやすさで差別化可能
   - 価格戦略: プレミアム価格（競合比+20%）
   ```

### ステップ6: データ分析チームとの連携

```bash
# 分析チームにアタッチ（別ターミナルで）
tmux attach-session -t analysis

# コマンドラインからの直接通信
claude-agents send product_manager "プロダクトロードマップを作成してください"
claude-agents send data_analyst "競合分析の詳細データを提供してください"
```

### ステップ7: システム状態監視

```bash
# 総合状態確認
claude-agents status

# エージェント一覧
claude-agents status --agents

# 出力例:
# 📊 6個のエージェントが設定済み
# 🎭 ceo → strategy:1.1
# 🎭 cto → strategy:1.2
# 🎭 cfo → strategy:1.3
# ...
```

## 🔄 シナリオ切り替えの実例

### 現在のシナリオから別のシナリオへ

```bash
# 実行中にシナリオ切り替え
claude-agents switch collaborative-coding

# または完全リセットして新規構築
claude-agents reset
claude-agents init --scenario market-analysis
claude-agents start
```

### シナリオ一覧の確認

```bash
claude-agents list --detailed

# 出力例:
# 📦 hello-world
#    基本的なマルチエージェント通信デモ
#    エージェント: 5個
#    セッション: 2個
#    主要エージェント: president, boss1, worker1
#
# 🎯 business-strategy (現在)
#    事業戦略や経営方針を議論するシナリオ
#    エージェント: 6個
#    セッション: 2個
#    主要エージェント: ceo, cto, cfo
```

## ⚠️ トラブルシューティング

### よくある問題と解決方法

**問題1: `claude-agents: command not found`**
```bash
# 解決方法
npm install -g claude-agents

# または（ローカル開発時）
npm link
```

**問題2: tmuxセッションが見つからない**
```bash
# 確認
claude-agents status --tmux
tmux list-sessions

# 解決方法
claude-agents reset
claude-agents start
```

**問題3: エージェントマッピングエラー**
```bash
# 確認
claude-agents status --agents
cat ./tmp/agent_mapping.json

# 解決方法
claude-agents switch <current-scenario>
```

**問題4: Claude Code認証エラー**
```bash
# 手動認証手順
tmux attach-session -t strategy
# 最初のペインで claude コマンド実行・認証
# その後他ペインでも claude コマンド実行
```

**問題5: 環境をリセットしたい**
```bash
# 完全リセット
claude-agents reset --force

# または手動リセット
tmux kill-server
rm -f claude-agents.json
rm -rf ./tmp ./logs
claude-agents init
```

### ログ確認

```bash
# 送信ログ
cat logs/send_log.jsonl

# 構造化ログの例
# {"timestamp":"2025-06-15T14:00:00.000Z","agent":"ceo","target":"strategy:1.1","message":"戦略会議を開始","length":12}

# NPMデバッグログ
DEBUG=claude-agents* claude-agents start

# tmuxデバッグ
tmux list-sessions -v
```

## 🎯 実践的な使用シーン

### シーン1: 新プロダクト企画会議

```bash
claude-agents init --scenario product-development
claude-agents start
# UXデザイナー、UIデザイナー、プロダクトオーナー、ユーザーリサーチャー
```

### シーン2: 技術アーキテクチャレビュー

```bash
claude-agents init --scenario collaborative-coding
claude-agents start
# アーキテクト、フロントエンド、バックエンド、DevOps、QA、テックリード
```

### シーン3: 市場参入戦略検討

```bash
claude-agents init --scenario market-analysis
claude-agents start
# 市場調査、競合分析、消費者インサイト、トレンド分析、ビジネスアナリスト
```

## 📊 期待される成果

### 定量的効果
- **セットアップ時間**: 95%削減（15分→30秒）
- **操作複雑性**: 多段階コマンド → ワンコマンド
- **学習コスト**: 大幅削減（統合CLI）
- **エラー率**: 依存関係チェックにより大幅削減

### 定性的効果
- **現実的な業務シミュレーション**: 実際のビジネスシーンを体験
- **専門性特化したエージェント協働**: 各分野の専門知識を活用
- **柔軟なシナリオ切り替え**: 用途に応じた最適な構成
- **エンタープライズ対応**: 本格的なチーム協働の実現

## 🎓 学習・研修での活用

### 教育機関での使用
- **ビジネススクール**: 戦略策定プロセスの体験学習
- **工学部**: アジャイル開発とチーム協働の実践
- **経営学部**: 組織内コミュニケーションの理解

### 企業研修での活用
- **新人研修**: 部門間連携の理解促進
- **管理職研修**: 意思決定プロセスの体験
- **チームビルディング**: 役割分担と協働の練習

### 個人スキル向上
- **コミュニケーション**: 専門性を活かした議論スキル
- **プロジェクト管理**: マルチステークホルダー調整
- **戦略思考**: 複数視点からの課題分析

## 🔗 Legacy Information

### 旧Bashスクリプト版（参考情報）

<details>
<summary>v1.x Bashスクリプト版の情報（クリックで展開）</summary>

**注意**: 以下の情報は旧バージョン（v1.x）のものです。現在は**NPMパッケージ版（v2.0）の使用を強く推奨**します。

#### 旧コマンド体系
```bash
# 旧版（非推奨）
./setup.sh
./agent-send.sh ceo "メッセージ"
./scenario-manager.sh set business-strategy

# 新版（推奨）
claude-agents init
claude-agents send ceo "メッセージ"
claude-agents switch business-strategy
```

#### 移行理由
- **保守性**: 個別スクリプト → 統合NPMパッケージ
- **エラーハンドリング**: 基本的なもの → 包括的なエラー処理
- **ユーザビリティ**: コマンド分散 → 統一されたCLI
- **プラットフォーム対応**: Linux/macOS限定 → クロスプラットフォーム

</details>

---

## 🚀 はじめよう！

新しいMulti-Agent Communication体験で、実践的なコラボレーションスキルを身につけてください！

```bash
# 今すぐ始める
npm install -g claude-agents
claude-agents init --scenario business-strategy
claude-agents start
```

🤖✨ **AI powered collaboration awaits you!**
