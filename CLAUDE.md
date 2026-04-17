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

## Document Organization

When **docs直下** (root of docs, excluding subdirectories) accumulates **5 or more files** (excluding `index.md`), automatically organize and move older articles to category folders:

- **`docs/AI/`** — AI-related articles (AI tools, concepts, techniques)
- **`docs/TOOL/`** — Tool-related articles (software, frameworks, utilities)

### Guidelines:
1. Review each article's content to determine appropriate category
2. Create new category folders as needed based on content
3. Maintain chronological order when moving (move oldest articles first)
4. Update navigation if necessary

**Current organization status**: docs直下 = index.md のみ

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
- **Chat Language**: すべてのチャットのやり取りは日本語で行うこと
- **No tests**: There is no test suite. A successful `zensical build --clean` is the only validation
- **No environment variables**: The project has no `.env` file or runtime secrets; all config is in `zensical.toml`
- **No node_modules / package.json**: Pure Python toolchain — only `pip install zensical` needed
- **Dockerfile** is present but partially commented out; it is not used in CI


## URL Summarization Workflow

When a user provides a URL, follow these steps:

1. **Fetch** the URL content using the `WebFetch` tool
2. **Summarize** the content in clear, readable Japanese (or the same language as the user's request), covering:
   - Title / overview of the page
   - Key points and main topics
   - Notable details, data, or conclusions
3. **Save** the summary as a new Markdown file under `docs/` with:
   - A descriptive, lowercase, hyphenated filename (e.g., `docs/summary-topic-name.md`)
   - Front matter with an appropriate icon (e.g., `icon: lucide/link`)
   - A `# Title` heading
   - A **Source** line linking back to the original URL
   - The structured summary using headings, bullet points, and admonitions as appropriate
4. **Commit and push** the new file to the current development branch

### Example file structure

```markdown
---
icon: lucide/link
---

# ページタイトルの要約

**Source**: <https://example.com/article>

## 概要

...

## 主なポイント

- ...
- ...

## まとめ

...
```

## Pull Request Guidelines

- **No reviewers**: When creating a pull request, do NOT assign any reviewers (`--reviewer` flag must not be used)
- **No PRs**: Do NOT create pull requests. Push directly to the current branch.
- **No new branches**: Do NOT create new branches. Always push to the already-checked-out branch.

## What NOT to Do

- Do not add `node_modules`, `package.json`, or JavaScript build tooling — the stack is Python-only
- Do not commit the generated `site/` directory — it is produced by CI and excluded via `.gitignore`
- Do not push directly to `master`/`main` without confirming CI will pass (`zensical build --clean`)
- Do not add backend code, databases, or server-side logic — this is a purely static site
