# Claude Code Knowledge Base

このファイルは、Claude Codeが本プロジェクトで学習・蓄積した知見を記録します。

## 学習済み内容

### 2025-06-17: プロジェクト初期分析
- **システム理解**: tmuxベースのマルチエージェント通信システムの動作原理を把握
- **アーキテクチャ**: NPMパッケージ化されたCLI + tmux統合の構成を理解
- **通信メカニズム**: `tmux send-keys`を使用したエージェント間メッセージングの実装詳細

### 2025-06-17: 対話式シナリオ作成システム実装
- **UX設計**: 複雑なYAMLファイル編集を5分の対話式プロセスに簡素化
- **テンプレートシステム**: 業界別（ビジネス、開発、ヘルスケアなど）のベストプラクティステンプレート
- **自動化**: scenario.yaml, agents.yaml, layout.yaml の完全自動生成
- **エラーハンドリング**: 入力検証、ファイル生成エラー、設定競合の包括的処理

### コードパターンの理解
- **エラーハンドリング**: Promise-based非同期処理での適切なエラー処理パターン
- **設定管理**: JSON/YAML形式の統合設定システム
- **ログ管理**: JSONL形式での構造化ログと日次ローテーション
- **対話式CLI**: inquirer.jsを使用したユーザーフレンドリーな入力収集
- **ファイル生成**: テンプレートベースの動的YAML/Markdownファイル生成

## ベストプラクティス

### 開発ワークフロー
- **テスト駆動開発**: Jest使用、カバレッジ80%閾値
- **モック活用**: tmuxコマンドの適切なモック化
- **非同期処理**: Promise chainとasync/awaitの使い分け

### コード品質
- **エスケープ処理**: tmux送信時の特殊文字処理の重要性
- **依存関係管理**: 外部ツール（tmux, Node.js）の可用性チェック
- **設定検証**: 設定ファイルの存在確認と妥当性検証

### プロジェクト固有の知見
- **エージェントマッピング**: 動的マッピング生成の効率性
- **セッション管理**: tmuxセッションのライフサイクル管理
- **ログ分析**: 構造化ログによる通信パターンの分析
- **シナリオ設計**: 現実的なビジネスシナリオからの抽象化手法
- **テンプレート活用**: 業界固有のエージェント役割とコミュニケーションパターン

## よく発生する問題と解決方法

### tmux関連
- **セッション競合**: 同名セッションの適切な削除・再作成
- **ペイン管理**: ペイン数とエージェント数の不整合対策
- **権限問題**: tmuxサーバーへのアクセス権限設定

### 設定関連
- **設定ファイル競合**: JSON/YAML設定の優先順位
- **エージェント解決**: エイリアス機能による名前解決の柔軟性
- **シナリオ切り替え**: 実行時のシナリオ変更処理

## パフォーマンス最適化の知見

### 通信最適化
- **送信間隔**: エージェント間の適切な通信間隔設定
- **並列処理**: 複数tmuxコマンドの効率的な並列実行
- **キャッシュ戦略**: エージェントマッピングのメモリキャッシュ

### リソース管理
- **メモリ使用量**: 大量ログファイルのメモリ効率
- **ディスク容量**: ログローテーションによる容量管理
- **CPU負荷**: tmux操作の負荷分散

## 避けるべきアンチパターン

### 設計アンチパターン
- ❌ **同期的tmux操作**: blocking処理による全体パフォーマンス低下
- ❌ **ハードコード設定**: 設定の外部化を怠ることによる保守性低下
- ❌ **エラー握りつぶし**: tmux操作エラーの適切でない処理

### 実装アンチパターン
- ❌ **グローバル状態依存**: 過度なグローバル変数への依存
- ❌ **テスト不備**: 非同期処理の不適切なテスト実装
- ❌ **ログ肥大化**: 無制限なログ出力による容量問題

## 今後の学習ポイント

### 技術的深掘り
- [ ] tmux APIの更なる活用方法
- [ ] 複雑なシナリオでのパフォーマンス特性
- [ ] エラー回復戦略の詳細分析

### システム拡張
- [ ] プラグインシステムの実装パターン
- [ ] 大規模エージェント構成での運用ノウハウ
- [ ] 他の通信方式との比較・評価

---

*このファイルは各Claude Codeセッションで更新され、プロジェクト理解の蓄積に活用されます。*