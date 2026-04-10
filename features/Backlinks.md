[中文](./Backlinks.zh.md) | **English**

# Backlinks

Gleaner tracks both wikilinks and standard markdown links to build a link index, enabling bidirectional navigation between Markdown files.

## Wikilink Syntax

Gleaner supports the same wikilink syntax used by Obsidian:

- **Basic link** — `[[target]]` creates a link to a file named "target"
- **Aliased link** — `[[target|display text]]` creates a link that shows "display text" but navigates to "target"

Wikilinks are rendered as clickable links in the content area, styled distinctly from standard markdown links.

## Link Resolution Rules

When you write `[[target]]`, Gleaner resolves it using the following priority:

1. **Title match** — Looks for a file whose title (first `# heading`) matches "target"
2. **Filename match** — Looks for a file whose filename (without `.md` extension) matches "target"
3. **Cross-repo resolution** — If no match is found in the current repo, Gleaner searches all other synced repos

When multiple matches exist across repos, the file in the **current repository** (the repo containing the linking file) takes priority.

## Link States

Links are visually styled to indicate their resolution status:

- **Resolved links** — Displayed as standard clickable links; clicking navigates to the target file
- **Unresolved links** — Displayed with a distinct style (typically dimmed or with a dashed underline) to indicate no matching file was found

## Standard Markdown Links

In addition to wikilinks, Gleaner also tracks standard markdown links:

```markdown
[display text](./path/to/file.md)
```

These are parsed and included in the link index, so they appear in backlink panels and the knowledge graph just like wikilinks.

## Right Panel: Links Tab

When viewing a file, the right panel's **Links** tab shows three sections:

- **Backlinks** — Files that link *to* the current file (via wikilinks or standard links)
- **Outgoing links** — Files that the current file links *to*
- **External links** — URLs pointing outside the knowledge base (e.g. `https://...`)

Each entry shows the file title and a snippet of the surrounding context.

## Visualization

All tracked links are visualized in the [Knowledge Graph](./Knowledge%20Graph.md), where files appear as nodes and links as edges. This provides a bird's-eye view of how your notes are interconnected.

## Tips

- **Use wikilinks liberally** — The more you link between notes, the richer your backlinks and graph become
- **Choose clear titles** — Since resolution first checks titles, a clear and unique first heading (`# Title`) makes linking more reliable
- **Check unresolved links** — Periodically review unresolved links to fix typos or create missing files

---

## Related

- [Knowledge Graph](./Knowledge%20Graph.md) — Visualizing the link network
- [Multi-Repo](./Multi-Repo.md) — Cross-repo link resolution
- [File Browsing](./File%20Browsing.md) — Navigating the three-column layout
