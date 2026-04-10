[中文](./Proxy%20Setup.zh.md) | **English**

# Proxy Setup

In regions where access to GitHub's API is restricted or unreliable, you can configure a proxy to route all GitHub API requests through an intermediary server.

## How It Works

When a proxy URL is configured, Gleaner prepends it to all GitHub API request URLs. For example:

- Without proxy: `https://api.github.com/repos/owner/repo/git/trees/main`
- With proxy: `https://your-proxy.com/https://api.github.com/repos/owner/repo/git/trees/main`

The proxy server receives the full GitHub URL and forwards the request on your behalf.

## Configuration

1. Open the Settings page
2. Navigate to the **Token** tab
3. Enter the proxy URL in the proxy field (e.g. `https://gh-proxy.com`)
4. Click "Save"

The proxy is applied immediately to all subsequent API requests.

## Proxy Requirements

Not all proxy services are compatible. The proxy must support:

- **CORS** — The proxy must include appropriate `Access-Control-Allow-Origin` headers, since requests come from a browser
- **Full URL forwarding** — The proxy must accept the full GitHub API URL as a path parameter and forward it as-is
- **Header forwarding** — The proxy must forward request headers (especially `Authorization` for token-authenticated requests)

## Recommended Proxy

**[gh-proxy.com](https://gh-proxy.com)** is a commonly used proxy that meets these requirements.

> **Important:** Many "ghproxy" services found online are designed only for `git clone` operations and do **not** support the GitHub REST API. Verify that your chosen proxy works with REST API endpoints like `/repos/{owner}/{repo}/git/trees/{sha}` before relying on it.

## Media Proxy

Gleaner also proxies media content embedded in Markdown files:

- **Images** — Image URLs pointing to GitHub are automatically routed through the configured proxy
- **Videos** — Video URLs are automatically converted to `raw.githubusercontent.com` format and proxied

This ensures that images and videos in your Markdown files load correctly even in restricted network environments.

## Verification

After configuring a proxy, verify it works:

1. Add a repository and trigger a sync
2. Check that the file tree loads successfully
3. Open a file with images to confirm media loads correctly
4. If sync fails, check the browser console for CORS or network errors

---

## Related

- [GitHub Token](./GitHub%20Token.md) — Token authentication through the proxy
- [First Setup](../getting-started/First%20Setup.md) — Initial configuration
- [Architecture](./Architecture.md) — How the sync engine makes API requests
