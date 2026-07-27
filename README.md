# Cerebro - GRE Knowledge Management

A repository-based system for knowledge hosting through markdown documents, automatically published as an HTML site via GitHub Pages.

## Overview

Cerebro provides a lightweight, Git-driven workflow for creating, reviewing, and publishing internal knowledge articles. Authors write in markdown, reviewers verify via preview deployments, and merged content is automatically published.

## Features

- **Markdown authoring** — Write docs in standard markdown with extensions (admonitions, code highlighting, mermaid diagrams)
- **Snowflake-branded theme** — Custom MkDocs Material theme with Snowflake brand colors
- **Full-text search** — Client-side Lunr.js search, rebuilt on every deploy
- **PR preview deployments** — Automatically generated preview URLs for every pull request
- **Auto-publish on merge** — Push to `main` triggers a build and deploy to GitHub Pages

## Quick Start

```bash
# Install uv (if needed)
curl -LsSf https://astral.sh/uv/install.sh | sh

# Install dependencies
uv sync

# Serve locally
uv run mkdocs serve
```

Site available at `http://127.0.0.1:8000`

## Workflow

```mermaid
flowchart LR

    A[Write markdown] -->|push branch| B[Open PR]

    B -->|auto-deploy| C[Preview site]

    C -->|approve & merge| D[Publish to GitHub Pages]
```

1. Create or edit `.md` files under `docs/`
2. Open a Pull Request
3. Review the auto-generated preview deployment
4. Merge to `main` — site publishes automatically

## Documentation

- [Deployment Guide](DEPLOYMENT.md) — End-to-end setup and pipeline configuration
- [Contributing](docs/getting_started/contributing.md) — How to add and organize content

## Tech Stack

| Component | Tool |
|-----------|------|
| Site generator | MkDocs + Material theme |
| Package manager | uv |
| CI/CD | GitHub Actions |
| Hosting | GitHub Pages |
| Search | Lunr.js (built-in) |
| Diagrams | Mermaid |
