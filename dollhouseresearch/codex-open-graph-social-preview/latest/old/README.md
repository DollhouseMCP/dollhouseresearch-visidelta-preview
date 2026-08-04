# Dollhouse Research Website

Static, markdown-first organization site for DollhouseMCP Inc (DBA Dollhouse Research).

## Stack

- GitHub Pages compatible Jekyll layout
- Markdown content pages
- Custom CSS/JS (no framework dependency)

## Local Preview

If Ruby/Jekyll is available:

```bash
bundle exec jekyll serve
```

If you only need a quick static check:

```bash
python -m http.server 8000
```

Then open `http://localhost:8000`.

### Rendered Diff Viewer (Old vs New)

For content-review passes, you can generate a rendered side-by-side comparison between `origin/main` and your current branch:

```bash
./scripts/build-rendered-diff-viewer.sh origin/main /tmp/dollhouse-rendered-diff build
python3 -m http.server 4310 --directory /tmp/dollhouse-rendered-diff
```

Then open `http://localhost:4310` and click `Compare` for any changed page.

## Key Pages

- `/` Home
- `/projects/` Project index
- `/news-press/` Verified announcements and external coverage
- `/press-kit/` Boilerplate, brand assets, and media references
- `/blog/` Primary writing and publication index
- `/research/` Proposal papers and architecture research index
- `/about/` Company and organization context
- `/writing/` Legacy writing path that forwards to blog content

## Content Operations

- News/press workflow: `docs/news-press-workflow.md`
- Issue intake template: `.github/ISSUE_TEMPLATE/news_press_entry.yml`
- Screenshot helper: `scripts/capture-news-screenshot.sh`

## Quality Checks

- Workflow: `.github/workflows/website-quality.yml`
- Markdown lint config: `.markdownlint-cli2.yaml`
- Spelling config: `.cspell.json`
- Link check config: `.lychee.toml`

## Licensing

- Repository license: AGPL-3.0 (`LICENSE`)
- Licensing notes: `LICENSING.md`
