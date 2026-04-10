**中文** | [English](./Proxy%20Setup.md)

# 代理配置

在 GitHub API 访问受限或不稳定的地区，你可以配置代理服务器来路由所有 GitHub API 请求。

## 工作原理

配置代理 URL 后，Gleaner 会将其添加到所有 GitHub API 请求 URL 的前面。例如：

- 无代理：`https://api.github.com/repos/owner/repo/git/trees/main`
- 有代理：`https://your-proxy.com/https://api.github.com/repos/owner/repo/git/trees/main`

代理服务器接收完整的 GitHub URL 并代为转发请求。

## 配置方法

1. 打开设置页面
2. 切换到 **Token** 选项卡
3. 在代理字段中输入代理 URL（如 `https://gh-proxy.com`）
4. 点击「保存」

代理会立即应用到所有后续的 API 请求。

## 代理要求

并非所有代理服务都兼容。代理必须支持：

- **CORS** — 代理必须包含适当的 `Access-Control-Allow-Origin` 响应头，因为请求来自浏览器
- **完整 URL 转发** — 代理必须接受完整的 GitHub API URL 作为路径参数并原样转发
- **请求头转发** — 代理必须转发请求头（特别是用于 Token 认证的 `Authorization` 头）

## 推荐代理

**[gh-proxy.com](https://gh-proxy.com)** 是一个常用的代理服务，满足上述要求。

> **重要提示：**网上找到的许多 "ghproxy" 服务仅设计用于 `git clone` 操作，**不支持** GitHub REST API。在依赖之前，请验证你选择的代理是否支持 `/repos/{owner}/{repo}/git/trees/{sha}` 等 REST API 端点。

## 媒体代理

Gleaner 同样会代理 Markdown 文件中嵌入的媒体内容：

- **图片** — 指向 GitHub 的图片 URL 会自动通过配置的代理路由
- **视频** — 视频 URL 会自动转换为 `raw.githubusercontent.com` 格式并通过代理加载

这确保了在网络受限环境中，Markdown 文件中的图片和视频也能正常加载。

## 验证

配置代理后，按以下步骤验证：

1. 添加一个仓库并触发同步
2. 检查文件树是否成功加载
3. 打开一个包含图片的文件，确认媒体内容正常加载
4. 如果同步失败，检查浏览器控制台中是否有 CORS 或网络错误

---

## 相关文档

- [GitHub Token 配置](./GitHub%20Token.zh.md) — 通过代理进行 Token 认证
- [首次配置](../getting-started/First%20Setup.zh.md) — 初始配置
- [技术架构](./Architecture.zh.md) — 同步引擎如何发起 API 请求
