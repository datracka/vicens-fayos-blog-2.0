## 1. Hugo Project Scaffold

- [x] 1.1 Install Hugo latest stable version locally (via `brew install hugo` or direct download)
- [x] 1.2 Run `hugo new site . --force` at the repository root to generate Hugo scaffolding
- [x] 1.3 Create `.gitignore` with `public/` and `resources/_gen/` entries
- [x] 1.4 Set base site config in `config.toml`: `baseURL`, `languageCode`, `title`, `theme = "lean"`

## 2. Vercel Deployment Config

- [x] 2.1 Create `vercel.json` with `buildCommand: "hugo --minify"`, `outputDirectory: "public"`, and `installCommand: ""`
- [x] 2.2 Add `HUGO_VERSION` environment variable to `vercel.json` matching the locally installed version

## 3. Default Theme (lean)

- [x] 3.1 Create `themes/lean/` directory with `theme.toml` (name, description, min Hugo version)
- [x] 3.2 Create `themes/lean/layouts/_default/baseof.html` with full HTML document structure (`<html>`, `<head>`, `<body>`, block definitions)
- [x] 3.3 Create `themes/lean/layouts/index.html` (or `list.html`) that extends baseof and renders all posts ordered by date
- [x] 3.4 Create `themes/lean/layouts/posts/single.html` that extends baseof and renders title, date, cover image, and markdown body
- [x] 3.5 Create `themes/lean/static/css/style.css` with minimal readable styles: constrained content width (`max-width: ~70ch`), comfortable line height, system font stack, basic link and heading styles
- [x] 3.6 Link `style.css` in `baseof.html` head

## 4. Post Content Model

- [x] 4.1 Create `content/posts/` directory
- [x] 4.2 Add a single test post (`content/posts/test-post/index.md` + `images/`) with all frontmatter fields to validate the setup
- [x] 4.3 Implement `cover_image` rendering in `single.html` using `.Resources.GetMatch .Params.cover_image` with a nil-check guard
- [x] 4.4 Implement `excerpt` display in the list layout (show below title when `.Params.excerpt` is present)

## 5. Validation

- [x] 5.1 Run `hugo server` and verify the test post renders at its slug URL with cover image and content
- [x] 5.2 Run `hugo --minify` and verify `public/` is generated with no errors
- [x] 5.3 Verify the list page shows the test post with title, date, and excerpt
- [x] 5.4 Verify a post without `cover_image` renders without broken `<img>` markup
- [x] 5.5 Verify mobile layout renders without horizontal scroll (browser devtools responsive mode)

## 6. Content Migration (existing posts)

- [x] 6.1 Copy all exported posts from `datocms-exporter/export/` into `content/posts/` (each folder maps directly)
- [x] 6.2 Run `hugo server` and spot-check that existing posts render correctly (title, date, cover image, body)
- [x] 6.3 Fix any frontmatter incompatibilities found during spot-check (e.g. date format, path issues)
