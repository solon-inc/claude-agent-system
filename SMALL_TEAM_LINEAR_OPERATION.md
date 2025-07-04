# 3人チーム向けLinear運用ガイド - Claude Code連携版

## チーム構成と役割

### メンバー構成
```yaml
team:
  - role: "ビジネスオーナー"
    responsibilities:
      - ビジョン・戦略策定
      - 優先順位決定
      - ステークホルダー調整
      - 予算管理
    claude_agents: ["TaskManager", "DataGatherer"]
    
  - role: "ビジネス企画"
    responsibilities:
      - 要件定義
      - 市場調査・分析
      - ユーザーストーリー作成
      - プロジェクト管理
    claude_agents: ["TaskManager", "DataGatherer"]
    
  - role: "エンジニア"
    responsibilities:
      - 技術設計・実装
      - インフラ構築
      - 品質管理
      - 技術調査
    claude_agents: ["Developer", "TaskManager", "DataGatherer"]
```

## Linear設定（3人チーム最適化）

### シンプルなラベル体系
```yaml
labels:
  # 担当者（アサインの代替として使用）
  owner: "@ビジネスオーナー"
  planner: "@ビジネス企画"
  engineer: "@エンジニア"
  
  # フェーズ（現在の段階）
  phase:discovery    # 調査・検討
  phase:planning     # 企画・設計
  phase:development  # 開発・実装
  phase:review       # レビュー・検証
  
  # 優先度（シンプルに3段階）
  p0  # 今すぐ（ブロッカー）
  p1  # 今週中
  p2  # 今後
  
  # タイプ（作業種別）
  type:decision     # 意思決定が必要
  type:research     # 調査・分析
  type:implement    # 実装作業
  type:document     # ドキュメント作成
```

### ワークフローステート（最小限）
```yaml
states:
  - name: "Inbox"
    description: "新規・未整理"
    
  - name: "Ready"
    description: "着手可能"
    
  - name: "In Progress"
    description: "作業中"
    
  - name: "Review"
    description: "レビュー待ち"
    
  - name: "Done"
    description: "完了"
```

## Claude Code活用パターン

### 1. ビジネスオーナーの典型的な1日

#### 朝のルーティン（TaskManager使用）
```bash
# Linear上の状況確認
"今日の重要タスクを確認"
"意思決定が必要なタスクを表示"
"ブロッカーになっているタスクは？"

# 優先順位の調整
"p0タスクの一覧を表示"
"[タスクID]の優先度をp1に変更"
```

#### 戦略検討（DataGatherer使用）
```bash
# 市場調査
"競合の最新動向を調査して"
"このテクノロジーのトレンドを分析"

# データ収集
"先週のSlack議論をまとめて"
"重要な決定事項を整理"
```

### 2. ビジネス企画の典型的な1日

#### 要件定義作業（TaskManager使用）
```bash
# ユーザーストーリー作成
"[Feature] ユーザー認証機能のタスクを作成"
"要件定義のテンプレートで新規タスクを作成"

# タスクの詳細化
"[タスクID]にユーザーストーリーを追加"
"受け入れ条件を定義"
```

#### プロジェクト管理（TaskManager使用）
```bash
# 進捗確認
"今週のスプリント状況を確認"
"各メンバーの作業負荷を表示"

# 調整作業
"来週の作業計画を作成"
"依存関係のあるタスクを確認"
```

### 3. エンジニアの典型的な1日

#### 開発作業（Developer使用）
```bash
# タスク実装
"Linear DEV-123を実装開始"
"ブランチを作成してセットアップ"

# コード作成
"認証APIを実装"
"単体テストを追加"

# 進捗更新
"実装完了、PRを作成"
```

#### 技術調査（DataGatherer使用）
```bash
# 技術選定
"ReactとVueの比較調査"
"認証ライブラリのベストプラクティスを調査"

# 問題解決
"このエラーの解決方法を調査"
"パフォーマンス改善の方法を検索"
```

## 効率的なタスク運用

### タスク作成のルール

#### 1. タイトルの命名規則
```
[誰が] [何を] [いつまでに]

例：
"[Owner] 予算承認 [今週金曜]"
"[Planner] ユーザーヒアリング実施 [3/15]"
"[Engineer] 認証API実装 [2日]"
```

#### 2. 必須情報
```markdown
## Why（なぜ必要か）
[背景と目的を1-2文で]

## What（何をするか）
- [ ] 具体的なアクション1
- [ ] 具体的なアクション2

## Who（誰が確認するか）
レビュアー: @メンバー名

## When（いつまでに）
期限: YYYY-MM-DD
```

