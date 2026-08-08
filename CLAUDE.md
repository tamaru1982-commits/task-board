# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

A React + Vite task board app. Add tasks via text input, toggle completion with a checkbox, delete tasks, and completed tasks render grayed out with strikethrough.

## Commands

- `npm install` — install dependencies
- `npm run dev` — start the Vite dev server (default port 5173)
- `npm run build` — production build to `dist/`
- `npm run preview` — preview the production build

## Architecture

Single-component app: `src/App.jsx` holds all task state (`{ id, text, done }[]`) via `useState` and handles add/toggle/delete inline. Tasks persist to `localStorage` (key `task-board:tasks`) via a `useEffect` that runs on every state change; initial state is read from `localStorage` in `useState`'s lazy initializer. No backend. Styling is plain CSS in `src/App.css` (`.task.done` applies the grayed-out/strikethrough look) and `src/index.css` (page-level defaults).

## Deployment

Deploys to GitHub Pages at `https://tamaru1982-commits.github.io/task-board/` via `.github/workflows/deploy.yml`, which builds with Vite and publishes `dist/` on every push to `main`. `vite.config.js` sets `base: '/task-board/'` to match the Pages project-site path — required because it's served from a subpath, not the domain root.

One-time manual step (not automatable from here): in the repo's Settings → Pages, set **Source** to **GitHub Actions**.

## Git ワークフロー

- コードに変更を加えたら、その都度コミットしてGitHubにプッシュすること（変更をローカルに留め置かない）。
- コミットメッセージは変更内容が分かるよう簡潔に書く。
- プッシュ前に `git status` / `git diff` で変更内容を確認する。
- force push など破壊的な操作は行わない。
