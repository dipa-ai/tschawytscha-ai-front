# Tshawytscha AI Frontend

The frontend for [tshawytscha.ai](https://tshawytscha.ai) — an AI chatbot powered by OpenAI's GPT-4o. Built with React 18 and Vite.

This is the client-side SPA that communicates with a separate backend service (`tshawytscha-ai-back`) for authentication and chat API calls.

## Prerequisites

- Node.js 22+
- npm

## Getting Started

```bash
git clone https://github.com/dipa-ai/tschawytscha-ai-front.git
cd tschawytscha-ai-front
npm install
npm run dev
```

> **Note:** The dev server requires the backend service running at `/api` for authentication (`/api/init`) and chat (`/api/chat`) endpoints. Configure Vite proxy or run the backend alongside.

## Scripts

| Command             | Description                        |
|---------------------|------------------------------------|
| `npm run dev`       | Start Vite dev server              |
| `npm run build`     | Production build to `dist/`        |
| `npm run preview`   | Preview the production build       |
| `npm run lint`      | Run ESLint                         |

## Project Structure

```
src/
  main.jsx              # App entry point
  App.jsx               # Root component (auth, chat state, API calls)
  App.css
  index.css
  components/
    Header/             # App header
    Conversation/       # Chat message list
    QuestionInput/      # User text input
    CatchButton/        # Submit button
```

Each component has co-located `.jsx` and `.css` files.

## Deployment

- **Docker:** Multi-stage build (Node 22 Alpine + nginx) — serves static files on port 80
- **Kubernetes:** Helm chart in `install/kubernetes/chart/` with Envoy Gateway HTTPRoute
- **CI/CD:** GitHub Actions builds and pushes Docker image + Helm chart on `v*` tags

```bash
# Build Docker image locally
docker build -t tschawytscha-ai-front .
docker run -p 8080:80 tschawytscha-ai-front
```

## License

[Apache 2.0](LICENSE)
