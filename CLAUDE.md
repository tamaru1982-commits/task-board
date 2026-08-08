# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

A React + Vite task board app. Add tasks via text input, toggle completion with a checkbox, delete tasks, and completed tasks render grayed out with strikethrough.

## デプロイ先

https://tamaru1982-commits.github.io/task-board/

## 技術スタック

- React 18 (`react`, `react-dom`)
- Vite 5 + `@vitejs/plugin-react`（開発サーバー・バンドラー）
- プレーンCSS（CSSフレームワーク・CSS-in-JSなし）
- 永続化は `localStorage` のみ（バックエンド・DBなし）
- GitHub Actions + GitHub Pages（デプロイ）

## コンポーネントの命名規約

- コンポーネントファイルは `PascalCase.jsx`（例: `App.jsx`）、default export。
- 対応するスタイルシートは同名の `ComponentName.css`（例: `App.css`）で、コンポーネントと1対1にする。
- イベントハンドラ関数は「動詞+対象」の camelCase（例: `addTask`, `toggleTask`, `deleteTask`）。
- CSSクラス名は kebab-case とし、要素の役割を表す名前にする（例: `task-form`, `task-list`, `delete-button`）。完了状態などの修飾は `done` のような単一の状態クラスを併記する（例: `task done`）。

## Commands

- `npm install` — install dependencies
- `npm run dev` — start the Vite dev server (default port 5173)
- `npm run build` — production build to `dist/`
- `npm run preview` — preview the production build

## Architecture

Single-component app: `src/App.jsx` holds all task state (`{ id, text, done }[]`) via `useState` and handles add/toggle/delete inline. Tasks persist to `localStorage` (key `task-board:tasks`) via a `useEffect` that runs on every state change; initial state is read from `localStorage` in `useState`'s lazy initializer. No backend. Styling is plain CSS in `src/App.css` (`.task.done` applies the grayed-out/strikethrough look) and `src/index.css` (page-level defaults).

## Deployment

Deploys via `.github/workflows/deploy.yml`, which builds with Vite and publishes `dist/` to GitHub Pages (see デプロイ先 above) on every push to `main`. `vite.config.js` sets `base: '/task-board/'` to match the Pages project-site path — required because it's served from a subpath, not the domain root.

One-time manual step (not automatable from here): in the repo's Settings → Pages, set **Source** to **GitHub Actions**.

## Git ワークフロー

- コードに変更を加えたら、その都度コミットしてGitHubにプッシュすること（変更をローカルに留め置かない）。
- コミットメッセージは変更内容が分かるよう簡潔に書く。
- プッシュ前に `git status` / `git diff` で変更内容を確認する。
- force push など破壊的な操作は行わない。
