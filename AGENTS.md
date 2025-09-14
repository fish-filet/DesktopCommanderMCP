# Repository Guidelines

## Project Structure & Module Organization
- `src/` TypeScript ESM server code (strict mode). Key modules: `server.ts`, `command-manager.ts`, `terminal-manager.ts`, `search-manager.ts`, plus `tools/`, `handlers/`, `utils/`, and `data/` for assets. Build output goes to `dist/`.
- `test/` Node.js test scripts (no framework). Files start with `test` and end with `.js` (e.g., `test-default-shell.js`).
- `scripts/` maintenance utilities (e.g., `sync-version.js`, log tools). `docs/`, `screenshots/` contain documentation assets.
- Runtime config is stored under `~/.claude-server-commander/` (see `src/config.ts`). Do not edit `dist/` directly.

## Build, Test, and Development Commands
- `npm run build` — compile TypeScript to `dist/` and copy helper scripts.
- `npm start` — run `dist/index.js`.
- `npm run watch` — TypeScript watch mode for local development.
- `npm test` — build then execute `test/run-all-tests.js` to run all tests.
- Examples: run a single test after build: `node test/test-default-shell.js`. Clean build artifacts: `npm run clean`.
- Setup helpers: `npm run setup` to build and configure locally; debug server: `npm run start:debug`.

## Coding Style & Naming Conventions
- Language: TypeScript, ESM (`"type": "module"`), Node ≥ 18, strict typing on.
- Indentation: 2 spaces; include semicolons; prefer named exports; keep side effects in entrypoints only.
- Filenames: kebab-case for `.ts` in `src/` (e.g., `config-manager.ts`).
- Naming: PascalCase for types/interfaces (`ServerConfig`), camelCase for variables/functions, UPPER_SNAKE_CASE for global constants (e.g., `VERSION`).

## Testing Guidelines
- Framework: custom runner `test/run-all-tests.js`. Tests live in `test/` and must be `.js` starting with `test`.
- Run all: `npm test`. Run one: `node test/test-allowed-directories.js` (after `npm run build`).
- Keep tests deterministic and isolated. Avoid network access; write files only under `test/test_output` or temp paths.
- Focus coverage on core flows: terminal execution, search, config loading and mutations.

## Commit & Pull Request Guidelines
- Commits: concise, imperative mood (e.g., "Fix search session errors"), reference issues/PRs when relevant.
- PRs must: pass `npm run build` and `npm test`, include a clear description, link related issues, and update docs when behavior changes. Include logs or before/after snippets for behavior changes.
- CI runs Codespell; ensure spelling passes locally if available.

## Security & Configuration Tips
- Do not commit artifacts in `dist/` or user config from `~/.claude-server-commander/`.
- Changes to defaults (e.g., blocked commands in `src/config-manager.ts`) require rationale and tests.
