# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Tshawytscha AI is a chatbot frontend that communicates with a separate backend service via `/api/*` endpoints. The frontend is a React 18 SPA built with Vite, using JSX (not TypeScript). It uses the OpenAI SDK client-side only for types — actual AI calls go through the backend's `/api/chat` endpoint. Authentication is cookie-based via `/api/init`.

## Commands

- **Dev server:** `npm run dev`
- **Build:** `npm run build`
- **Lint:** `npm run lint` (ESLint flat config with react/react-hooks/react-refresh plugins)
- **Preview production build:** `npm run preview`

## Architecture

- **Entry:** `src/main.jsx` renders `<App />` into `#root`
- **App.jsx:** Main component managing auth state, chat messages, and API calls. Calls `/api/init` on mount for cookie-based auth, then `/api/chat` for conversations.
- **Components:** Each in `src/components/<Name>/` with co-located `.jsx` and `.css` files:
  - `Header` — app header (supports `minimal` prop for error states)
  - `Conversation` — renders chat message list
  - `QuestionInput` — text input for user questions
  - `CatchButton` — submit button
- **Styling:** Component-scoped CSS files + global `index.css` + inline styles in `index.html` (gradient background, bubble animations)

## Deployment

- Docker multi-stage build: builds with Node 22, serves static files with nginx on port 80 (config in `nginx.conf`)
- Helm chart in `install/kubernetes/chart/` deploys to Kubernetes with Envoy Gateway HTTPRoute
- CI: GitHub Actions builds and pushes Docker image + Helm chart to OCI registry on `v*` tags
- Domain: `tshawytscha.ai` — frontend serves static files, `/api` routes to `tshawytscha-ai-back` service
