[中文](./Multi-Repo.zh.md) | **English**

# Multi-Repo

Gleaner supports connecting multiple GitHub repositories simultaneously, allowing you to build a unified knowledge base from separate sources.

## Adding Multiple Repositories

In the Settings page, you can add as many repositories as needed. Each repository is specified in `owner/repo` format and can have its own label, branch, commit pin, and path filters.

## File Tree Organization

When multiple repos are synced, the left sidebar groups files by repository:

- Each repo appears as a top-level section with its name and a file count badge
- A status indicator shows the sync state of each repo (synced, syncing, error)
- Each section can be independently expanded or collapsed

## Cross-Repo Wikilink Resolution

Wikilinks are resolved globally across all synced repositories. When you write `[[some note]]`:

1. Gleaner first searches the **current repository** (the repo containing the file with the link)
2. If no match is found, it searches **all other synced repos**

This means you can seamlessly link between files in different repos using the same `[[wikilink]]` syntax. The current-repo priority ensures that when duplicate titles exist, the local match is preferred.

## Graph Visualization

In the [Knowledge Graph](./Knowledge%20Graph.md), each repository is assigned a distinct color. This makes it easy to:

- See which repos contribute the most content
- Identify cross-repo connections
- Toggle individual repos on or off to focus your view

## Independent Sync

Each repository syncs independently:

- You can trigger sync for all repos at once, or re-sync individual repos
- Tree SHA comparison is per-repo, so unchanged repos are skipped entirely
- If one repo fails to sync (e.g. rate limit), others are unaffected

## Organizing with Profiles

Use [Profiles](../guides/Profiles.md) to organize different sets of repos for different contexts. For example, you might have one profile for work-related repos and another for personal knowledge bases. Switching profiles loads a different repo configuration instantly.

---

## Related

- [Backlinks](./Backlinks.md) — Cross-repo link resolution details
- [Knowledge Graph](./Knowledge%20Graph.md) — Color-coded multi-repo visualization
- [Profiles](../guides/Profiles.md) — Switching between repo sets
- [Repo Config](../advanced/Repo%20Config.md) — Per-repo branch, commit, and path settings
