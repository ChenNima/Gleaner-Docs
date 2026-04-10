[中文](./Profiles.zh.md) | **English**

# Profiles

Profiles let you maintain multiple configurations in Gleaner, each with its own set of repositories and settings. This is useful for organizing different knowledge bases or sharing configurations across devices.

## Profile Types

### Local Profile

- Configuration is stored entirely in your browser's IndexedDB
- You add and manage repos through the Settings UI
- Best for quick personal use on a single device

### GitHub Profile

- Configuration is loaded from a `gleaner.yaml` file stored in a GitHub repository
- You specify the config repo in `owner/repo` format
- Best for sharing configurations across devices or with others
- Changes to the YAML file on GitHub are picked up on next sync

## Creating a Profile

1. Open the Settings page
2. Click "New Profile"
3. Choose a profile type (Local or GitHub)
4. Give it a name
5. For GitHub profiles, specify the config repo that contains the `gleaner.yaml` file

## Switching Profiles

Select a different profile from the profile dropdown in Settings. When you switch:

1. Any active sync is aborted
2. The new profile's configuration is loaded
3. Shared cache (file content) from previously synced repos is preserved
4. An automatic sync starts for the new profile's repos

This means switching is fast — repos that were already synced under a previous profile don't need to be re-downloaded.

## Deleting a Profile

Click the delete button next to a profile in the Settings page. This removes the profile configuration but does not delete cached file data. Other profiles that reference the same repos will still have access to cached content.

## YAML Configuration Format

For GitHub profiles, the `gleaner.yaml` file uses this format:

```yaml
repos:
  - repo: owner/repo-name
    label: My Knowledge Base
    branch: main
    includePaths:
      - docs/
      - notes/
    excludePaths:
      - docs/drafts/

  - repo: another-owner/another-repo
    label: Reference Docs
```

All fields except `repo` are optional. See [Repo Config](../advanced/Repo%20Config.md) for full details on each field.

## Import & Export

Gleaner supports several ways to transfer profile configurations:

- **Download YAML** — Export the current profile's configuration as a `.yaml` file
- **Upload file** — Import a `.yaml` file from your local filesystem to create or update a profile
- **Import from GitHub** — Specify a GitHub repo containing a `gleaner.yaml` to import its configuration directly

---

## Related

- [First Setup](../getting-started/First%20Setup.md) — Creating your first profile
- [Multi-Repo](../features/Multi-Repo.md) — Managing multiple repos in a profile
- [Repo Config](../advanced/Repo%20Config.md) — Detailed repo configuration options
