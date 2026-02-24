## Context

Vicens Fayos has a collection of technical blog posts exported from DatoCMS as markdown files. Each post lives in its own folder (`<slug>/index.md` + `images/`), with frontmatter fields like `title`, `slug`, `date`, `excerpt`, and `cover_image`. The goal is to build a minimal, fast personal blog that can render these posts with no CMS dependency, hosted on Vercel.

Hugo is chosen as the SSG: it's a single binary with no Node runtime, extremely fast builds, and has first-class support for the page bundle structure (folder-per-post with `index.md`) already used by the exports.

## Goals / Non-Goals

**Goals:**
- Hugo project initialized and buildable with a single `hugo` command
- Posts rendered from `/content/posts/<slug>/index.md` using Hugo page bundles
- `cover_image` frontmatter field resolved to the local `images/` subfolder of each post bundle
- Clean default theme with minimal CSS — readable, no clutter
- Theme-swappable: the theme lives under `themes/` and can be replaced or extended without touching content
- Vercel deployment via `vercel.json` pointing at Hugo's `public/` output

**Non-Goals:**
- Search, comments, tags/categories (can be added later)
- RSS (Hugo generates this automatically — no explicit work needed)
- CMS re-integration or API-driven content
- Internationalization at launch
- Custom domain setup (Vercel config only, DNS is out of scope)

## Decisions

### 1. Project root layout

Hugo is initialized at the repository root (not a subfolder). This keeps the repo focused — the blog IS the project.

```
/
├── config.toml          # Hugo site config
├── content/
│   └── posts/
│       └── <slug>/
│           ├── index.md
│           └── images/
├── themes/
│   └── lean/            # Default theme
├── layouts/             # Override point for theme customization
├── static/
├── public/              # Hugo output (gitignored)
└── vercel.json
```

**Alternative considered**: Hugo in a `/blog` subfolder. Rejected — adds indirection and complicates Vercel config without benefit.

### 2. Page bundles over flat files

Each post is a Hugo **leaf bundle** (`content/posts/<slug>/index.md`). This keeps each post's assets (images) co-located and lets Hugo resolve `cover_image: images/foo.webp` as a page resource via `.Page.Resources.GetMatch`.

**Alternative considered**: Flat `content/posts/<slug>.md` with images in `static/`. Rejected — breaks co-location and requires manual path management across posts.

### 3. Theme as a standalone directory under `themes/`

The default theme (`themes/lean/`) contains all layout templates and CSS. Hugo's `theme` config key points to it. Swapping themes means changing one line in `config.toml` and dropping a new folder under `themes/` — content and layouts are untouched.

A `layouts/` directory at the root acts as the override layer: any file there takes precedence over the active theme, allowing targeted customization without forking the theme.

**Alternative considered**: Embed layouts directly at root without a `themes/` directory. Rejected — makes theme-swapping harder and conflates the site structure with theme concerns.

### 4. Frontmatter mapping

The exported frontmatter includes fields Hugo doesn't natively know (`id`, `status`, `author_id`, `category_id`, `cover_image`, `excerpt`). Hugo treats unknown fields as custom params, accessible via `.Params.<field>`. No frontmatter migration is needed — the files work as-is.

The `cover_image` value (e.g., `images/foo.webp`) is resolved in the theme template using:
```go
{{ $img := .Resources.GetMatch .Params.cover_image }}
```

### 5. Vercel deployment

Hugo's build command (`hugo --minify`) and output directory (`public`) are declared in `vercel.json`. Vercel's zero-config detection handles Hugo natively, but an explicit config avoids ambiguity.

```json
{
  "buildCommand": "hugo --minify",
  "outputDirectory": "public",
  "installCommand": ""
}
```

Hugo binary availability on Vercel: Vercel's build environment includes Hugo. No custom install step needed.

## Risks / Trade-offs

- **Hugo version drift** → Pin the Hugo version in `vercel.json` via the `HUGO_VERSION` env var to avoid unexpected build differences between local and CI.
- **`cover_image` path mismatches** → If an exported post's `cover_image` points to a file that doesn't exist in `images/`, the template will silently render no image. A nil-check in the template (`{{ if $img }}`) prevents broken markup.
- **Theme lock-in feels fake without a real second theme** → The swap mechanism is real (Hugo's `theme` config), but it's only validated when a second theme is actually installed. This is acceptable at foundation stage.

## Migration Plan

1. Run `hugo new site . --force` at repo root to scaffold the Hugo project
2. Copy existing exported posts from `datocms-exporter/export/` into `content/posts/`
3. Create `themes/lean/` with base template, single post layout, list layout, and minimal CSS
4. Verify `hugo server` renders all posts locally
5. Add `vercel.json` and push — Vercel auto-deploys on the connected branch

Rollback: Hugo generates nothing in-place; `public/` is gitignored. Reverting means deleting Hugo config files — no data loss risk.

## Open Questions

- Should `excerpt` render as a subtitle on the post page, or only in list views?
- Should the list page be paginated at launch, or a flat list (fine for small post counts)?
- Author info (name, bio, social links) — hardcoded in theme config or a data file?
