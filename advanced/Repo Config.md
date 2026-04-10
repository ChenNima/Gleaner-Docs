[中文](./Repo%20Config.zh.md) | **English**

# Repo Config

Each repository in Gleaner can be configured with advanced options for branch selection, commit pinning, and path filtering. These options are available via the expand button on each repo row in the Settings page.

## Branch Selection

By default, Gleaner syncs the repository's default branch (usually `main` or `master`). You can override this:

- Leave the branch field empty to use the repository's default branch
- Enter a specific branch name (e.g. `develop`, `docs`) to sync from that branch

## Commit Pinning

Commit pinning lets you lock a repository to a specific point in time, ensuring the synced content doesn't change even when new commits are pushed.

| `commit` field value | Behavior |
|---------------------|----------|
| Empty / not set | Always syncs the latest commit on the configured branch |
| `pin` | Locks to the current latest commit SHA (auto-lock) |
| A full SHA string | Locks to that exact commit |

### How to Use

- **Auto-lock** — Toggle the pin switch to lock to the current latest commit. Gleaner records the SHA automatically.
- **Manual SHA** — Paste a specific commit SHA to lock to an exact version.
- **Update to latest** — Click "Update" to refresh the pinned SHA to the current branch tip.
- **Unlock** — Toggle the pin switch off to return to always-latest behavior.

Commit pinning is useful for documentation snapshots, stable reference versions, or preventing unexpected content changes.

## Path Filtering

Path filtering lets you control which files are synced from a repository. This is useful for large repos where you only need specific directories.

### `includePaths`

An array of path prefixes. When specified, only files whose path starts with one of these prefixes are included.

```yaml
includePaths:
  - docs/
  - notes/guides/
```

If a file's path matches **any** of the include prefixes, it is included.

### `excludePaths`

An array of path prefixes. Files whose path starts with any of these prefixes are excluded, **after** include filtering is applied.

```yaml
excludePaths:
  - docs/drafts/
  - docs/archive/
```

### Evaluation Order

1. If `includePaths` is set, only files matching at least one include prefix pass through
2. Then, any files matching an `excludePaths` prefix are removed
3. Remaining files are synced

If neither is set, all `.md` files in the repo are synced.

## Full YAML Format

```yaml
repos:
  - repo: owner/repo-name
    label: Display Name
    branch: main
    commit: abc123def456...
    includePaths:
      - docs/
      - guides/
    excludePaths:
      - docs/drafts/
      - docs/internal/
```

## Use Cases

| Scenario | Configuration |
|----------|--------------|
| Sync only a `docs/` folder | `includePaths: ["docs/"]` |
| Exclude draft content | `excludePaths: ["drafts/", "wip/"]` |
| Lock to a release version | `commit: <release-sha>` |
| Track a feature branch | `branch: feature/new-docs` |
| Sync everything (default) | Leave all fields empty |

---

## Related

- [Profiles](../guides/Profiles.md) — Managing YAML configuration files
- [Multi-Repo](../features/Multi-Repo.md) — Working with multiple repos
- [First Setup](../getting-started/First%20Setup.md) — Adding your first repo
