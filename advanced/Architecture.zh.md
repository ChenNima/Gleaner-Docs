**中文** | [English](./Architecture.md)

# 技术架构

本文档描述了 Gleaner 的内部架构，包括数据流、技术栈、数据模型、同步引擎和 Markdown 渲染管线。

## 概览

```
浏览器
  ├── React UI ←→ Zustand Stores ←→ IndexedDB (Dexie.js)
  │
  └── 同步引擎 ──→ GitHub REST API
                    （可选通过代理）
```

Gleaner 作为单页应用完全在浏览器中运行，没有后端服务器。所有数据从 GitHub REST API 获取并缓存在本地 IndexedDB 中。

## 技术栈

| 层级 | 技术 |
|------|------|
| 框架 | Vite + React 19 + TypeScript |
| 状态管理 | Zustand |
| 本地数据库 | IndexedDB（通过 Dexie.js） |
| 样式 | Tailwind CSS 4 + shadcn/ui 规范 |
| Markdown 渲染 | unified（remark + rehype 管线） |
| 图谱可视化 | react-force-graph-2d |
| 包管理器 | pnpm |
| E2E 测试 | Playwright |

## 数据模型

Gleaner 使用四个主要的 IndexedDB 表：

| 表 | 描述 |
|----|------|
| **repos** | 仓库元数据：owner、仓库名、分支、commit SHA、同步状态 |
| **files** | 文件内容和元数据：路径、内容、标题（第一个标题）、文件树 SHA |
| **links** | 解析后的链接索引：源文件、目标文件、链接类型（wikilink/标准）、解析状态 |
| **profiles** | Profile 配置：名称、类型（本地/GitHub）、仓库列表、设置 |

## 同步流程

同步引擎对每个仓库执行以下步骤：

1. **获取文件树** — 调用 GitHub Trees API（`GET /repos/{owner}/{repo}/git/trees/{branch}?recursive=1`）获取完整文件列表
2. **比较文件树 SHA** — 如果文件树 SHA 与缓存值匹配，说明此仓库未变化，可以完全跳过
3. **过滤 `.md` 文件** — 仅保留 Markdown 文件，同时应用 `includePaths` 和 `excludePaths` 过滤规则
4. **比较文件 SHA** — 对每个 `.md` 文件，比较其 blob SHA 与缓存版本以识别变更文件
5. **下载变更文件** — 通过 Contents API（`GET /repos/{owner}/{repo}/contents/{path}`）获取新增或修改文件的内容
6. **解析链接** — 从每个下载的文件中提取 `[[wikilinks]]` 和标准 Markdown 链接
7. **构建索引** — 使用解析后的引用更新链接索引，应用跨仓库解析（当前仓库优先）

### 增量同步

Gleaner 使用两级 SHA 比较以提高效率：

- **文件树级 SHA** — 如果根文件树未变化，跳过整个仓库
- **文件级 SHA** — 在变化的文件树中，只下载 blob SHA 与缓存版本不同的文件

这意味着初次同步后，后续同步通常只需要下载少量变更文件。

### 速率限制处理

当 GitHub API 返回 403（速率限制）或 429（请求过多）响应时：

1. 同步引擎**暂停**所有请求
2. 读取 `x-ratelimit-reset` 响应头以确定限制重置时间
3. **等待**直到重置时间
4. **重试**失败的请求并继续

不会因为速率限制而跳过任何文件——同步始终会完成，只是在需要暂停时可能耗时更长。

## Markdown 渲染管线

Gleaner 使用 unified 管线将 Markdown 转换为 React 组件：

```
源 Markdown
  → remark-parse        （Markdown → mdast）
  → remark-gfm          （GitHub 风格 Markdown 扩展）
  → remark-rehype        （mdast → hast，允许危险 HTML）
  → rehype-raw           （解析 Markdown 中的原始 HTML）
  → rehype-slug          （为标题添加 ID）
  → rehype-highlight     （代码块语法高亮）
  → rehype-react         （hast → React 元素）
```

### 自定义组件

在 `rehype-react` 阶段，某些 HTML 元素被替换为自定义 React 组件：

| HTML 元素 | 自定义组件 | 用途 |
|-----------|-----------|------|
| `<img>` | `RepoImage` | 将图片 URL 通过配置的代理路由 |
| `<video>` | `RepoVideo` | 将视频 URL 转换为 `raw.githubusercontent.com` 格式并代理 |
| `<a>` | `MdLink` | 处理 wikilink 导航和内部链接路由 |
| `<pre>` | `CodeBlock` | 添加复制按钮和增强的代码块样式 |
| `<table>` | `ResponsiveTable` | 在小屏幕上为表格添加水平滚动包裹 |

## 链接解析

链接解析过程：

1. **提取** — 在解析过程中，从每个文件中提取所有 `[[wikilinks]]` 和标准 `[文本](路径.md)` 链接
2. **解析** — 将每个链接与文件索引匹配：
   - 标题匹配（第一个 `# 标题`）优先于文件名匹配
   - 首先搜索当前仓库；如果未找到匹配项，再搜索其他仓库
3. **索引** — 解析后的链接存储在 links 表中，支持反向链接查询和图谱构建

---

## 相关文档

- [代理配置](./Proxy%20Setup.zh.md) — 代理路由如何与同步引擎集成
- [GitHub Token 配置](./GitHub%20Token.zh.md) — API 请求的认证
- [双向链接](../features/Backlinks.zh.md) — 链接索引如何驱动反向链接
- [知识图谱](../features/Knowledge%20Graph.zh.md) — 链接索引如何驱动图谱
