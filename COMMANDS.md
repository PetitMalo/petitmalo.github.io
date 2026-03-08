# Project Commands — petitmalo.github.io

Astro static site (using the [Astro Cactus](https://github.com/chrismwilliams/astro-theme-cactus) theme).

## First time setup

The project uses `pnpm` but it can be activated via `corepack` (already installed):

```bash
corepack enable   # one-time, activates pnpm
pnpm install      # install dependencies
```

Or with plain `npm`:

```bash
npm install
```

## Daily use

| Command | What it does |
|---|---|
| `pnpm dev` / `npm run dev` | Start local dev server at `http://localhost:4321` (hot reload) |
| `pnpm build` / `npm run build` | Build the site into `dist/` (also runs pagefind indexing) |
| `pnpm preview` / `npm run preview` | Serve the built `dist/` locally to check the final output |

## Code quality

| Command | What it does |
|---|---|
| `pnpm check` / `npm run check` | Type-check Astro files + lint with Biome |
| `pnpm lint` / `npm run lint` | Auto-fix linting issues (Biome) |
| `pnpm format` / `npm run format` | Format all files with Prettier |

## Content

Posts and notes are Markdown (`.md`) or MDX (`.mdx`) files inside `src/content/`.
Each file needs a frontmatter block at the top, e.g.:

```md
---
title: "My post title"
publishDate: 2026-03-08
description: "Short description"
tags: ["tag1", "tag2"]
---

Content goes here...
```

## Deployment

The site is hosted on GitHub Pages. Pushing to the relevant branch triggers the
deploy automatically via GitHub Actions — no manual step needed.
