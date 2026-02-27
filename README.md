# Vicens Fayos Blog

Personal blog built with [Hugo](https://gohugo.io/).

## Requirements

- [Hugo](https://gohugo.io/installation/) v0.156.0+

## Setup

```bash
git clone <repo-url>
cd vicens-fayos-blog-2.0
```

## Run locally

```bash
hugo server
```

The site will be available at `http://localhost:1313`.

## Build

```bash
hugo --minify
```

Output is generated in the `public/` directory.

## Deploy to Vercel

1. Push the repo to GitHub.
2. Import the project in [Vercel](https://vercel.com/).
3. Vercel auto-detects the config from `vercel.json` — no additional setup needed.
4. Deploy.

The `vercel.json` already sets the build command (`hugo --minify`), output directory (`public`), and Hugo version (`0.156.0`).
