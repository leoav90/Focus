# Repository Guidelines

## Project Structure & Module Organization

This repository is a small static web app. The application lives in `index.html`, which contains the HTML, CSS, and vanilla JavaScript in one file. There is no backend, package manifest, build step, or separate asset directory yet. Local app state is stored in `localStorage`, primarily under `projects-data-v1`; preserve backward compatibility when changing persistence or schema migration logic.

Hidden folders such as `.git`, `.codex`, and `.agents` are tooling metadata and should not be edited as application source.

## Build, Test, and Development Commands

There is no install step. Open `index.html` directly in a browser to run the app.

Useful local checks:

```powershell
& 'C:\Users\leandroa\.cache\codex-runtimes\codex-primary-runtime\dependencies\node\bin\node.exe' -e "const fs=require('fs'); const html=fs.readFileSync('index.html','utf8'); const m=html.match(/<script>([\s\S]*)<\/script>/); new Function(m[1]); console.log('script-parse-ok');"
```

This validates that the embedded JavaScript parses. Use browser manual testing for behavior.

## Coding Style & Naming Conventions

Use vanilla JavaScript, plain CSS, and semantic HTML. Keep the existing style: two-space indentation, `var` declarations, descriptive function names, and section comments such as `// ---------- render ----------`. Prefer small helper functions over large inline blocks when logic is reused.

Keep user-facing text in Spanish to match the current UI. Use existing patterns for icons: inline SVG helper functions such as `iconPlus`, `iconInfo`, and `svgWrap`.

## Testing Guidelines

No automated test framework is configured. For each change, run the JavaScript parse check above and complete focused manual tests in the browser. For storage changes, test migration from older `localStorage` data, export/import flows, invalid JSON handling, and persistence after reload.

Name ad hoc verification notes by feature in PR descriptions, for example: `backup import`, `task migration`, or `Focus de hoy`.

## Commit & Pull Request Guidelines

Recent commits use short, imperative summaries, for example `Add backup import layer` and `Enrich task model`. Follow that pattern.

Pull requests should include a concise summary, manual test steps, screenshots or screen recordings for UI changes, and notes about persistence/schema compatibility. Mention any remaining risks, especially around `localStorage` quota, schema migrations, or data loss prevention.

## Security & Data Safety

Do not add backend calls or external data transmission unless explicitly requested. Before import, migration, or destructive changes, preserve local backup behavior and avoid deleting existing project/task fields during compatibility phases.
