# Base44 Dev Environment

## Project Overview
Single-file static web app (`index.html`) — a product catalog ("T.M.IMPORT44").
React 18 (UMD) + Babel standalone are loaded via CDN and transpiled in-browser.
No build step, no backend, no package manager.

## Running
```
docker compose -f docker-compose.base44.yml up -d
```
Serves `index.html` via nginx on host port 3000. Edits to `index.html` appear on browser refresh (no live-reload server needed).

## Verification
- `curl -s http://localhost:3000/ | grep T.M.IMPORT44` confirms the page is served.
- No external credentials required.
