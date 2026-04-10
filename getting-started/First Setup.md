[中文](./First%20Setup.zh.md) | **English**

# First Setup

This guide walks you through creating your first profile, adding repositories, and understanding the sync process.

## Creating a Profile

On first launch, Gleaner redirects you to the Settings page. You need to create a profile to get started.

There are two profile types:

- **Local** — Configuration is stored entirely in your browser. You manually add repos in the Settings UI.
- **GitHub** — Configuration is loaded from a `gleaner.yaml` file in a GitHub repository. Ideal for sharing setups across devices.

For most users, a **Local** profile is the simplest way to begin.

> For more on profile management, see [Profiles](../guides/Profiles.md).

## Adding Repositories

In the Settings page under the "Repositories" tab:

1. Enter a GitHub repository in `owner/repo` format (e.g. `ChenNima/Gleaner-Docs`)
2. Optionally add a label for easy identification
3. Click "Add" to add it to the list
4. Click "Save & Sync" to start syncing

You can add multiple repositories. See [Repo Config](../advanced/Repo%20Config.md) for advanced options like branch selection, commit pinning, and path filtering.

## How Sync Works

When you click "Save & Sync", Gleaner performs the following steps:

1. **Fetch tree** — Calls the GitHub Trees API to get the full file listing for each repo
2. **Filter Markdown** — Keeps only `.md` files (and respects path filters if configured)
3. **Download content** — Fetches the content of each Markdown file via the GitHub Contents API
4. **Parse links** — Extracts `[[wikilinks]]` and standard markdown links from each file, resolving them to build the link index

This entire process happens in your browser. Files and their parsed links are cached in IndexedDB, so subsequent syncs are incremental — only changed files are re-downloaded.

## Sync Progress

During sync, a progress indicator appears in the status bar at the bottom of the page. It shows:

- The current phase (fetching tree, downloading files, parsing)
- A count of files processed vs. total
- Estimated time remaining for large repos

## Token Recommendation

Without a GitHub Personal Access Token, you are limited to **60 API requests per hour**. For any repo with more than a few dozen files, you will likely hit this limit during initial sync.

We strongly recommend configuring a token before syncing large repositories. See [GitHub Token](../advanced/GitHub%20Token.md) for setup instructions.

> If you are in a region with restricted access to GitHub, you may also need to configure a [Proxy](../advanced/Proxy%20Setup.md).

---

## What's Next

- Manage multiple configurations with [Profiles](../guides/Profiles.md)
- Explore your synced files with [File Browsing](../features/File%20Browsing.md)
- Use [Search](../features/Search.md) to quickly find content across all repos
