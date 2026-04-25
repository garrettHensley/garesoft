# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

`garesoft.dev` — a static Astro 5 site styled like a 90s/Win95 webpage. It's primarily a devlog for the indie game *This is My Temple*. Deployed to GitHub Pages on every push to `main` via `.github/workflows/deploy.yml` (uses `withastro/action@v3`); the `CNAME` file at the root pins the custom domain.

## Commands

Use **bun** (a `bun.lock` is checked in).

| Command | Action |
| :-- | :-- |
| `bun install` | Install dependencies |
| `bun dev` | Local dev server on `localhost:4321` |
| `bun build` | Production build to `./dist/` |
| `bun preview` | Preview the production build |
| `bun astro check` | Astro + TypeScript diagnostics |

There is no test suite or linter configured — `astro check` is the closest thing to a verification step.

## Architecture

Astro content-collection driven, with one collection (`blog`) and a single dynamic route that renders each post.

- **Content collection (`src/content.config.ts`)**: a `blog` collection loaded via `glob({ pattern: "**/*.md", base: "./src/blog" })`. There is **no zod schema declared** — frontmatter shape is enforced only by convention (see "Adding a blog post" below). If you add a schema, update existing posts to match.
- **Posts (`src/blog/postN.md`)**: plain markdown files. The collection `id` derives from the filename (e.g. `post5.md` → `/blog/post5/`).
- **Dynamic route (`src/pages/blog/[id].astro`)**: `getStaticPaths` enumerates every post and `render(post)` produces `<Content />`. This page also sets the per-post `<head>` (title, description, og:image).
- **Index (`src/pages/index.astro`)**: pulls the collection, sorts by `data.date` descending, slices the latest 5, renders each through `PreviewImage`.
- **Blog index (`src/pages/blog/index.astro`)**: same pattern but slices 3.
- **Layout (`src/layouts/Layout.astro`)**: shared shell — header link to `/`, cobblestone background, retro border styling, CSS variables (`--primary`, `--accent`, etc.) in `:root`. All pages wrap content in `<MySiteLayout>`.
- **Assets**: two distinct conventions, do not mix them up:
  - `public/images/...` — referenced in markdown/HTML as `/images/foo.png`. Use this for blog post `image:` frontmatter and anything referenced as a plain string URL.
  - `src/assets/images/...` — imported in `.astro` files and passed to Astro's `<Image />` component for optimization.

## Adding a blog post (the common task)

1. Create `src/blog/postN.md` (next sequential number; the filename becomes the URL slug).
2. Frontmatter must include — every existing post except `post1.md` follows this:
   ```yaml
   ---
   title: "..."
   description: "..."
   date: "YYYY-MM-DD"
   image: "/images/whatever.png"   # path under public/, used by index preview + og:image
   ---
   ```
   `post1.md` predates the `image` convention and is the reason the index/preview tolerate a missing image — keep new posts consistent by always including one.
3. Drop the preview image into `public/images/` (or `public/images/gifs/`, `public/images/title/` — match what's already there).
4. No registration step; the glob loader picks it up. `bun dev` to verify the post appears on `/`, `/blog`, and `/blog/postN/`.

## Conventions worth knowing

- The site's voice is irreverent/retro — `<marquee>`, `<blockquote class="tiktok-embed">`, ALL CAPS terminal flavor text in the index. Don't "modernize" these without being asked.
- Inline `<style>` blocks per-page are the norm; there is no global stylesheet beyond `Layout.astro`'s `<style>`. Use CSS variables from `:root` rather than reintroducing colors.
- `tsconfig.json` extends `astro/tsconfigs/strict`. TS errors will surface via `astro check` / the dev server, not a separate `tsc` step.
