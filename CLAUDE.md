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

## エージェントの追加ガイドライン

- **会話は日本語で** - すべてのエージェント間のコミュニケーションは日本語で行う

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

[以下、元のファイルの残りの内容を継続...]

---

最終更新: 2025-01-27