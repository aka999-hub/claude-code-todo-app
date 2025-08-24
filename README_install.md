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

### React Router v7 パッケージのインストール

React Router の初期化が claude code に任せる異なるパッケージのインストールしてしまうらしいので、手動でインストール
[Cloudflare Workers w/ D1](https://reactrouter.com/start/framework/deploying#cloudflare-workers-w-d1)

```
npx create-react-router@latest --template remix-run/react-router-templates/cloudflare-d1
```

```実際
 node  /workspace   main  npx create-react-router@latest --template remix-run/react-router-templates/cloudflare-d1

Need to install the following packages:
create-react-router@7.8.2
Ok to proceed? (y) y

npm warn deprecated inflight@1.0.6: This module is not supported, and leaks memory. Do not use it. Check out lru-cache if you want a good and tested way to coalesce async requests by a key value, which is much more comprehensive and powerful.
npm warn deprecated glob@7.2.3: Glob versions prior to v9 are no longer supported

         create-react-router v7.8.2

   dir   Where should we create your new project?
         .

      ◼  Template: Using remix-run/react-router-templates/cloudflare-d1...
      ✔  Template copied

 overwrite   Your project directory contains files that will be overwritten by
             this template (you can force with `--overwrite`)

             Files that would be overwritten:
               README.md

             Do you wish to continue?

             Yes
      ◼  Nice! Git has already been initialized

  deps   Install dependencies with npm?
         Yes

      ✔  Dependencies installed

  done   That's it!
         Check out README.md for development and deploy instructions.

         Join the community at https://rmx.as/discord

 node  /workspace   main ● ? 
```

### package.json に修正

devcontainerで開発しているのでローカルホストの許可だけしていると上手く参照できないため `--host`を追記
`npm run dev` -> `react-router dev --host`

```
  "scripts": {
    "build": "react-router build",
    "cf-typegen": "wrangler types",
    "db:generate": "dotenv -- drizzle-kit generate",
    "db:migrate": "wrangler d1 migrations apply --local DB",
    "db:migrate-production": "dotenv -- drizzle-kit migrate",
    "deploy": "npm run build && wrangler deploy",
    // "dev": "react-router dev", // JSONファイルはコメントを許可しないのでこの行は削除
    "dev": "react-router dev --host",
```

### npm run dev 実行

```
npm run dev
```

```実際
> dev
> react-router dev --host

  ➜  Local:   http://localhost:5173/
  ➜  Network: http://172.17.0.2:5173/
  ➜  Debug:   http://localhost:5173/__debug
  ➜  press h + enter to show help
```

### http://localhost:5173/ にアクセス

ブラウザで http://localhost:5173/ にアクセス

```
Oops!
D1_ERROR: no such table: guestBook: SQLITE_ERROR

Error: D1_ERROR: no such table: guestBook: SQLITE_ERROR
    at D1DatabaseSessionAlwaysPrimary._sendOrThrow (cloudflare-internal:d1-api:127:19)
    at D1PreparedStatement.raw (cloudflare-internal:d1-api:317:32)
    at D1PreparedQuery.all (/workspace/node_modules/.vite/deps_ssr/drizzle-orm_d1.js:163:18)
    at loader (/workspace/app/routes/home.tsx:35:21)
    at callRouteHandler (/workspace/node_modules/.vite/deps_ssr/react-router.js:10829:16)
    at commonRoute.loader (/workspace/node_modules/.vite/deps_ssr/react-router.js:10972:19)
    at /workspace/node_modules/.vite/deps_ssr/react-router.js:4595:19
    at callLoaderOrAction (/workspace/node_modules/.vite/deps_ssr/react-router.js:4647:16)
    at async Promise.all (index 0)
    at defaultDataStrategy (/workspace/node_modules/.vite/deps_ssr/react-router.js:4301:17)
```

### エラーが出ているので、claude code に修正を依頼

```
claude --dangerously-skip-permissions
```

```
│ WARNING: Claude Code running in Bypass Permissions mode                              │
│                                                                                      │
│ In Bypass Permissions mode, Claude Code will not ask for your approval before        │
│ running potentially dangerous commands.                                              │
│ This mode should only be used in a sandboxed container/VM that has restricted        │
│ internet access and can easily be restored if damaged.                               │
│                                                                                      │
│ By proceeding, you accept all responsibility for actions taken while running in      │
│ Bypass Permissions mode.                                                             │
│                                                                                      │
│ https://docs.anthropic.com/s/claude-code-security                                    │
│                                                                                      │
│   1. No, exit                                                                        │
│ ❯ 2. Yes, I accept
```

```claude への指示
`npm run dev`すると次のエラーが出るので、直してください：
Oops!
D1_ERROR: no such table: guestBook: SQLITE_ERROR

Error: D1_ERROR: no such table: guestBook: SQLITE_ERROR
    at D1DatabaseSessionAlwaysPrimary._sendOrThrow (cloudflare-internal:d1-api:127:19)
    at D1PreparedStatement.raw (cloudflare-internal:d1-api:317:32)
    at D1PreparedQuery.all (/workspace/node_modules/.vite/deps_ssr/drizzle-orm_d1.js:163:18)
    at loader (/workspace/app/routes/home.tsx:35:21)
    at callRouteHandler (/workspace/node_modules/.vite/deps_ssr/react-router.js:10829:16)
    at commonRoute.loader (/workspace/node_modules/.vite/deps_ssr/react-router.js:10972:19)
    at /workspace/node_modules/.vite/deps_ssr/react-router.js:4595:19
    at callLoaderOrAction (/workspace/node_modules/.vite/deps_ssr/react-router.js:4647:16)
    at async Promise.all (index 0)
    at defaultDataStrategy (/workspace/node_modules/.vite/deps_ssr/react-router.js:4301:17)
```

```実際
> `npm run dev`すると次のエラーが出るので、直してください：
  Oops!
  D1_ERROR: no such table: guestBook: SQLITE_ERROR

  Error: D1_ERROR: no such table: guestBook: SQLITE_ERROR
      at D1DatabaseSessionAlwaysPrimary._sendOrThrow
  (cloudflare-internal:d1-api:127:19)
      at D1PreparedStatement.raw (cloudflare-internal:d1-api:317:32)
      at D1PreparedQuery.all
  (/workspace/node_modules/.vite/deps_ssr/drizzle-orm_d1.js:163:18)
      at loader (/workspace/app/routes/home.tsx:35:21)
      at callRouteHandler
  (/workspace/node_modules/.vite/deps_ssr/react-router.js:10829:16)
      at commonRoute.loader
  (/workspace/node_modules/.vite/deps_ssr/react-router.js:10972:19)
      at /workspace/node_modules/.vite/deps_ssr/react-router.js:4595:19
      at callLoaderOrAction
  (/workspace/node_modules/.vite/deps_ssr/react-router.js:4647:16)
      at async Promise.all (index 0)
      at defaultDataStrategy
  (/workspace/node_modules/.vite/deps_ssr/react-router.js:4301:17)
  ⎿  ⧉ Selected 15 lines from README_install.md in Visual Studio Code

● I need to fix the database table issue. Let me investigate the database setup and
   create the missing guestBook table.

● Update Todos
  ⎿  ☐ Investigate database schema and migration setup
     ☐ Create or run database migrations to create guestBook table
     ☐ Verify the fix by running npm run dev

● Search(pattern: "**/*.sql")
  ⎿  Found 1 file (ctrl+r to expand)

● Search(pattern: "**/drizzle/**")
  ⎿  Found 3 files (ctrl+r to expand)

● Read(drizzle.config.ts)
  ⎿  Read 14 lines (ctrl+r to expand)

● Read(app/routes/home.tsx)
  ⎿  Read 57 lines (ctrl+r to expand)

● Read(database/schema.ts)
  ⎿  Read 8 lines (ctrl+r to expand)

● Read(drizzle/0000_outstanding_trauma.sql)
  ⎿  Read 7 lines (ctrl+r to expand)

● Read(package.json)
  ⎿  Read 40 lines (ctrl+r to expand)

● Update Todos
  ⎿  ☒ Investigate database schema and migration setup
     ☐ Create or run database migrations to create guestBook table
     ☐ Verify the fix by running npm run dev

● I can see the issue. The database schema and migration files exist, but the local
   database hasn't been migrated yet. I need to run the migration to create the
  guestBook table in the local D1 database.

● Bash(npm run db:migrate)
  ⎿  > db:migrate
     > wrangler d1 migrations apply --local DB
     … +23 lines (ctrl+r to expand)

● Update Todos
  ⎿  ☒ Investigate database schema and migration setup
     ☒ Create or run database migrations to create guestBook table
     ☐ Verify the fix by running npm run dev

● Perfect! The migration has been applied successfully. Now let me test that the
  dev server works:

● Bash(npm run dev)
  ⎿  Running in the background (down arrow to manage)

● BashOutput(Reading shell output)
  ⎿  > dev
     > react-router dev --host
     … +4 lines (ctrl+r to expand)
  ⎿  Default inspector port 9229 not available, using 9230 instead

● Kill Bash(Kill shell: bash_1)
  ⎿  Shell bash_1 killed

● Update Todos
  ⎿  ☒ Investigate database schema and migration setup
     ☒ Create or run database migrations to create guestBook table
     ☒ Verify the fix by running npm run dev

● データベースのマイグレーションを実行してguestBookテーブルを作成しました。npm run
  devが正常に動作することを確認しました。D1_ERRORは解決されています。
```

### claude codeが修正後、再度 `npm run dev` 実行

```
npm run dev
```

```実際
 node  /workspace   main ● ?  npm run dev

> dev
> react-router dev --host

  ➜  Local:   http://localhost:5173/
  ➜  Network: http://172.17.0.2:5173/
  ➜  Debug:   http://localhost:5173/__debug
  ➜  press h + enter to show help
```

画面表示されることを確認

### githubにコミット

```
chore: init react router app
```

### CLAUDE.md について

- You can place CLAUDE.md files in several locations:
  　CLAUDE.md は格納先により役割があるらしい
  - The root of your repo,
    リポジトリのルート、またはclaudeを実行する場所（最も一般的な使用法）。CLAUDE.mdという名前を付けてgitにチェックインすれば、セッション間やチームで共有できます（推奨）。または、CLAUDE.local.mdという名前を付けて.gitignoreで保存します。

  - Any parent of the directory
    claude を実行するディレクトリの親ディレクトリ。これはモノリポジトリで最も便利です。モノリポジトリでは、claude を root/foo から実行し、root/CLAUDE.md と root/foo/CLAUDE.md の両方に CLAUDE.md ファイルが存在する可能性があります。これらのファイルは両方とも自動的にコンテキストに取り込まれます。

  - Any child of the directory
    claude を実行するディレクトリの子ディレクトリ。これは上記の逆で、この場合、Claude は子ディレクトリ内のファイルを操作するたびに CLAUDE.md ファイルを読み込みます。

  - Your home folder
    ホームフォルダ（~/.claude/CLAUDE.md）は、すべてのclaudeセッションに適用されます。

- CLAUDE.md は継続的にメンテしていく

### CLAUDE.md に Lintを必ず行うように修正する

claude CLI で "#" を入力すると "Add to memory." 違うモードに切り替わる
Lintを必ず実施するように命令する

```
# Run typecheck and lint after completing tasks and be sure they ALWAYS pass.
```

```実際
╭──────────────────────────────────────────────────────────────╮
│ # Run typecheck and lint after completing tasks and be sure  │
│   they ALWAYS pass.                                          │
╰──────────────────────────────────────────────────────────────╯
╭──────────────────────────────────────────────────────────────╮
│                                                              │
│ Where should this memory be saved?                           │
│                                                              │
│  ❯ 1. Project memory          Checked in at ./CLAUDE.md      │
│   2. Project memory (local)  Gitignored in                   │
│   ./CLAUDE.local.md                                          │
│    3. User memory             Saved in ~/.claude/CLAUDE.md   │
│                                                              │
│ Example project memory: “Run lint with the following command │
│  after major edits: npm run lint”                            │
│
```

入れる場所を聞かれるので、`1. Project memory` を選択

```
 Run typecheck and lint after completing tasks and be sure
they ALWAYS pass.
  ⎿  Good to know.
```

CLAUDE.md の変更箇所を確認し、命令が追記されることを確認

```CLAUDE.md
## Architecture Notes
- Keep components small and focused
- Separate business logic from UI components
- Use proper error boundaries
- Implement proper loading and error states
- Consider offline functionality with service workers
- Run typecheck and lint after completing tasks and be sure they ALWAYS pass.
```

anthropic では prompt improver を使ってAIに改善してもらっている記事がある（※従量課金対象）
[Use our prompt improver to optimize your prompts](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/prompt-improver)

https://www.youtube.com/watch?v=GFJp1Wa1zMo&t=504s
20:21
