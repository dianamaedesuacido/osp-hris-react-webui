# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

`osp-hris-react-webui` is the web UI for an HRIS (HR information system). Right now it is the stock Vite + React + TypeScript template: `src/App.tsx` is still the template's demo page, and no app features have been built yet. There is no router, state library, API client or test framework so far. Add them on purpose when they're needed, and update this file when you do.

## Commands

- `npm run dev`: Vite dev server with HMR (http://localhost:5173 by default)
- `npm run build`: type-checks first (`tsc -b`), then builds to `dist/`. A type error fails the build.
- `npm run lint`: ESLint over the whole repo
- `npm run preview`: serves the built `dist/`

No test runner is configured yet.

## Toolchain notes

- The versions are recent: React 19, Vite 8, TypeScript 6, ESLint 10 (flat config in `eslint.config.js`). `@vitejs/plugin-react` uses Oxc, not Babel or SWC. The React Compiler is not enabled.
- TypeScript uses project references. `tsconfig.json` points to `tsconfig.app.json` (covers `src/`, browser code) and `tsconfig.node.json` (covers `vite.config.ts`).
- These `tsconfig.app.json` settings shape how code is written:
  - `verbatimModuleSyntax`: import types with `import type`.
  - `erasableSyntaxOnly`: no `enum`, `namespace` or constructor parameter properties. Use union types or `as const` objects instead.
  - `noUnusedLocals` / `noUnusedParameters`: unused variables or parameters fail the build.
  - `allowImportingTsExtensions`: imports keep their `.tsx` extension, e.g. `import App from './App.tsx'`.
- ESLint includes `react-refresh/only-export-components`, so a component file should export only components or HMR will break.
- Files in `public/` are served from the site root. For example, `public/icons.svg` is used as `/icons.svg#id`. Assets in `src/assets/` are imported as modules instead.
