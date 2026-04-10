**中文** | [English](./First%20Setup.md)

# 首次配置

本指南将引导你创建第一个配置文件、添加仓库，并了解同步过程。

## 创建 Profile

首次启动时，Gleaner 会将你重定向到设置页面。你需要创建一个 Profile 才能开始使用。

有两种 Profile 类型：

- **本地（Local）** — 配置完全存储在浏览器中。你在设置界面手动添加仓库。
- **GitHub** — 配置从 GitHub 仓库中的 `gleaner.yaml` 文件加载。适合在多台设备之间共享配置。

对于大多数用户，**本地** Profile 是最简单的入门方式。

> 更多 Profile 管理内容请参见 [配置文件管理](../guides/Profiles.zh.md)。

## 添加仓库

在设置页面的「仓库」选项卡中：

1. 输入 GitHub 仓库地址，格式为 `owner/repo`（例如 `ChenNima/Gleaner-Docs`）
2. 可选：填写一个易于辨认的标签
3. 点击「添加」将其加入列表
4. 点击「保存并同步」开始同步

你可以添加多个仓库。高级选项（如分支选择、版本锁定、路径过滤）请参见 [仓库高级配置](../advanced/Repo%20Config.zh.md)。

## 同步原理

当你点击「保存并同步」时，Gleaner 会执行以下步骤：

1. **获取文件树** — 调用 GitHub Trees API 获取每个仓库的完整文件列表
2. **过滤 Markdown** — 仅保留 `.md` 文件（如果配置了路径过滤规则则同时应用）
3. **下载内容** — 通过 GitHub Contents API 获取每个 Markdown 文件的内容
4. **解析链接** — 从每个文件中提取 `[[wikilinks]]` 和标准 Markdown 链接，解析后构建链接索引

整个过程在浏览器中完成。文件及其解析后的链接缓存在 IndexedDB 中，后续同步为增量模式——只会重新下载有变化的文件。

## 同步进度

同步期间，页面底部状态栏会显示进度指示器，包括：

- 当前阶段（获取文件树、下载文件、解析中）
- 已处理文件数 / 总文件数
- 大型仓库的预估剩余时间

## Token 建议

如果没有配置 GitHub Personal Access Token，你的 API 请求限制为**每小时 60 次**。对于文件数超过几十个的仓库，首次同步时很可能触及此限制。

我们强烈建议在同步大型仓库之前配置 Token。配置方法请参见 [GitHub Token 配置](../advanced/GitHub%20Token.zh.md)。

> 如果你所在的地区访问 GitHub 受限，可能还需要配置 [代理](../advanced/Proxy%20Setup.zh.md)。

---

## 接下来

- 使用 [配置文件管理](../guides/Profiles.zh.md) 管理多套配置
- 通过 [文件浏览](../features/File%20Browsing.zh.md) 浏览已同步的文件
- 使用 [全局搜索](../features/Search.zh.md) 在所有仓库中快速查找内容
