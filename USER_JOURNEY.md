# エージェントシステムを使った企画から開発までのユーザージャーニー

## 概要
TaskManager、Developer、DataGathererの3つのエージェント定義（CLAUDE.md）を活用して、アイデアから製品リリースまでを効率的に進めるユーザージャーニーです。

## 💻 システム構成

### 専用PC体制（3台構成）
1. **TaskManager専用PC**: プロジェクト管理・タスク管理専用（24/7稼働）
2. **DataGatherer専用PC**: 情報収集・調査専用（24/7稼働）
3. **Developer専用PC**: 開発タスク専用（24/7稼働）

### 各PCの役割
- **TaskManager PC**: Linearを常時監視、タスクの作成・割り当て・進捗管理
- **DataGatherer PC**: 30分ごとに自動でタスクを確認、調査・情報収集を実行
- **Developer PC**: 30分ごとに自動で開発タスクを確認、TDD実装を自律的に実行

## 📚 重要な前提知識

### 専用PC体制での運用方法
各PCにそれぞれのエージェントを常駐させることで、リアルタイムでの並行作業が可能になります。

### 各PCでのセットアップ
```bash
# TaskManager専用PCでの設定
mkdir -p ~/taskmanager
cd ~/taskmanager
cp CLAUDE.taskmanager.md ./CLAUDE.md

# DataGatherer専用PCでの設定
mkdir -p ~/datagatherer
cd ~/datagatherer
cp CLAUDE.datagatherer.md ./CLAUDE.md

# Developer PCでの設定
mkdir -p ~/developer
cd ~/developer
cp CLAUDE.developer.md ./CLAUDE.md
```

### エージェント間の連携
- **すべての連携はLinear経由**: 各PCはLinearを通じて情報を共有
- **リアルタイム更新**: executorラベルによる自動タスク検出
- **非同期コラボレーション**: 各エージェントが独立して動作

## 🚀 Phase 1: プロジェクト立ち上げフェーズ（Day 1-3）

### 1.1 プロジェクト初期化
**使用PC**: TaskManager専用PC

```bash
# TaskManager専用PCで実行
"新規プロジェクトを開始"
→ タイプ: business
→ プロジェクト名: "NextGen EC - 事業企画"

# DataGatherer用の初期タスクを作成
"市場調査タスクを作成"
→ 担当: DataGatherer (executor:datagatherer)
→ 優先度: High (1)
```

**同時にDataGatherer専用PCで**:
```bash
# DataGathererが自動でタスクを検出
"自分のタスクを確認"
→ executor:datagathererのタスクが表示される
→ 自動的に調査を開始
```

## 🔍 Phase 2: 調査・情報収集フェーズ（Day 4-7）

### 2.1 同時並行での調査実行
**使用PC**: DataGatherer専用PC（自動実行）

```bash
# DataGatherer専用PCでは30分ごとに自動確認
# タスクが検出されると自動的に実行

"Linear issue BUS-001を確認"
→ タスク: "ECサイトの最新トレンド調査"

# 調査実行
"ECサイトの最新トレンドを調査して"
"Shopifyの競合分析をして"
"2025年のEコマース市場動向を調べて"

# 結果をLinearに自動コメント
→ 調査結果がLinearにリアルタイムで反映
```

## 🚀 Phase 3: 開発フェーズ（Day 15-60）

### 3.1 開発タスクの自動実装
**使用PC**: Developer専用PC（自動実行）

```bash
# Developer専用PCでは30分ごとに自動確認・実行
"自分のタスクを確認して実行"
→ executor:developerラベルのタスクを自動検索
→ 優先度順（0:Urgent → 4:None）でソート
→ 最優先タスクを自動選択

# 自動実装の流れ
→ "DEV-123: 商品検索機能の実装"を自動検出
→ 設計フェーズ（Perplexity技術調査、実現可能性評価）
→ ユーザー承認取得
→ GitHub Issue作成（Ultra Think）
→ ブランチ自動作成: feature/DEV-123-product-search
→ TDDサイクルで自動実装開始
  - Red: 失敗するテストを作成
  - Green: 最小限の実装
  - Refactor: コード改善
→ 各フェーズで詳細なGitHubコミット
→ Linear上で進捗を自動更新
→ PR作成まで自動実行
```

### 3.2 日々の開発サイクル
**典型的な1日の流れ**:

**朝（9:00） - 3台同時稼働**:

**TaskManager専用PC**:
```bash
"本日のスプリントタスクを確認"
→ 優先順位順にタスク一覧表示
→ ブロッカーの確認

"各エージェントの稼働状況を確認"
→ DataGatherer、Developerのタスク進捗をモニタリング
```

**DataGatherer専用PC**:
```bash
# 自動でタスクを検出・実行中
→ executor:datagathererのタスクを自動処理
→ 優先度順に調査・情報収集
```

**Developer専用PC**:
```bash
# 自動でタスクを検出・実行中
→ executor:developerのタスクを自動処理
→ 優先度順にTDD実装
→ GitHub Issueに詳細記録（Ultra Think）
```

## 📊 エージェント連携パターン

### パターン1: プロジェクト開始フロー（推奨）
```
TaskManager（プロジェクト初期化・タスク作成）
    ↓
DataGatherer（調査・情報収集）
    ↓
TaskManager（調査結果を基にタスク更新）
    ↓
Developer（実装）
```

### パターン2: 問題解決フロー
```
Developer（問題発見）
    ↓
TaskManager（調査タスク作成）
    ↓
DataGatherer（解決策調査）
    ↓
TaskManager（対応タスク作成）
    ↓
Developer（修正実装）
```

## 💡 専用PC体制での成功のポイント

### 1. 3台同時稼働の利点
- **完全な並行作業**: 各エージェントが独立して動作
- **リアルタイム連携**: Linearを介した即座の情報共有
- **待ち時間ゼロ**: 他エージェントの作業完了を待つ必要なし

### 2. 自律的運用の実現
- **TaskManager**: 24/7でプロジェクト監視、即応タスク作成
- **DataGatherer**: 30分ごとの自動確認、優先度ベース処理
- **Developer**: 設計→実装→PR作成まで完全自動化

### 3. Linearを中心とした情報ハブ
- **単一情報源**: すべての情報がLinearに集約
- **executorラベル**: 各PCが自分のタスクを自動識別
- **コメントベース連携**: 非同期で効率的な情報交換

## 🎯 期待される成果

1. **開発速度の向上**: 30-50%の効率化
2. **情報の透明性**: 全メンバーが最新情報にアクセス可能
3. **品質の向上**: 自動テストとレビューによる品質保証
4. **ナレッジの蓄積**: すべての決定と学びが記録される
5. **24/7稼働**: 人間の休息時間も開発が継続

最終更新: 2025-01-27