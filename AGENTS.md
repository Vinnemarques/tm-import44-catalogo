# AGENTS.md

## Project Overview
Single-page static HTML app ("T.M.IMPORT44 — Catálogo") using React 18 via CDN (UMD), Babel standalone for JSX compilation in-browser, and Supabase as backend (auth + data). No build step, no npm dependencies, no backend server.

## Running
- Served as a static file via nginx in `docker-compose.base44.yml` on port 3000.
- The Supabase URL and anon key are hardcoded in `index.html` — no external secrets needed.
- Edits to `index.html` are visible on browser refresh; call `reload_preview` after changes.
