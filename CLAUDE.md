# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

@AGENTS.md

The exercise brief and the remaining challenges are in `readme 2.md` (the filename has a space).

## Team rules

- Never merge pull requests or merge into `main`. Humans merge on GitHub.
- When resolving merge conflicts, never drop a teammate's work. Keep both sides' lines, and ask before removing anything someone else wrote.
- Ask before `git push` or opening a pull request.
- Branches: `feature/<topic>` off `main` (e.g. `feature/workshops`, `feature/agents-<name>`).

## Gotchas

- `npm run build` fails while any `##...##` placeholder remains in a page or a component it imports (`src/pages/news.astro` has some until Challenge 5), and when a content file is missing a schema field from `src/content.config.ts`. Run the build to verify changes; there are no tests.
- Dependencies aren't installed in a fresh clone. Run `npm install` first.
- Adding a collection (e.g. `news`) means adding it to `collections` in `src/content.config.ts`.
