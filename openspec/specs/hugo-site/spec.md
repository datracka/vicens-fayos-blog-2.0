## ADDED Requirements

### Requirement: Hugo project initialized at repository root
The site SHALL be a valid Hugo project scaffolded at the repository root, with `config.toml`, `content/`, `themes/`, `layouts/`, `static/`, and `public/` directories following Hugo conventions.

#### Scenario: Project builds successfully
- **WHEN** `hugo --minify` is run from the repository root
- **THEN** Hugo produces a static site in `public/` with no errors

#### Scenario: Local development server starts
- **WHEN** `hugo server` is run from the repository root
- **THEN** Hugo starts a local dev server and serves the site at `localhost:1313`

### Requirement: Hugo version is pinned
The project SHALL declare an explicit Hugo version to ensure consistent builds across local and CI environments.

#### Scenario: Version declared in Vercel config
- **WHEN** Vercel runs the build
- **THEN** it uses the Hugo version declared in `vercel.json` via the `HUGO_VERSION` environment variable

### Requirement: Vercel deployment configured
The project SHALL include a `vercel.json` file that declares the Hugo build command and output directory so Vercel can deploy the site without manual configuration.

#### Scenario: Vercel detects and builds the site
- **WHEN** a push is made to the connected Vercel branch
- **THEN** Vercel runs `hugo --minify` and serves the contents of `public/`

#### Scenario: No install step required
- **WHEN** Vercel runs the build
- **THEN** no `npm install` or package manager step is executed (Hugo is a self-contained binary)

### Requirement: Public output directory is gitignored
The `public/` directory SHALL be listed in `.gitignore` so generated files are never committed.

#### Scenario: Public directory absent from repository
- **WHEN** `git status` is run after a `hugo build`
- **THEN** files under `public/` do not appear as untracked or staged
