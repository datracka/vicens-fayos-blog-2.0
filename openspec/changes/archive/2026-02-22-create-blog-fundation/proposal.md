## Why

A personal blog is needed to publish technical posts authored by Vicens Fayos. Posts already exist as exported markdown files (from DatoCMS) and need a modern, fast, and maintainable publishing platform. Hugo is chosen for its speed, simplicity, and strong static-site ecosystem — deployed to Vercel for zero-config hosting.

## What Changes

- Initialize a new Hugo project as the root of this repository
- Define a clean, lean default theme with support for easy theme-swapping
- Establish a `/posts` content directory where each post lives in its own folder: `posts/<slug>/index.md` + `images/`
- Configure Hugo to parse the existing frontmatter fields (`title`, `slug`, `cover_image`, `date`, `excerpt`) from the exported markdown files
- Wire up `cover_image` to render the post's hero/cover image from the local `images/` subfolder
- Configure Vercel deployment via `vercel.json`

## Capabilities

### New Capabilities

- `hugo-site`: Core Hugo project setup — config, directory structure, build pipeline, and Vercel deployment config
- `post-content`: Content model for blog posts: frontmatter schema, folder structure (`posts/<slug>/index.md` + `images/`), and how Hugo maps these to rendered pages
- `blog-theme`: Default theme — layout templates (list, single post, base), minimal CSS, and the mechanism for swapping themes

### Modified Capabilities

<!-- None — this is a greenfield project -->

## Impact

- **New project root**: Hugo project initialized at `/` of this repo (or a dedicated subfolder TBD in design)
- **Content pipeline**: Existing exported posts (from `datocms-exporter/export/`) can be copied into `posts/` with no or minimal frontmatter changes
- **Build**: `hugo` command generates static output to `public/`
- **Deploy**: Vercel picks up `public/` as the static output on every push
- **Dependencies**: Hugo binary (latest stable), no Node.js required at runtime
