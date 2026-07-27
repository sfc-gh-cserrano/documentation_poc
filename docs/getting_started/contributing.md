# Contributing to Cerebro

This guide explains how to add, edit, and publish knowledge articles in Cerebro.

## Prerequisites

- Git access to this repository
- A text editor that supports markdown (VS Code, etc.)

## Local Development

To preview the site locally:

```bash
pip install -r requirements.txt
mkdocs serve
```

The site will be available at `http://127.0.0.1:8000`.

## Adding Content

### Create a New Article

1. Create a markdown file under `docs/`:
   - For a new topic area, create a subdirectory: `docs/my-topic/index.md`
   - For a page within an existing topic: `docs/existing-topic/my-page.md`

2. Add a YAML front matter header (optional):
   ```markdown
   ---
   title: My Article Title
   ---
   ```

3. Write your content using standard markdown.

### Add Images

1. Place image files in `docs/assets/`
2. Reference them with relative paths in your markdown:
   ```markdown
   ![Alt text](../assets/my-image.png)
   ```

### Update Navigation

If you want explicit control over page ordering, edit the `nav` section in `mkdocs.yml`:

```yaml
nav:
  - Home: index.md
  - Getting Started: getting-started/index.md
  - My New Section: my-topic/index.md
```

If omitted from `nav`, pages are still accessible via search and direct URL but won't appear in the sidebar.

## Workflow

### 1. Create a Branch

```bash
git checkout -b docs/my-new-article
```

### 2. Write Your Content

Add or edit files under `docs/`. Use `mkdocs serve` locally to preview.

### 3. Open a Pull Request

Push your branch and open a PR against `main`.

### 4. Review the Preview

Once the PR is opened, a GitHub Action automatically builds and deploys a preview. Look for the bot comment on your PR with a link like:

```
https://<org>.github.io/<repo>/preview/pr-<number>/
```

Use this to verify formatting, images, and navigation before merging.

### 5. Merge

Once approved, merge the PR. The deploy workflow will automatically:
- Build the site
- Publish to GitHub Pages
- Update the search index
- Clean up the preview deployment

## File Organization

```
docs/
├── index.md              # Site homepage
├── assets/               # Images and static files
├── topic-a/
│   ├── index.md          # Topic landing page
│   └── subtopic.md       # Detailed sub-page
└── topic-b/
    └── index.md
```

## Markdown Features

Cerebro supports these markdown extensions:

| Feature | Syntax |
|---------|--------|
| Admonitions | `!!! note "Title"` |
| Code highlighting | Fenced blocks with language tag |
| Table of contents | Auto-generated from headings |
| Permalink anchors | Auto-added to all headings |

## Search

The site includes full-text client-side search powered by Lunr.js. The search index is rebuilt automatically on every deployment. No configuration is needed — all published pages are indexed.

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Preview not appearing | Check the Actions tab for build errors |
| Images not loading | Verify relative path from the markdown file to `assets/` |
| Page not in navigation | Add it to the `nav` section in `mkdocs.yml` |
| Build fails with `--strict` | Fix any broken links or missing references |
