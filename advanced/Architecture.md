[中文](./Architecture.zh.md) | **English**

# Architecture

This document describes Gleaner's internal architecture, including its data flow, tech stack, data model, sync engine, and Markdown rendering pipeline.

## Overview

```
Browser
  ├── React UI ←→ Zustand Stores ←→ IndexedDB (Dexie.js)
  │
  └── Sync Engine ──→ GitHub REST API
                       (optionally via Proxy)
```

Gleaner runs entirely in the browser as a single-page application. There is no backend server. All data is fetched from GitHub's REST API and cached locally in IndexedDB.

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Framework | Vite + React 19 + TypeScript |
| State management | Zustand |
| Local database | IndexedDB via Dexie.js |
| Styling | Tailwind CSS 4 + shadcn/ui conventions |
| Markdown rendering | unified (remark + rehype pipeline) |
| Graph visualization | react-force-graph-2d |
| Package manager | pnpm |
| E2E testing | Playwright |

## Data Model

Gleaner uses four main IndexedDB tables:

| Table | Description |
|-------|-------------|
| **repos** | Repository metadata: owner, repo name, branch, commit SHA, sync status |
| **files** | File content and metadata: path, content, title (first heading), tree SHA |
| **links** | Parsed link index: source file, target file, link type (wikilink/standard), resolved status |
| **profiles** | Profile configurations: name, type (local/GitHub), repo list, settings |

## Sync Flow

The sync engine performs these steps for each repository:

1. **Get tree** — Call GitHub Trees API (`GET /repos/{owner}/{repo}/git/trees/{branch}?recursive=1`) to get the complete file listing
2. **Compare tree SHA** — If the tree SHA matches the cached value, this repo is unchanged and can be skipped entirely
3. **Filter `.md` files** — Keep only Markdown files, applying `includePaths` and `excludePaths` filters
4. **Compare file SHAs** — For each `.md` file, compare its blob SHA against the cached version to identify changed files
5. **Download changed files** — Fetch content for new or modified files via the Contents API (`GET /repos/{owner}/{repo}/contents/{path}`)
6. **Parse links** — Extract `[[wikilinks]]` and standard markdown links from each downloaded file
7. **Build index** — Update the link index with resolved references, applying cross-repo resolution with current-repo priority

### Incremental Sync

Gleaner uses a two-level SHA comparison for efficiency:

- **Tree-level SHA** — Skips the entire repo if the root tree hasn't changed
- **File-level SHA** — Within a changed tree, only downloads files whose individual blob SHA differs from the cached version

This means that after the initial sync, subsequent syncs typically only download a handful of changed files.

### Rate Limit Handling

When the GitHub API returns a 403 (rate limit) or 429 (too many requests) response:

1. The sync engine **pauses** all requests
2. It reads the `x-ratelimit-reset` header to determine when the limit resets
3. It **waits** until the reset time
4. It **retries** the failed request and continues

No files are skipped due to rate limiting — the sync always completes, though it may take longer if pauses are needed.

## Markdown Rendering Pipeline

Gleaner uses a unified pipeline to transform Markdown into React components:

```
Source Markdown
  → remark-parse        (Markdown → mdast)
  → remark-gfm          (GitHub Flavored Markdown extensions)
  → remark-rehype        (mdast → hast, with allowDangerousHtml)
  → rehype-raw           (parse raw HTML in Markdown)
  → rehype-slug          (add IDs to headings)
  → rehype-highlight     (syntax highlight code blocks)
  → rehype-react         (hast → React elements)
```

### Custom Components

During the `rehype-react` stage, certain HTML elements are replaced with custom React components:

| HTML Element | Custom Component | Purpose |
|-------------|-----------------|---------|
| `<img>` | `RepoImage` | Routes image URLs through the configured proxy |
| `<video>` | `RepoVideo` | Converts video URLs to `raw.githubusercontent.com` and proxies them |
| `<a>` | `MdLink` | Handles wikilink navigation and internal link routing |
| `<pre>` | `CodeBlock` | Adds copy button and enhanced code block styling |
| `<table>` | `ResponsiveTable` | Wraps tables for horizontal scrolling on small screens |

## Link Resolution

The link resolution process:

1. **Extract** — During parsing, all `[[wikilinks]]` and standard `[text](path.md)` links are extracted from each file
2. **Resolve** — Each link is matched against the file index:
   - Title match (first `# heading`) takes priority over filename match
   - Current repo is searched first; other repos are searched if no match is found
3. **Index** — Resolved links are stored in the links table, enabling backlink lookups and graph construction

---

## Related

- [Proxy Setup](./Proxy%20Setup.md) — How proxy routing integrates with the sync engine
- [GitHub Token](./GitHub%20Token.md) — Authentication for API requests
- [Backlinks](../features/Backlinks.md) — How the link index powers backlinks
- [Knowledge Graph](../features/Knowledge%20Graph.md) — How the link index powers the graph
