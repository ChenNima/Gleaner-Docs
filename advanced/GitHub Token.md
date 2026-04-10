[中文](./GitHub%20Token.zh.md) | **English**

# GitHub Token

Configuring a GitHub Personal Access Token (PAT) dramatically increases your API rate limit and enables access to private repositories.

## Rate Limits

| Configuration | Rate Limit |
|--------------|------------|
| Without token | 60 requests/hour |
| With token | 5,000 requests/hour |

For any repository with more than a handful of files, the unauthenticated limit of 60 requests/hour will be exhausted quickly during initial sync. A token is strongly recommended for practical use.

## Creating a Token

1. Go to [GitHub Settings > Developer settings > Personal access tokens > Fine-grained tokens](https://github.com/settings/personal-access-tokens/new)
2. Give the token a descriptive name (e.g. "Gleaner Reader")
3. Set an expiration date
4. Under **Repository access**, select the repos you want Gleaner to access (or "All repositories" for convenience)
5. Under **Permissions**, expand "Repository permissions" and set **Contents** to **Read-only**
6. Click "Generate token" and copy the token value

> Only **read-only Contents** permission is needed. Gleaner never writes to your repositories.

## Configuring in Gleaner

1. Open the Settings page
2. Navigate to the **Token** tab
3. Paste your token into the token field
4. Click "Save"

The token is applied immediately. Your next sync will use the authenticated rate limit.

## Storage

Your token is stored locally in the browser's IndexedDB database. It is:

- **Never sent to any server** — Gleaner is a pure SPA with no backend
- **Only sent to GitHub's API** (or your configured proxy) as an `Authorization` header
- **Persisted across sessions** — You only need to enter it once per browser

## Private Repository Access

With a token that has access to private repositories, Gleaner can sync those repos just like public ones. Simply add the private repo in `owner/repo` format in Settings, and ensure the token has read access to it.

## Security Tips

- **Local only** — Your token never leaves the browser except in direct API calls to GitHub
- **No backend** — There is no server that could intercept or store your token
- **Read-only** — Only grant read-only Contents permission; Gleaner has no need for write access
- **Rotate regularly** — Set a reasonable expiration date and generate a new token periodically
- **Use fine-grained tokens** — Prefer fine-grained tokens over classic tokens for minimal scope

---

## Related

- [First Setup](../getting-started/First%20Setup.md) — Initial configuration including token
- [Proxy Setup](./Proxy%20Setup.md) — Configure a proxy for restricted regions
- [Quick Start](../getting-started/Quick%20Start.md) — Getting started with Gleaner
