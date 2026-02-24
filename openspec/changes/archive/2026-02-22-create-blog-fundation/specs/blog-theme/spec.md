## ADDED Requirements

### Requirement: Default theme lives under themes/lean/
The site SHALL ship with a default theme named `lean` located at `themes/lean/`. Hugo's `config.toml` SHALL reference it via `theme = "lean"`. The theme SHALL contain all layout templates and CSS required to render the site without any root-level `layouts/` overrides.

#### Scenario: Site renders with lean theme active
- **WHEN** `config.toml` has `theme = "lean"` and the `themes/lean/` directory exists
- **THEN** Hugo builds the site using the lean theme templates with no missing layout errors

### Requirement: Theme is swappable via a single config change
Changing the active theme SHALL require only updating the `theme` key in `config.toml` and providing a new theme directory under `themes/`. Content files and root-level config SHALL not require modification.

#### Scenario: Second theme activates cleanly
- **WHEN** a second theme directory is placed under `themes/<other-name>/` and `config.toml` is updated to `theme = "<other-name>"`
- **THEN** Hugo builds the site using the new theme without errors

### Requirement: Root layouts/ directory acts as theme override
The project SHALL support a root-level `layouts/` directory. Files placed there SHALL take precedence over the active theme's templates, enabling targeted customization without forking the theme.

#### Scenario: Root layout overrides theme template
- **WHEN** a file at `layouts/posts/single.html` exists and the active theme also has `themes/lean/layouts/posts/single.html`
- **THEN** Hugo uses the root-level file to render single post pages

### Requirement: Lean theme provides base template
The `lean` theme SHALL include a base HTML template (`baseof.html`) that defines the full HTML document structure: `<html>`, `<head>` (with title, meta charset, viewport, CSS link), and `<body>` with a main content block.

#### Scenario: All pages share the base layout
- **WHEN** Hugo renders any page (list or single)
- **THEN** the output is a valid HTML document with `<html>`, `<head>`, and `<body>` tags

### Requirement: Lean theme provides post list layout
The `lean` theme SHALL include a list layout that renders all posts under `content/posts/` as a linked list, showing each post's title, date, and excerpt (if present).

#### Scenario: List page renders all posts
- **WHEN** the blog index or `/posts/` list page is rendered
- **THEN** each post appears as a linked item with title and date visible

#### Scenario: Excerpt shown when available
- **WHEN** a post has an `excerpt` frontmatter field
- **THEN** the list item includes the excerpt text below the title

### Requirement: Lean theme provides single post layout
The `lean` theme SHALL include a single post layout that renders the post title, date, cover image (when present), and the full markdown content.

#### Scenario: Post page renders all content
- **WHEN** a single post page is rendered
- **THEN** the page shows the title, formatted date, and the full rendered markdown body

#### Scenario: Cover image shown when present
- **WHEN** the post has a valid `cover_image` resource
- **THEN** the cover image is rendered above the post body as an `<img>` element

### Requirement: Lean theme CSS is minimal and readable
The theme's CSS SHALL prioritize readability: a constrained content width, comfortable line height, legible font stack, and no decorative framework dependencies. It SHALL be a single plain CSS file with no build step required.

#### Scenario: Site is readable on desktop
- **WHEN** a post page is viewed in a desktop browser
- **THEN** body text is constrained to a readable line length (max ~70ch) and uses a legible font stack

#### Scenario: Site is readable on mobile
- **WHEN** a post page is viewed on a mobile viewport
- **THEN** text reflows appropriately and requires no horizontal scrolling
