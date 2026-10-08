# AGENTS.md

## Project Overview
Single-page static HTML app ("T.M.IMPORT44 — Catálogo") — a product catalog/store built with React 18 (loaded via CDN UMD), compiled in-browser with Babel standalone. No build step, no npm dependencies, no backend server.

## Architecture
- `index.html` is the entire application — React components written as `<script type="text/babel">` JSX, compiled client-side by Babel.
- Data backend is Supabase (REST API + auth). The Supabase URL and anon key are hardcoded in `index.html` (public client-side values, not secrets).
- No server-side code; nginx serves the static file.

## Setup
- `docker compose -f docker-compose.base44.yml up -d` — serves `index.html` via nginx on port 3000.
- No credentials needed — Supabase anon key is embedded in the HTML.

## Verification
- `curl -s -o /dev/null -w "%{http_code}" http://localhost:3000/` should return 200.
- The page title should be "T.M.IMPORT44 — Catálogo".

## Notes
- Editing `index.html` requires a preview reload (no live-reload dev server; static file served by nginx).
- React/ReactDOM/Babel are loaded from unpkg CDN, so the preview needs network access to unpkg.com.
