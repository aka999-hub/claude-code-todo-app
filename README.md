# claude-code-todo-app

### claude code を dev container で動作させる .devcontainer 関連

[anthropics/claude-code](https://github.com/anthropics/claude-code/tree/main/.devcontainer)

### claude code 起動

```
claude
```

### CLAUDE.md の作成

- 要件の作成
- （プロジェクトで使ってきた）コード規約、ベストプラクティス 等があったら INPUT にする
- claude code 自身に作ってもらう

```
CLAUDE.mdのベストプラクティスを調査して、シンプルなTodoアプリ用のCLAUDE.mdを作ってください。技術スタックはReact Router v7, SQLite, Vitest, Playwrightを使いたいです。デプロイ先はCloudeflareで、Cloudeflare Workersを使いたいです。実装はNEVER始めないでください。
```

```実行結果
> CLAUDE.mdのベストプラクティスを調査して、シンプルなTodoアプリ用のCLAUDE.mdを作ってください。技術スタックはReact
  Router v7, SQLite, Vitest, Playwrightを使いたいです。デプロイ先はCloudeflareで、Cloudeflare
  Workersを使いたいです。実装はNEVER始めないでください。
  ⎿  ⧉ Selected 1 lines from README.md in Visual Studio Code

● Update Todos
  ⎿  ☐ Research CLAUDE.md best practices from Claude Code documentation
     ☐ Create CLAUDE.md for Todo app with React Router v7, SQLite, Vitest, Playwright, Cloudflare Workers

● Fetch(https://docs.anthropic.com/en/docs/claude-code/claude_code_docs_map.md)
  ⎿  Received 16.7KB (200 OK)

● Fetch(https://docs.anthropic.com/en/docs/claude-code/memory)
  ⎿  Received 2MB (200 OK)

● Fetch(https://docs.anthropic.com/en/docs/claude-code/examples/project-setup)
  ⎿  Received 2MB (200 OK)

● Update Todos
  ⎿  ☒ Research CLAUDE.md best practices from Claude Code documentation
     ☐ Create CLAUDE.md for Todo app with React Router v7, SQLite, Vitest, Playwright, Cloudflare Workers

● Write(CLAUDE.md)
  ⎿  Wrote 57 lines to CLAUDE.md
     # Todo App Project Configuration
     ## Project Overview
     This is a modern Todo application built with:
     - **Frontend**: React with React Router v7
     - **Database**: SQLite
     - **Testing**: Vitest for unit tests, Playwright for e2e tests
     - **Deployment**: Cloudflare Workers
     ## Technology Stack Details
     … +47 lines (ctrl+r to expand)

● Update Todos
  ⎿  ☒ Research CLAUDE.md best practices from Claude Code documentation
     ☒ Create CLAUDE.md for Todo app with React Router v7, SQLite, Vitest, Playwright, Cloudflare Workers

● CLAUDE.mdを作成しました。このファイルはReact Router v7、SQLite、Vitest、Playwright、Cloudflare
  Workersを使用するTodoアプリの開発に必要な情報を含んでいます。
```

### git コミットコマンド

```
chore: add CLAUDE.md
```
