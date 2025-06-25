# Claude Agent System

Claude Code用の特殊エージェント（TaskManager、Developer、DataGatherer）の管理システム

## 概要

このリポジトリは、Claude Codeで使用する3つの特殊エージェントのCLAUDE.mdファイルを管理・開発するためのものです。各エージェントは特定の役割に特化し、連携してプロジェクトを効率的に進めます。

## エージェント一覧

### 1. TaskManager (`CLAUDE.taskmanager.md`)
- **役割**: Linearを中心としたタスク管理
- **バージョン**: 2.0.0
- **主な機能**: プロジェクト管理、タスク作成・更新、レポート生成

### 2. Developer (`CLAUDE.developer.md`)
- **役割**: コード実装に特化した開発
- **バージョン**: 1.0.0
- **主な機能**: コード実装、テスト作成、デバッグ、PR作成

### 3. DataGatherer (`CLAUDE.sample.md`)
- **役割**: プロジェクト情報の自動収集・整理
- **バージョン**: 1.3.0
- **主な機能**: 情報収集、ドキュメント処理、レポート生成、会議メモ管理

## ドキュメント

- [ユーザージャーニー](USER_JOURNEY.md) - 企画から開発までの具体的な活用方法
- [マイルストーン管理](LINEAR_MILESTONE_MANAGEMENT.md) - Linear上でのマイルストーン管理方法
- [エージェント分離ガイド](AGENT_SEPARATION_GUIDE.md) - エージェントの役割分担
- [Linear運用ガイド](SMALL_TEAM_LINEAR_OPERATION.md) - 小規模チームでのLinear運用
- [チケット駆動開発](LINEAR_TICKET_DRIVEN_DEVELOPMENT.md) - Linear連携開発ガイド

## 使い方

各エージェントのCLAUDE.mdファイルを、使用したいプロジェクトの`.claude/`フォルダにコピーして使用します。

```bash
# 例: TaskManagerを使用する場合
cp CLAUDE.taskmanager.md /path/to/your/project/.claude/CLAUDE.md
```

## 重要な制約

このプロジェクトでは以下の制約があります：

1. **CLAUDE.local.mdのみを更新すること** - それ以外のファイルは指示があるまで更新禁止
2. **GitHubへの操作はMCPツールにより行う**
3. **ユーザーからの指示完了時はSlackへ通知**

## ライセンス

このプロジェクトはMITライセンスの下で公開されています。