### 日次スタンドアップ（10分）

#### Linear画面を共有しながら実施
```yaml
agenda:
  1. Doneに移動したタスク（昨日の完了）
  2. In Progressのタスク（今日やること）
  3. Blockerの確認（助けが必要なこと）
  4. 新規Inboxの優先度付け（全員で）
```

#### Claude Codeでの自動化
```bash
# スタンドアップ準備（TaskManager）
"昨日から今日の進捗サマリーを作成"
"各メンバーの本日のタスクを表示"
"ブロッカータスクをリストアップ"
```

### 週次レビュー（30分）

#### 金曜日の振り返り
```yaml
review_items:
  1. 完了タスクの確認
  2. 来週の優先順位決定
  3. プロセス改善の提案
  4. 役割分担の調整
```

## コミュニケーションフロー

### Linear中心の非同期コミュニケーション

#### 1. 質問・相談
```markdown
# Linearコメントでメンション
@engineer テクニカルな実現可能性を教えてください
@planner この要件の優先度はどう考えますか？
@owner この方向性で進めて良いでしょうか？
```

#### 2. 意思決定の記録
```markdown
# 決定事項は必ずLinearに記録
## 決定内容
[何を決めたか]

## 理由
[なぜその決定をしたか]

## 影響範囲
[この決定で変わること]

決定者: @owner
日付: YYYY-MM-DD
```

### Slack連携（補助的に使用）

#### 通知設定
```yaml
linear_to_slack:
  - p0タスクの作成
  - 自分へのメンション
  - ステータス変更（Review → Done）
  
slack_to_linear:
  - 重要な議論は手動でLinearに転記
  - アクションアイテムは即タスク化
```

## タスクテンプレート（3人チーム用）

### 意思決定タスク
```markdown
[Decision] [決定事項]

## 決定が必要な理由
[背景説明]

## 選択肢
1. オプションA：[説明]
2. オプションB：[説明]

## 推奨案
[企画/エンジニアからの提案]

## 決定期限
[いつまでに決める必要があるか]

ラベル: @owner, type:decision, p0
```

### 調査タスク
```markdown
[Research] [調査内容]

## 調査目的
[何のために調べるか]

## 調査項目
- [ ] 項目1
- [ ] 項目2

## 期待する成果
[調査結果をどう使うか]

## 担当
主: @planner/@engineer
サポート: @必要に応じて

ラベル: type:research, phase:discovery
```

### 実装タスク
```markdown
[Dev] [機能名]

## 要件
[企画からの要件]

## 技術仕様
[エンジニアが記載]

## テスト方針
- [ ] 単体テスト
- [ ] 動作確認手順

## レビュー
コード: @engineer
動作確認: @planner

ラベル: @engineer, type:implement, phase:development
```

## 効率化のコツ

### 1. 役割を超えた協力
- 全員がすべてのタスクを見られる
- 得意分野で助け合う
- 決定は早く、実装も早く

### 2. ドキュメント最小化
- Linearのdescriptionに集約
- 外部ドキュメントは最小限
- 議論の経緯もコメントで残す

### 3. 自動化の活用
```bash
# 毎朝の定型作業（TaskManager）
"今日の作業リストを作成"
"優先度の再評価"

# 週次レポート（DataGatherer）
"今週の進捗をまとめて"
"来週の課題を整理"

# コード品質（Developer）
"テストカバレッジを確認"
"リファクタリング候補を提案"
```

### 4. 迅速な意思決定
- 議論は最大30分
- 決定事項は即記録
- 修正は後からでもOK

## アンチパターン（避けるべきこと）

1. **過度な階層化**
   - エピックやサブタスクを深くしすぎない
   - フラットな構造を保つ

2. **承認プロセスの複雑化**
   - 3人なので直接対話
   - 形式的な承認は最小限

3. **ツールの使いすぎ**
   - Linear + Claude Code + Slackで完結
   - 他のツールは極力使わない

4. **完璧主義**
   - 70%で進める
   - 早期のフィードバックを重視

## 成功指標（KPI）

```yaml
weekly_metrics:
  - タスク完了数（目標: 15-20個/週）
  - サイクルタイム（目標: 2日以内）
  - ブロッカー解消時間（目標: 4時間以内）
  
monthly_metrics:
  - 機能リリース数
  - ユーザーフィードバック反映率
  - チーム満足度
```

## まとめ

3人の小規模チームでは、シンプルさと速度が鍵。Linear上ですべてを完結させ、Claude Codeで作業を自動化することで、コミュニケーションコストを最小化しながら生産性を最大化できます。