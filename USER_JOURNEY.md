# エージェントシステムを使った企画から開発までのユーザージャーニー

## 概要
TaskManager、Developer、DataGathererの3つのエージェントを活用して、アイデアから製品リリースまでを効率的に進めるユーザージャーニーです。

---

## 🎯 Phase 1: プロジェクト立ち上げフェーズ（Day 1-3）

### 1.1 プロジェクト初期化
**使用エージェント**: TaskManager

```bash
# TaskManagerを起動（最初に使用）
claude code --agent taskmanager

# プロジェクトとLinearの初期化
"新規プロジェクトを開始"
→ タイプ: business
→ プロジェクト名: "NextGen EC - 事業企画"

# Linear設定ファイルの初期化
"プロジェクト設定を初期化"
```

**自動生成される内容**:
- Linearプロジェクトの作成
- デフォルトマイルストーン（市場調査完了、ビジネスモデル確定、事業計画書承認）
- 基本的なラベル体系
- linear_config.yamlの生成

### 1.2 初期タスクの作成
**使用エージェント**: TaskManager

```bash
# 初期調査タスクの作成
"市場調査タスクを作成"
→ "ECサイトの最新トレンド調査"
→ "競合他社の分析"
→ "ターゲット顧客の調査"

# チーム体制の整理
"チーム情報を登録"
→ メンバー: "山田太郎（PM）、鈴木花子（フロントエンド）、田中次郎（バックエンド）"
```

---

## 🔍 Phase 2: 調査・情報収集フェーズ（Day 4-7）

### 2.1 市場調査タスクの実行
**使用エージェント**: DataGatherer（TaskManagerから引き継ぎ）

```bash
# DataGathererを起動
claude code --agent datagatherer

# Linear上のタスクを確認
"Linear issue BUS-001を確認"
→ タスク: "ECサイトの最新トレンド調査"

# 調査実行
"ECサイトの最新トレンドを調査して"
"Shopifyの競合分析をして"
"2025年のEコマース市場動向を調べて"
```

**成果物**:
- knowledge_base/EXTERNAL_INSIGHTS.md に市場調査結果
- Linear上のタスクにコメントで進捗報告
- 重要な発見をSlackに通知

### 2.2 調査結果のタスク化
**使用エージェント**: TaskManager（DataGathererから引き継ぎ）

```bash
# TaskManagerに戻る
claude code --agent taskmanager

# 調査結果を基に新たなタスクを作成
"調査結果を基にタスクを作成"
→ DataGathererの調査結果を参照
→ 優先順位の高い機能をタスク化
→ マイルストーンに紐付け
```

---

## 📋 Phase 3: 要件定義フェーズ（Day 8-14）

### 3.1 要件の詳細化
**使用エージェント**: TaskManager

```bash
# 要件定義タスクの作成
"ユーザーストーリーを作成"
→ "商品検索機能の実装"
→ "決済システムの統合"
→ "在庫管理システムの構築"

# システム企画フェーズへの移行
"新規プロジェクトを開始"
→ タイプ: system_planning
→ プロジェクト名: "NextGen EC - システム企画"
```

### 3.2 技術調査の依頼
**使用エージェント**: TaskManager → DataGatherer

```bash
# TaskManager
"技術調査タスクを作成"
→ Linear issue: "SYS-001: 決済システムの技術選定"

# DataGatherer
"Linear issue SYS-001を実行"
→ "決済システムのベストプラクティスを調査して"
→ "StripeとPayPalの比較分析をして"
→ 調査結果をLinearにコメント
```

### 3.3 会議・意思決定の記録
**使用エージェント**: DataGatherer

```bash
# 要件定義会議の記録
"要件定義会議の議事録を作成"

# 会議音声の文字起こし
"inboxフォルダの会議音声を処理して"
→ 自動的に決定事項とアクションアイテムを抽出
→ Linear上に決定事項を記録
```

---

## 🚀 Phase 4: 開発フェーズ（Day 15-60）

### 4.1 開発タスクの割り当て
**使用エージェント**: TaskManager → Developer

```bash
# TaskManager
"開発フェーズを開始"
→ プロジェクトタイプ: development
→ マイルストーン: MVP完成、テスト完了、本番リリース

"開発タスクを割り当て"
→ Linear issueを開発者に割り当て
→ 優先順位とスプリントを設定
```

### 4.2 開発タスクの実装
**使用エージェント**: Developer（TaskManagerから引き継ぎ）

```bash
# Developer
"Linear issue DEV-123を実装"
→ 自動的にブランチ作成: feature/DEV-123-product-search
→ 実装開始
→ テスト作成
→ Linear上で進捗更新
```

### 4.3 日々の開発サイクル
**典型的な1日の流れ**:

