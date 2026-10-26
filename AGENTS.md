# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Website for Creative Code Kortrijk (CCK), a creative coding club in Kortrijk, Belgium. Astro 7 static site, plain CSS (no CSS framework), Space Grotesk font via Fontsource. This repo is a classroom starter (Howest Web 3 "Git Party"): `readme 2.md` holds the challenge instructions; `readme.md` holds the Figma design links and credits (and is where hidden-code digit locations should be documented).

## Stack & constraints

### Commands

- `npm run dev` — dev server (`--host`); `npm start` — dev server without `--host`
- `npm run build` — static build; fails if any content frontmatter violates the schema
- `npm run preview` — serve the build

No test runner or linter is configured.

### Architecture

- **Content collections** are defined in `src/content.config.ts` (glob loader over `src/content/<name>/*.md`). Schemas are strict: a missing frontmatter field breaks the build. Image fields use `image()` and are relative paths to files in that collection's `img/` folder (e.g. `pic: img/casey.jpeg`).
  - `workshops`: title, image
  - `team`: name, function, bio, pic
  - `foundations`: title, description
  - `news` is intentionally not defined yet (a later challenge); starter items live in `resources/news/` and should be copied to `src/content/news/` (frontmatter: title, date).
- **Layouts**: `src/layouts/Base.astro` (head, Header, Footer, global styles) wraps all pages; `Markdown.astro` is the detail-page layout with `top`, default, and `sidebar` slots.
- **Components** in `src/components/`: each collection has a list component (`Workshops`, `Foundations`, `Team`) plus a card component (`*Card`). `Hero` is the home page header. `Code` is for a hidden 4-digit code game.
- **Pages**: `src/pages/index.astro` composes the home page; `news.astro`; `about.md`.
- **Detail pages** don't exist yet: starter templates are in `resources/{workshops,foundations,team}/detailpage` (not in `src/`). They are meant to become dynamic routes (e.g. `src/pages/<collection>/[id].astro`) using `getStaticPaths` with the entry id.

### Placeholders

Starter files contain `##WHAT-SHOULD-BE-HERE##` placeholders (e.g. in `src/pages/news.astro` and the detail page templates) that must be replaced with real logic/content. Search with `grep -rn "##" src resources` to find remaining ones.

### Workflow conventions

- Git branches follow `feature/<name>` and merge to `main` via GitHub pull requests; humans resolve merge conflicts and click merge, not the agent.
- Per the challenge instructions, an `AGENTS.md` (sections: Project, Stack & constraints) is expected in the repo root.
- Deployment target is GitHub Pages via the Astro GitHub Actions workflow (not yet added).

Redo