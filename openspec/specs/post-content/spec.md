## ADDED Requirements

### Requirement: Posts stored as Hugo leaf bundles
Each blog post SHALL live in its own directory under `content/posts/<slug>/` containing an `index.md` file and an `images/` subdirectory. This structure is known as a Hugo leaf bundle.

#### Scenario: Post directory structure is valid
- **WHEN** a post with slug `my-post` exists
- **THEN** the file system contains `content/posts/my-post/index.md` and optionally `content/posts/my-post/images/`

#### Scenario: Hugo recognizes the post as a page
- **WHEN** Hugo builds the site
- **THEN** each `content/posts/<slug>/index.md` is rendered as a page at URL `/<slug>/` (using the `slug` frontmatter field) or `/posts/<slug>/` (using directory path)

### Requirement: Post frontmatter schema
Each post's `index.md` SHALL include frontmatter with the following fields. Hugo SHALL parse them without requiring any migration or transformation of existing exported files.

| Field | Type | Required | Description |
|---|---|---|---|
| `title` | string | yes | Display title of the post |
| `slug` | string | yes | URL-safe identifier used as the public URL path |
| `date` | string (ISO 8601) | yes | Publication date |
| `cover_image` | string | no | Relative path to the cover image (e.g. `images/foo.webp`) |
| `excerpt` | string | no | Short summary shown in list views |
| `status` | string | no | Publication status (ignored by Hugo rendering, preserved as metadata) |

#### Scenario: Post renders with all required fields
- **WHEN** a post has `title`, `slug`, and `date` in frontmatter
- **THEN** Hugo renders the post page with the correct title and accessible at the correct URL

#### Scenario: Optional fields absent do not cause errors
- **WHEN** `cover_image` or `excerpt` are absent from frontmatter
- **THEN** Hugo renders the post without errors and without broken image markup

### Requirement: Cover image resolved from page bundle resources
When `cover_image` is present, the theme template SHALL resolve it as a Hugo page resource relative to the post's bundle directory using `.Resources.GetMatch`.

#### Scenario: Cover image renders on post page
- **WHEN** a post has `cover_image: images/photo.webp` and the file exists at `content/posts/<slug>/images/photo.webp`
- **THEN** the rendered post page includes an `<img>` element pointing to the correctly processed image

#### Scenario: Missing cover image does not produce broken markup
- **WHEN** `cover_image` is set in frontmatter but the referenced file does not exist in `images/`
- **THEN** the image element is omitted from the rendered HTML (nil-check in template)

### Requirement: Posts listed on the blog index
The blog SHALL have a list page (at `/posts/` or `/`) that shows all published posts ordered by date descending.

#### Scenario: All posts appear in list
- **WHEN** multiple posts exist under `content/posts/`
- **THEN** the list page renders a link for each post showing at minimum the title and date

#### Scenario: List is ordered by date
- **WHEN** posts have different `date` values
- **THEN** the list page shows them in descending chronological order (newest first)
