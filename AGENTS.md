# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Website for **Creative Code Kortrijk (CCK)**, a creative coding club in Kortrijk, Belgium. It is built by a team of three students as a "Git Party" class exercise: the assignment and its challenges are in `readme 2.md` (read it for the full task list). `readme.md` holds the design links (Figma design, illustration credits) and `README2.md` the team member names. The filesystem is case-insensitive (macOS), so `README.md` and `readme.md` are the same file.

Three people work in parallel, each with their own agent, on separate `feature/*` branches merged into `main` via pull requests (GitHub Flow). Per the assignment:
- Do **not** merge pull requests; humans do that on GitHub.
- When resolving merge conflicts, never drop a teammate's work. Propose a resolution and let the user review it before committing.

## Commands

```bash
npm install
npm run dev       # astro dev --host (dev server, exposed on LAN)
npm run build     # astro build -> dist/
npm run preview   # serve the built site
```

There are no tests or linters. `npm run build` is the check: content collection schemas are validated at build time, so a missing frontmatter field fails the build.

## Architecture

Astro 7 static site, no UI framework and no CSS framework.

- **Content collections** are defined in `src/content.config.ts` with `glob` loaders and Zod schemas: `workshops` (title, image), `team` (name, function, bio, pic), `foundations` (title, description). Markdown lives in `src/content/<collection>/`, images in an `img/` subfolder referenced relatively from frontmatter and validated with `image()`. A `news` collection is still to be added (source items in `resources/news/`, each with `title` and `date`).
- **Pages**: `src/pages/index.astro` (home; section components like `Workshops`, `Foundations`, `Team` are meant to be added here), `news.astro`, `about.md` (uses `layouts/Markdown.astro`).
- **Layouts**: `Base.astro` wraps every page (Header, Footer, global styles, Space Grotesk font, `<title>CCK | {title}</title>`). `Markdown.astro` builds on `Base` with a two-column layout and named slots `top` and `sidebar`, used by detail pages.
- **Section/card pattern**: each collection has a list component (`Workshops.astro`, `Team.astro`, `Foundations.astro`) that should fetch the collection and render one `*Card.astro` per entry.
- **Detail pages**: starter templates (no file extension) are in `resources/<collection>/detailpage`. They are meant to become dynamic routes such as `src/pages/<collection>/[id].astro`, using `getStaticPaths()` with the entry `id` as the route parameter and rendering the Markdown body inside the `Markdown` layout.
- **Placeholders**: unfinished code contains `##SOMETHING##` markers (e.g. in `news.astro`, the components and the detail page templates). These must be replaced with real logic or content, and pages containing them will not compile.
- **Styling**: `src/styles/global.css` defines design tokens as CSS custom properties: colors (`--color-primary` is #B9FF66), fluid type scale `--fs-*`, fluid spacing `--sp-*`, radii `--br-*`, `--max-width-page`. Use these tokens in component-scoped `<style>` blocks instead of hardcoded values. `.container` and `.md` (Markdown prose, `markdown.css`) are shared classes.
- **Hidden code game**: the site hides digits of a 4-digit code (e.g. `news.astro` contains one). `src/components/Code.astro` is the input component for a future `/code` page. It checks each digit with the `pattern` attribute of its four inputs (currently the dummy values 1-4), so the real code goes there. Where each digit is hidden gets documented in `README.md`.
- **Deployment**: planned on GitHub Pages via the Astro GitHub Actions workflow. `astro.config.mjs` is currently empty (no `site`/`base` set yet).
