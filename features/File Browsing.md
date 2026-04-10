[中文](./File%20Browsing.zh.md) | **English**

# File Browsing

Gleaner uses a three-column layout similar to Obsidian for navigating and reading Markdown files.

## Layout Overview

| Column | Position | Content |
|--------|----------|---------|
| File Tree | Left sidebar | Repository file tree with expand/collapse |
| Content Area | Center | Markdown rendering with breadcrumb navigation |
| Right Panel | Right sidebar | Links tab (backlinks + outgoing) and Graph tab (local graph) |

## File Tree (Left Sidebar)

The left sidebar displays the file tree for all synced repositories.

- **Expand/collapse** — Click folder icons to expand or collapse directories
- **Sorting** — Directories are listed first, followed by files, both sorted alphabetically
- **Multi-repo sections** — When multiple repositories are configured, each repo appears as a top-level section with its own collapsible tree
- **Collapse all** — Use the collapse-all button at the top of the sidebar to collapse the entire tree at once

Clicking a `.md` file opens it in the content area.

## Content Area

The center column renders the selected Markdown file with full support for:

- **Standard Markdown** — Headings, paragraphs, lists, blockquotes, images, tables
- **GitHub Flavored Markdown (GFM)** — Task lists, strikethrough, autolinks, tables
- **Syntax-highlighted code blocks** — Language-specific highlighting via highlight.js
- **Inline HTML** — Raw HTML elements are rendered as-is
- **Wikilinks** — `[[target]]` and `[[target|alias]]` links are rendered as clickable links that navigate within Gleaner

### Breadcrumb Navigation

A breadcrumb bar appears above the content, showing the full path from the repository root to the current file. Each segment is clickable for quick navigation up the directory hierarchy.

## Right Panel

The right sidebar provides two tabs:

- **Links** — Shows [backlinks](./Backlinks.md) (other files that link to this one), outgoing links (links from this file to others), and external links
- **Graph** — Displays a local [Knowledge Graph](./Knowledge%20Graph.md) centered on the current file, showing its immediate connections

## Sidebar Controls

- **Toggle buttons** — Both sidebars can be toggled on/off using buttons in the top navigation bar
- **Drag to resize** — On desktop, drag the sidebar edges to adjust their width
- **Mobile overlay** — On small screens, sidebars open as overlays that can be dismissed by tapping outside

---

## Related

- [Multi-Repo](./Multi-Repo.md) — Managing files from multiple repositories
- [Backlinks](./Backlinks.md) — Understanding the links panel
- [Knowledge Graph](./Knowledge%20Graph.md) — Exploring the graph view
- [Themes](../guides/Themes.md) — Changing the visual appearance
- [Search](./Search.md) — Finding files quickly
- [Shortcuts](../guides/Shortcuts.md) — Keyboard navigation tips
