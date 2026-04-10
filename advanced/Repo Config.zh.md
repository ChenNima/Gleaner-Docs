**中文** | [English](./Repo%20Config.md)

# 仓库高级配置

Gleaner 中的每个仓库都可以配置高级选项，包括分支选择、版本锁定和路径过滤。这些选项可以通过设置页面中每个仓库行的展开按钮访问。

## 分支选择

默认情况下，Gleaner 同步仓库的默认分支（通常是 `main` 或 `master`）。你可以覆盖此设置：

- 分支字段留空则使用仓库的默认分支
- 输入特定的分支名（如 `develop`、`docs`）以从该分支同步

## 版本锁定

版本锁定（Commit Pinning）允许你将仓库锁定到特定的时间点，确保同步的内容不会因新提交的推送而改变。

| `commit` 字段值 | 行为 |
|----------------|------|
| 空 / 未设置 | 始终同步配置分支上的最新提交 |
| `pin` | 锁定到当前最新提交的 SHA（自动锁定） |
| 完整的 SHA 字符串 | 锁定到该确切的提交 |

### 使用方法

- **自动锁定** — 切换锁定开关以锁定到当前最新提交。Gleaner 会自动记录 SHA。
- **手动输入 SHA** — 粘贴特定的提交 SHA 以锁定到确切版本。
- **更新到最新** — 点击「更新」按钮将锁定的 SHA 刷新为当前分支的最新提交。
- **解锁** — 关闭锁定开关以恢复始终同步最新版本的行为。

版本锁定适用于文档快照、稳定参考版本，或防止意外的内容变更。

## 路径过滤

路径过滤允许你控制从仓库同步哪些文件。这对于只需要特定目录的大型仓库非常有用。

### `includePaths`

路径前缀数组。指定后，只有路径以这些前缀之一开头的文件才会被包含。

```yaml
includePaths:
  - docs/
  - notes/guides/
```

如果文件的路径匹配**任意一个**包含前缀，则该文件被包含。

### `excludePaths`

路径前缀数组。路径以这些前缀之一开头的文件会被排除，**在**包含过滤之后应用。

```yaml
excludePaths:
  - docs/drafts/
  - docs/archive/
```

### 评估顺序

1. 如果设置了 `includePaths`，只有匹配至少一个包含前缀的文件通过
2. 然后，匹配 `excludePaths` 前缀的文件被移除
3. 剩余文件被同步

如果两者都未设置，仓库中所有 `.md` 文件都会被同步。

## 完整 YAML 格式

```yaml
repos:
  - repo: owner/repo-name
    label: 显示名称
    branch: main
    commit: abc123def456...
    includePaths:
      - docs/
      - guides/
    excludePaths:
      - docs/drafts/
      - docs/internal/
```

## 使用场景

| 场景 | 配置方式 |
|------|---------|
| 仅同步 `docs/` 文件夹 | `includePaths: ["docs/"]` |
| 排除草稿内容 | `excludePaths: ["drafts/", "wip/"]` |
| 锁定到发布版本 | `commit: <release-sha>` |
| 跟踪功能分支 | `branch: feature/new-docs` |
| 同步所有内容（默认） | 所有字段留空 |

---

## 相关文档

- [配置文件管理](../guides/Profiles.zh.md) — 管理 YAML 配置文件
- [多仓库管理](../features/Multi-Repo.zh.md) — 使用多个仓库
- [首次配置](../getting-started/First%20Setup.zh.md) — 添加第一个仓库
