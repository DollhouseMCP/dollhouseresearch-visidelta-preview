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

## Blog Hub Publishing Rule

The blog at `/blog/` is the writing hub for every project in the portfolio. It is generated from two data files:

- `_data/blog_hub.yml` — one entry per post, portfolio wide. Posts on this site use a site-relative `url`; posts on project sites (dollhousemcp.com, etc.) use an absolute URL. **File order is the display order** (newest first, insert at top) for both `/blog/` and `/feed.xml` — dates alone cannot order same-day posts.
- `_data/blog_projects.yml` — one entry per project. Each project card's latest post is computed from `blog_hub.yml` at build time, so cards cannot go stale.

**The rule: any new post published on any project site must add one entry to `_data/blog_hub.yml` in the same working session.** Posts native to this site go in `_posts/` with `date`, `project`, and `permalink` front matter, plus a `blog_hub.yml` entry pointing at the local path.

The site feed at `/feed.xml` is hand-generated from `blog_hub.yml` (see `feed.xml`), so it includes spoke-site posts too — jekyll-feed is deliberately NOT used, since it would only see local posts. Feed sync automation is tracked in issue #39; until it lands, this manual rule is the only thing keeping the hub current.
