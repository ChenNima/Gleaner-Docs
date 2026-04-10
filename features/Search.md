[中文](./Search.zh.md) | **English**

# Search

Gleaner provides a fast, Cmd+K style command palette for searching across all your synced files. Search runs entirely against the local cache, so results appear instantly.

## Opening Search

There are three ways to open the search dialog:

| Method | Description |
|--------|-------------|
| **Cmd+K** (Mac) / **Ctrl+K** (Windows/Linux) | Keyboard shortcut from anywhere in the app |
| **Navbar button** | Click the search icon in the top navigation bar |
| **Mobile menu** | Tap the search option in the mobile hamburger menu |

## How It Works

Search queries are matched against both the **title** (first `# heading`) and the **full content** of each file. Matching is case-insensitive and runs entirely against the local IndexedDB cache, requiring no network requests.

Results appear as you type, with no delay.

## Search Results

Each result displays:

- **Title** — The file's first heading or filename
- **Repo badge** — A colored badge indicating which repository the file belongs to
- **Snippet** — Approximately 120 characters of context around the match, with the matching text highlighted
- **File path** — The relative path within the repository

Results are ranked by relevance, with title matches weighted higher than content matches.

## Keyboard Navigation

Once the search dialog is open, you can navigate entirely with the keyboard:

| Key | Action |
|-----|--------|
| **Up / Down arrows** | Move selection through the result list |
| **Enter** | Open the selected file |
| **Esc** | Close the search dialog |

## Tips

- **Incremental search** — Start typing and results refine in real time; you don't need to press Enter to search
- **Partial matches work** — You don't need to type the full title or word; partial strings match as expected
- **Search across repos** — Results include files from all synced repositories, not just the current one

---

## Related

- [File Browsing](./File%20Browsing.md) — Navigating files via the sidebar tree
- [Backlinks](./Backlinks.md) — Finding connections between files
- [Multi-Repo](./Multi-Repo.md) — Search spans all configured repos
- [Shortcuts](../guides/Shortcuts.md) — Full keyboard shortcut reference
