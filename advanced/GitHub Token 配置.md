# GitHub Token 配置

配置 GitHub Personal Access Token (PAT) 可以大幅提升 API 访问限额，并允许访问私有仓库。

## 为什么需要 Token

GitHub API 对未认证请求有严格的速率限制：

| 模式 | 限额 |
|------|------|
| **无 Token** | 60 次/小时 |
| **有 Token** | 5,000 次/小时 |

如果你的仓库包含较多文件（> 50 个 .md 文件），建议配置 Token 以避免同步时触发限额。

> 每个文件的内容下载需要 1 次 API 调用。一个 200 文件的仓库首次同步就需要 200+ 次请求。

## 创建 Token

1. 访问 [github.com/settings/tokens](https://github.com/settings/tokens)
2. 选择 **Fine-grained personal access tokens**
3. 权限设置：只需 **Contents** 的 **Read-only** 权限
4. 建议设置合理的过期时间

> 遵循最小权限原则：Gleaner 只需要读取仓库内容的权限。

## 配置 Token

在设置页面的「访问令牌」选项卡中：

1. 粘贴你的 Token（格式如 `ghp_xxxxxxxxxxxx`）
2. 点击「保存令牌」

Token 保存在浏览器的 IndexedDB 中，不会发送到任何第三方服务器。

## 访问私有仓库

配置 Token 后，你可以在 [[多仓库管理|仓库列表]] 中添加你有读取权限的私有仓库。确保 Token 的权限范围包含目标仓库。

## 安全提示

- Token 仅存储在本地浏览器中
- 所有 API 请求直接发往 GitHub（或配置的 [[代理配置|代理]]）
- Gleaner 没有后端服务器，不会中转你的 Token
- 建议为 Gleaner 创建专用的只读 Token
- 定期轮换 Token

## 相关

- [[首次配置]] — 基础配置流程
- [[代理配置]] — GitHub API 代理设置
- [[快速开始]] — 入门指南
