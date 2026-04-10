**中文** | [English](./GitHub%20Token.md)

# GitHub Token 配置

配置 GitHub Personal Access Token (PAT) 可以大幅提升 API 速率限制，并支持访问私有仓库。

## 速率限制

| 配置方式 | 速率限制 |
|---------|---------|
| 未配置 Token | 60 次请求/小时 |
| 配置 Token | 5,000 次请求/小时 |

对于文件数超过几十个的仓库，未认证的 60 次/小时限制在初次同步时会很快耗尽。强烈建议配置 Token 以便正常使用。

## 创建 Token

1. 前往 [GitHub Settings > Developer settings > Personal access tokens > Fine-grained tokens](https://github.com/settings/personal-access-tokens/new)
2. 为 Token 输入一个描述性名称（如 "Gleaner Reader"）
3. 设置过期时间
4. 在 **Repository access** 下，选择你希望 Gleaner 访问的仓库（或选择 "All repositories"）
5. 在 **Permissions** 下，展开 "Repository permissions"，将 **Contents** 设置为 **Read-only**
6. 点击 "Generate token" 并复制 Token 值

> 只需要 **只读 Contents** 权限。Gleaner 永远不会向你的仓库写入任何内容。

## 在 Gleaner 中配置

1. 打开设置页面
2. 切换到 **Token** 选项卡
3. 将 Token 粘贴到输入框中
4. 点击「保存」

Token 会立即生效。下次同步将使用已认证的速率限制。

## 存储方式

Token 存储在浏览器本地的 IndexedDB 数据库中：

- **永远不会发送到任何服务器** — Gleaner 是纯 SPA，没有后端
- **仅发送到 GitHub API**（或你配置的代理）作为 `Authorization` 请求头
- **跨会话持久化** — 每个浏览器只需输入一次

## 私有仓库访问

配置了具有私有仓库访问权限的 Token 后，Gleaner 可以像同步公开仓库一样同步私有仓库。只需在设置中以 `owner/repo` 格式添加私有仓库，并确保 Token 对其有读取权限。

## 安全建议

- **仅限本地** — Token 除了直接向 GitHub 发起 API 调用外，永远不会离开浏览器
- **无后端** — 没有服务器可以拦截或存储你的 Token
- **只读权限** — 仅授予只读 Contents 权限；Gleaner 不需要写入权限
- **定期轮换** — 设置合理的过期时间，定期生成新 Token
- **使用细粒度 Token** — 优先使用 Fine-grained Token 而非 Classic Token，以最小化权限范围

---

## 相关文档

- [首次配置](../getting-started/First%20Setup.zh.md) — 包括 Token 在内的初始配置
- [代理配置](./Proxy%20Setup.zh.md) — 为网络受限地区配置代理
- [快速开始](../getting-started/Quick%20Start.zh.md) — 开始使用 Gleaner
