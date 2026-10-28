# BuildSense — Construction Intelligence

Construction-site photo guidance, property estimates, project planning, weather advice, and a construction assistant for students and site teams.

## Run & Operate

- Click **Run** in Replit to start the web app and API service together.
- `pnpm install` — install the frontend and workspace dependencies
- `uv sync` — install FastAPI and Gemini dependencies
- `pnpm --filter @workspace/api-server run dev` — run FastAPI locally (port 8080)
- `pnpm --filter @workspace/construction-intel run dev` — run the React/Vite web app
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- Optional secret: `GEMINI_API_KEY` — keep it in Replit Secrets; never expose it in frontend code
- AI features are paused by default. Set `BUILDSENSE_AI_ENABLED=true` on the API service only after Google project access is confirmed

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9, Python 3.11
- Frontend: React + Vite
- API: FastAPI + Pydantic
- AI: Optional Google Gemini via `google-genai`; disabled by default
- Saved plans: SQLite
- Weather: Open-Meteo
- API codegen: Orval (from OpenAPI spec)

## Where things live

- `artifacts/construction-intel/` — React application and setup notes
- `artifacts/api-server/python/main.py` — FastAPI routes and app logic
- `artifacts/api-server/data/` — local SQLite data (ignored by Git)
- `lib/api-spec/openapi.yaml` — API contract and generated frontend hooks

## Architecture decisions

- The API artifact serves FastAPI at `/api`; the React app uses generated API hooks.
- Gemini photo reviews and chat are server-gated by `BUILDSENSE_AI_ENABLED`; the planner uses a transparent rules-based schedule while AI is paused.
- Uploaded photos are sent inline for analysis and are not saved by the app.
- Property estimates are explicitly indicative and do not use live comparable sales.
- Weather data comes from the public Open-Meteo forecast endpoint.

## Product

BuildSense provides optional AI safety-photo and concrete-crack reviews, indicative INR property estimates, rules-based or AI-assisted schedules, city weather guidance, and optional construction Q&A.

## User preferences

_Populate as you build — explicit user instructions worth remembering across sessions._

## Gotchas

- Gemini is intentionally disabled by default; enable it only after a usable API key and Google project access are confirmed.
- Restart `artifacts/api-server: API Server` after changing FastAPI code.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
