# Repo guide

Personal portfolio/blog at <https://samuelsalam815.github.io/>. Mid-migration from a hand-written static site to Astro, so that adding posts and projects is easy. The migration is on branch `astro-migration`; `main` is the default branch.

## Layout

- `docs/` — the **live** site: plain `index.html`, `styles.css`, and `assets/`. Deployed as-is. Treat as legacy until the Astro site replaces it.
- `astro/` — the new site (Astro 7, Node >= 22.23.4). Run all npm/astro commands from this directory.
  - `src/pages/` — routes. `index.astro` currently renders only `About`.
  - `src/layouts/Layout.astro` — shared HTML shell (title `Dev-S815`).
  - `src/components/About.astro` — ported about section. `Welcome.astro` is unused starter-template code; remove it once confirmed.
  - `src/posts/` — Markdown posts (frontmatter: `title`, `pubDate`, `description`, `author`, `image`, `tags`). Not yet wired to a content collection or route.
  - `src/assets/` — images imported by components and referenced from posts (relative paths like `../assets/x.gif`).
  - `public/` — static files served from the site root (favicons).
  - `astro/AGENTS.md` — Astro-generated dev-server and docs notes; follow it for `astro dev`.
- `.github/workflows/static.yml` — deploys `./docs` to GitHub Pages on push to `gh-pages`. It does **not** build Astro yet.
- `todo.md` — checklist of site tasks.

## Commands (run in `astro/`)

- `npm install`
- `astro dev --background` (see `astro/AGENTS.md`)
- `npm run build` — output goes to `astro/dist`
- `npm run preview`

## Migration state and open items

- Port remaining pieces from `docs/index.html` and `docs/styles.css` (page styling after the NieR: Automata UI, the Waukegan font in `docs/assets/WaukeganLdo-ax19.ttf`, background image).
- Posts need a content collection and a post route/listing so new posts appear without editing code.
- Post frontmatter `image` is still the Astro template placeholder; replace it.
- Deployment must change to build `astro/` (set `outDir` or upload `astro/dist`, and add `site`/`base` in `astro.config.mjs`) before `docs/` is retired. Do not change the workflow until the user asks.

## Conventions

- Keep the visual style consistent with the existing site (muted `#4E4B42` palette, NieR-inspired).
- Scope component styles in the component's `<style>` block.
- Do not edit `docs/` for migration work except to remove it at cutover; the live site depends on it.
- Pushing to `gh-pages` publishes the site. Never push there without explicit approval.
