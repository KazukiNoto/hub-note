# CLAUDE.md

This file provides guidance for AI assistants working in this repository.

## Project Overview

**hub-note** is a static documentation/notes site built with [Zensical](https://zensical.org) and deployed to GitHub Pages. It is an experimental project for publishing personal notes online.

- **Live site**: https://kazukinoto.github.io/hub-note/
- **Stack**: Zensical (Rust-based static site generator, successor to Material for MkDocs) + Python pip
- **Content format**: Markdown (`.md`) files in `docs/`
- **Configuration**: `zensical.toml` (TOML format)

## Repository Structure

```
hub-note/
├── .github/
│   └── workflows/
│       └── docs.yml        # GitHub Actions: build & deploy to GitHub Pages
├── docs/                   # All site content (Markdown source files)
│   ├── index.md            # Home page
│   ├── markdown.md         # Markdown syntax reference
│   └── zensical.md         # Zensical feature documentation/examples
├── dockerfile              # Docker image definition (python:3.12.1)
├── zensical.toml           # Main Zensical site configuration
└── README.md               # Project description (in Japanese)
```

## Development Workflow

1. Edit or add Markdown files under `docs/`
2. Optionally run `zensical serve` locally to preview changes
3. Commit and push to `master` or `main`
4. GitHub Actions automatically builds and deploys to GitHub Pages

## Adding Content

All content lives in `docs/`. To add a new page:

1. Create a new `.md` file under `docs/` (e.g., `docs/new-topic.md`)
2. Zensical auto-discovers it via directory structure (no explicit nav config required unless you want custom ordering)
3. Use a front matter `icon` if desired: `---\nicon: lucide/rocket\n---`

Navigation is currently auto-derived from the directory structure. To define explicit navigation, uncomment and fill in the `nav` array in `zensical.toml`:

```toml
nav = [
  { "Get started" = "index.md" },
  { "Markdown cheat sheet" = "markdown.md" },
]
```

## Configuration (`zensical.toml`)

Key settings in `[project]`:
- `site_name` — displayed in header and browser tab
- `site_description` — HTML meta description
- `site_author` — HTML meta author (currently placeholder)
- `copyright` — footer copyright notice

Key settings in `[project.theme]`:
- `language` — currently `"en"`
- `features` — list of enabled Zensical feature toggles (navigation, code blocks, search, etc.)
- Two `[[project.theme.palette]]` entries provide light (default) / dark (slate) theme toggle

Currently **disabled but available** features in the config (uncomment to enable):
- `navigation.tabs` — top navigation tabs
- `navigation.expand` — auto-expand sidebar sections
- `toc.integrate` — merge TOC into left sidebar
- `header.autohide` — hide header on scroll

## Supported Markdown Features

The site has the following Zensical extensions active (see `docs/zensical.md` for examples):

- **Admonitions** — `!!! note`, `!!! warning`, `??? tip` (collapsible), etc.
- **Code blocks** — syntax highlighting, copy button, line selection, annotations (`# (1)`)
- **Content tabs** — `=== "Tab name"` syntax with linked tab switching
- **Footnotes** — rendered as inline tooltips
- **Mermaid diagrams** — fenced code blocks with ` ```mermaid `
- **MathJax** — LaTeX math via `$...$` and `$$...$$`
- **Icons/emojis** — `:material-...`, `:fontawesome-...`, `:lucide-...`
- **Task lists** — `- [x]` / `- [ ]`
- **Tooltips** — `[text][ref]` with `[ref]: url "tooltip text"`

## Conventions

- **Language**: README and commit messages are in Japanese; content pages can be in any language
- **No tests**: There is no test suite. A successful `zensical build --clean` is the only validation
- **No environment variables**: The project has no `.env` file or runtime secrets; all config is in `zensical.toml`
- **No node_modules / package.json**: Pure Python toolchain — only `pip install zensical` needed
- **Dockerfile** is present but partially commented out; it is not used in CI


## What NOT to Do

- Do not add `node_modules`, `package.json`, or JavaScript build tooling — the stack is Python-only
- Do not commit the generated `site/` directory — it is produced by CI and excluded via `.gitignore`
- Do not push directly to `master`/`main` without confirming CI will pass (`zensical build --clean`)
- Do not add backend code, databases, or server-side logic — this is a purely static site
