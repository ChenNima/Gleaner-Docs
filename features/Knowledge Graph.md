[中文](./Knowledge%20Graph.zh.md) | **English**

# Knowledge Graph

The Knowledge Graph displays all files and their connections across your synced repositories as a force-directed graph.

## Global Graph

Access the global graph from the navigation bar. It displays:

- **Nodes** — Each Markdown file appears as a node
- **Edges** — Each link (wikilink or standard markdown link) between files appears as an edge
- **Color coding** — Nodes are colored by their source repository, making it easy to distinguish files from different repos

### Interactions

- **Hover** — Hovering over a node highlights it and its direct connections, dimming unrelated nodes
- **Click** — Clicking a node navigates to that file in the content viewer
- **Scroll zoom** — Use the mouse scroll wheel to zoom in and out
- **Drag** — Drag individual nodes to reposition them, or drag the background to pan the view

### Filters

The graph toolbar provides filtering options:

- **External links toggle** — Show or hide edges to external URLs
- **Repo visibility** — Toggle individual repositories on or off to focus on specific subsets of your knowledge base

## Local Graph

In addition to the global graph page, a **local graph** is available in the right panel when viewing any file. It shows:

- The current file as the center node
- All files within 1 degree of connection (files that link to or are linked from the current file)
- The edges between those files

The local graph shows a file's immediate context without navigating away from the page.

## Use Cases

| Goal | How the Graph Helps |
|------|-------------------|
| Find isolated notes | Look for nodes with no edges — these files have no links to or from other files |
| Identify hub documents | Large, highly connected nodes are key reference documents |
| Trace paths | Follow edges between nodes to see how two topics relate |
| Get a repo overview | Color coding shows how content is distributed across repositories |

---

## Related

- [Backlinks](./Backlinks.md) — The link data that powers the graph
- [File Browsing](./File%20Browsing.md) — The local graph in the right panel
- [Multi-Repo](./Multi-Repo.md) — How repos are color-coded in the graph
- [Search](./Search.md) — Another way to find and navigate files
