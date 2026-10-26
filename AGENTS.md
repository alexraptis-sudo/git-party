# AGENTS.md

## Project

- Website for Creative Coding Kortrijk (CCK), a creative coding community in Kortrijk, Belgium.
- Audience: artists, designers, programmers and people curious about creative coding, at any skill level.
- Content: workshops, foundations (the club's values), the team, and news. The about page and the content are placeholder text.
- Built by a three-person team (Alexandros Raptis, Riccardo Rossi, Bianca Serbanescu) as a Git/GitHub Flow exercise. Each person works on their own `feature/*` branch and merges through pull requests on GitHub.
- Design: Figma file linked in `readme.md` (based on the Positivus template).

## Stack & constraints

- Astro 7 static site, npm (`package-lock.json`). `npm run dev` (with `--host`), `npm run build`, `npm run preview`.
- No test, lint or format tooling.
- Content lives in Markdown content collections defined in `src/content.config.ts`, loaded with `glob` from `src/content/<collection>/`:
  - `workshops`: `title`, `image`
  - `team`: `name`, `function`, `bio`, `pic`
  - `foundations`: `title`, `description`
  - Images are referenced relative to the Markdown file (`img/` subfolders) and validated with `image()`.
- Pages in `src/pages/`; layouts `Base.astro` and `Markdown.astro` in `src/layouts/`; one `.astro` component per section in `src/components/`.
- Plain CSS only, no CSS framework: `src/styles/reset.css`, `global.css`, `markdown.css`, plus scoped `<style>` blocks in components. Spacing and font sizes use CSS custom properties (`--sp-*`, `--fs-*`).
- Font: `@fontsource-variable/space-grotesk`.
- Templates for detail pages are in `resources/<collection>/detailpage` (no file extension).
- Unfinished files contain `##...##` placeholder markers, and the build fails until these are replaced.
- Deployment target: GitHub Pages with Astro's GitHub Actions workflow. `astro.config.mjs` has no `site`/`base` yet.
