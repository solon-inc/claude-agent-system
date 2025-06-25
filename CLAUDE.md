# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## プロジェクト概要

このプロジェクトは、Claude Code用の特殊エージェント（TaskManager、Developer、DataGatherer）のCLAUDE.mdファイルを管理・開発するためのリポジトリです。**通常のプロジェクトとは異なり、最終的にCLAUDE.local.mdファイルのみを更新することが目的です。**

## 重要な制約

**⚠️ 重要: このプロジェクトでは以下の制約を必ず守ってください**

1. **CLAUDE.local.mdのみを更新すること** - それ以外のファイルは指示があるまで更新禁止
2. **CLAUDE.taskmanager.mdはClaude Codeが確実に目的を達成できるように記載** - 人間にとっての読みやすさは無視してよい
3. **GitHubへの操作はClaude Codeに設定済みのMCPツールにより行う**
4. **ユーザーからの指示が完了するたびにSlackへMCPツールで通知を投稿**

## プロジェクト構造

```
TaskManager/
├── CLAUDE.md                               # このファイル（プロジェクトガイド）
├── CLAUDE.local.md                         # 更新対象ファイル（存在する場合）
├── CLAUDE.taskmanager.md                   # TaskManagerエージェント定義
├── CLAUDE.developer.md                     # Developerエージェント定義
├── CLAUDE.sample.md                        # DataGathererエージェント定義（サンプル）
├── AGENT_SEPARATION_GUIDE.md               # エージェント分離ガイド
├── LINEAR_TICKET_DRIVEN_DEVELOPMENT.md     # Linear連携開発ガイド
└── SMALL_TEAM_LINEAR_OPERATION.md          # 小規模チームLinear運用ガイド
```

## エージェント概要

### 1. TaskManager (CLAUDE.taskmanager.md)
- **役割**: Linearを中心としたタスク管理エージェント
- **バージョン**: 2.0.0
- **特徴**: Linear First方針で、すべての情報をLinear内に集約
- **主な機能**: プロジェクト管理、タスク作成・更新、レポート生成

### 2. Developer (CLAUDE.developer.md)
- **役割**: コード実装に特化した開発エージェント
- **バージョン**: 1.0.0
- **特徴**: Linear上のタスクを受け取り、実装からデプロイまで担当
- **主な機能**: コード実装、テスト作成、デバッグ、PR作成

### 3. DataGatherer (CLAUDE.sample.md)
- **役割**: プロジェクト情報を自動収集・整理する専門エージェント
- **バージョン**: 1.3.0
- **特徴**: MCPツールを使用して情報収集し、Markdown形式で管理
- **主な機能**: 情報収集、ドキュメント処理、レポート生成、会議メモ管理

## 開発時の注意事項

### MCPツール利用
すべてのMCPツール呼び出しは必ず`mcp__`で始まるツール名を使用：
- `mcp__linear__*` - Linear連携
- `mcp__github__*` - GitHub連携
- `mcp__slack__*` - Slack連携
- `mcp__perplexity-ask__*` - 外部情報収集
- `mcp__markdownify__*` - ドキュメント変換

### Slack通知
ユーザーからの指示が完了するたびに、必ず以下の形式で通知：
```javascript
mcp__slack__slack_post_message({
  channel_id: "[設定されたチャンネルID]",
  text: "✅ [タスク内容] が完了しました"
})
```

### エージェント更新時の作業フロー
1. 対象エージェントのCLAUDE.*.mdファイルを分析
2. 改善点や機能追加を検討
3. **CLAUDE.local.mdに変更内容を記載**（他のファイルは更新しない）
4. GitHubへの操作はMCPツールで実行
5. Slackへ完了通知を送信

## よく使うコマンド

### エージェント分析
- 「TaskManagerエージェントの機能を分析して」
- 「Developerエージェントの改善点を提案して」
- 「DataGathererのバージョンアップ内容を確認して」

### 機能追加・改善
- 「TaskManagerにXXX機能を追加したい」
- 「DeveloperのLinear連携を強化して」
- 「DataGathererの会議メモ処理を改善して」

### ドキュメント確認
- 「エージェント分離ガイドの内容を確認」
- 「Linear運用ガイドを要約して」

## Tips

1. **エージェントの役割分担を明確に**: 各エージェントは特定の責務に特化
2. **Linear中心の情報管理**: TaskManagerを中心に、他エージェントもLinearと連携
3. **自動化の推進**: 定型作業はMCPツールで自動化
4. **バージョン管理**: エージェント更新時は必ずバージョン番号を更新

---

最終更新: 2025-01-25