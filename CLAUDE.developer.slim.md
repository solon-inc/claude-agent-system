# 開発実装エージェント実行指示書 v2.0.0

## 基本設定
- executor:developerラベルのタスクを自動実行
- 30分ごとに新規タスクを確認
- 優先度0(Urgent)→4(None)順で処理

## 必須フォルダ構造
```
.claude/
  developer_config.yaml
  developer_context.yaml
  task_details/
  daily_status.md
src/
tests/
docs/
.devcontainer/
```

## 自動実行フロー

### 1.タスク検出時
```bash
mcp__linear__linear_searchIssues
- labels: ["developer"]
- states: ["Todo", "In Progress"]
→優先度順ソート→最優先タスク選択
```

### 2.設計フェーズ(必須)
```bash
mcp__linear__linear_updateIssue(stateId:"In Progress")
mcp__github__create_issue("[Linear-ID] Design: タスク名")
mcp__perplexity-ask__perplexity_research(技術調査)
→実現可能性評価(低/中/高)
→ユーザー承認待ち(yes/no)
mcp__slack__slack_post_message("🎨設計完了:承認待ち")
```

### 3.実装フェーズ(TDD)
```bash
# Red
Write("tests/test_feature.py", 失敗テスト)
Bash("pytest tests/test_feature.py")→失敗確認
git commit -m "[Linear-ID] test: Add failing test"

# Green  
Write("src/feature.py", 最小実装)
Bash("pytest")→成功確認
git commit -m "[Linear-ID] feat: Implement minimum"

# Refactor
Edit("src/feature.py", リファクタリング)
Bash("pytest && ruff check && mypy")
git commit -m "[Linear-ID] refactor: Improve code"

mcp__github__add_issue_comment(進捗詳細)
mcp__slack__slack_post_message("🚀実装完了")
```

### 4.PR作成
```bash
gh pr create --title "[Linear-ID] タスク名" --body "$(cat <<'EOF'
## 概要
Linear: https://linear.app/team/issue/Linear-ID
Fixes #github-issue

## 実装内容
- 機能説明
- テストカバレッジ: X%
- パフォーマンス: Xms

## チェックリスト
- [x] テスト追加
- [x] 型チェック通過
- [x] Lint通過
EOF
)"

mcp__linear__linear_updateIssue(stateId:"In Review")
mcp__slack__slack_post_message("📝PR作成:レビュー待ち")
```

## コンテナ設定

### Dockerfile
```dockerfile
FROM python:3.11-slim
WORKDIR /app
RUN pip install --no-cache-dir pytest pytest-watch pytest-cov ruff mypy
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
CMD ["pytest-watch", "--runner", "pytest -xvs"]
```

### docker-compose.yml
```yaml
version: '3.8'
services:
  app:
    build: .
    volumes:
      - .:/app
    environment:
      - LINEAR_API_KEY=${LINEAR_API_KEY}
      - GITHUB_TOKEN=${GITHUB_TOKEN}
```

## 必須コマンド定義

### "自分のタスクを確認して実行"
1. mcp__linear__linear_searchIssues(labels:["developer"],states:["Todo","In Progress"])
2. 優先度順ソート
3. 最優先タスク自動実行

### "Linear issue XXXを実装"
1. mcp__linear__linear_getIssueById(id:"XXX")
2. 設計フェーズ→承認→TDD実装→PR作成

### "設計フェーズを開始"
1. 技術調査(Perplexity)
2. 実現可能性評価
3. GitHub Issue作成
4. ユーザー承認待ち

### "コンテナ環境をセットアップ"
1. Write("Dockerfile")
2. Write("docker-compose.yml")
3. Write(".dockerignore")
4. Bash("docker-compose build")

### "開発環境をチェック"
```bash
Bash("python --version && pytest --version && ruff --version && mypy --version && gh --version")
```

## エラー時対応
```bash
mcp__linear__linear_addIssueComment("エラー発生:[内容]")
mcp__slack__slack_post_message("⚠️ブロッカー:[Linear-ID]")
```

## 重要制約
1. executor:developerラベルのタスクのみ実行
2. 設計承認なしに実装禁止
3. TDDサイクル厳守
4. 全活動をGitHub記録
5. コンテナベース開発推奨
6. Slack通知必須(mcp__slack__slack_post_message)
7. 30分ごと自動実行