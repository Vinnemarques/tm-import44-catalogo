# AGENTS.md

## Project Overview
Single-file static HTML app (`index.html`) — a product catalog/store ("T.M.IMPORT44") built with React 18 (UMD via CDN) and in-browser Babel standalone for JSX transpilation. No build step, no package manager, no backend.

## Setup
- Served as static files via `nginx:alpine` (see `docker-compose.base44.yml`).
- The repo directory has restrictive permissions (700), so nginx must run as `root` — handled by the custom `nginx.base44.conf` mounted into the container.
- `docker compose -f docker-compose.base44.yml up -d` starts the server on port 3000.

## Key Fix (commit aa1a8fa)
Babel 8 (`@babel/standalone` latest from unpkg) defaults to the **automatic** JSX runtime, which emits ESM `import` statements. These fail in non-module inline scripts with `SyntaxError: Cannot use import statement outside a module`, preventing the app from rendering.

Fix: a small script after the Babel CDN load overrides the `react` preset to force the **classic** runtime (`React.createElement`), which is compatible with the UMD React loaded via `<script>` tags.

## Verification
- `curl http://localhost:3000/` returns 200 with the HTML content.
- Browser console shows only the expected Babel in-browser transformer warning (no errors).
- React renders the app (root div populated, loading screen visible).