**朝（9:00）**:
```bash
# TaskManager
"本日のスプリントタスクを確認"
→ 優先順位順にタスク一覧表示
→ ブロッカーの確認

# Developer
"割り当てられたタスクを確認"
→ Linear上の自分のタスクを表示
```

**日中（10:00-17:00）**:
```bash
# Developer
"DEV-124の実装を開始"
→ コード実装
→ 単体テスト作成
→ Linearステータス更新

# 技術的な課題発生時
Developer: "技術調査が必要"
→ TaskManagerでタスク作成
→ DataGathererに調査依頼
→ 結果を基にDeveloperが実装継続
```

**夕方（18:00）**:
```bash
# Developer
"PRを作成"
→ 自動的にLinearと連携
→ レビュー依頼

# TaskManager
"本日の進捗を更新"
→ 完了タスクをDoneに
→ 明日のタスクを準備
```

### 4.4 スプリント管理
**使用エージェント**: TaskManager

```bash
# 2週間スプリント
"新しいスプリントを開始"
"スプリントバックログを作成"
"バーンダウンチャートを確認"

# デイリースクラム
"スクラムミーティングの準備"
→ 各開発者の進捗を集計
→ ブロッカーをリスト化
```

---

## 🔄 Phase 5: テスト・品質保証フェーズ（Day 61-75）

### 5.1 テストタスクの管理
**使用エージェント**: TaskManager

```bash
# QAフェーズの開始
"テストフェーズを開始"
→ QAチェックリストを作成
→ テストケースをタスク化
→ バグトラッキングの準備
```

### 5.2 テスト実施
**使用エージェント**: Developer + TaskManager

```bash
# Developer
"統合テストを実行"
"E2Eテストを作成"

# TaskManager
"バグチケットを管理"
→ 重要度でラベル付け
→ 修正担当者をアサイン
```

### 5.3 フィードバック収集
**使用エージェント**: DataGatherer

```bash
"Slackのフィードバックを収集"
"テストレポートをまとめて"
→ Linear上にフィードバックを集約
```

---

## 🎉 Phase 6: リリース・運用フェーズ（Day 76+）

### 6.1 リリース準備
**使用エージェント**: TaskManager + Developer

```bash
# TaskManager
"リリースチェックリストを作成"
"デプロイ手順を文書化"
→ Linear上でリリース関連タスクを管理

# Developer
"本番環境へのデプロイ準備"
"リリースブランチを作成"
```

### 6.2 継続的な改善
**使用エージェント**: TaskManager中心の全エージェント連携

```bash
# 毎週月曜日
TaskManager: "今週のスプリント計画を立てて"
→ 先週の振り返り
→ 今週の優先タスク設定

DataGatherer: "週次レポートを作成"
→ TaskManagerが作成したタスクの進捗を集計

# 毎日
TaskManager: "デイリータスクの確認"
→ 各エージェントへのタスク割り当て
→ ブロッカーの管理

# 月次
TaskManager: "プロジェクトの振り返りを実施"
→ マイルストーン達成状況
→ 次月の計画策定
```

---

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

### パターン2: タスク駆動開発フロー
```
TaskManager（Linearタスク作成）
    ↓
Developer または DataGatherer（タスク実行）
    ↓
TaskManager（進捗管理・次タスク作成）
```

### パターン3: 問題解決フロー
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

### パターン4: 定期レビュー
```
TaskManager（レビュータスク作成）
    ↓
DataGatherer（情報収集）
    ↓
TaskManager（分析・計画更新）
    ↓
全エージェント（タスク実行）
```

---

## 💡 成功のポイント

### 1. TaskManagerを中心とした運用
- **プロジェクトの開始は必ずTaskManagerから**
- すべてのタスクはLinear上で管理
- 他のエージェントへの作業依頼もTaskManager経由

### 2. 各エージェントの強みを活かす
- **TaskManager**: プロジェクト全体の管理と計画
- **DataGatherer**: Linear上のタスクに基づく情報収集
- **Developer**: Linear上のタスクに基づく実装

### 3. Linear中心の情報管理
- すべての作業はLinear issueとして記録
- 進捗・ブロッカー・決定事項はLinearに集約
- エージェント間の引き継ぎもLinear経由

### 4. 自動化を最大限活用
- Linearステータスは自動更新
- タスク完了時の次タスク作成
- 定期的なレビューとレポート生成

### 5. 明確な役割分担
- TaskManager: "何をするか"を管理
- DataGatherer: "どうするか"を調査
- Developer: "実際に作る"を実行

---

## 🎯 期待される成果

1. **開発速度の向上**: 30-50%の効率化
2. **情報の透明性**: 全メンバーが最新情報にアクセス可能
3. **品質の向上**: 自動テストとレビューによる品質保証
4. **ナレッジの蓄積**: すべての決定と学びが記録される

---

最終更新: 2025-01-25