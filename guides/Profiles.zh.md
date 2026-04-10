**中文** | [English](./Profiles.md)

# 配置文件管理

Profile 允许你在 Gleaner 中维护多套配置，每套配置拥有独立的仓库集合和设置。

## Profile 类型

### 本地 Profile

- 配置完全存储在浏览器的 IndexedDB 中
- 通过设置界面添加和管理仓库
- 适合在单台设备上快速个人使用

### GitHub Profile

- 配置从 GitHub 仓库中的 `gleaner.yaml` 文件加载
- 以 `owner/repo` 格式指定配置仓库
- 适合跨设备或与他人共享配置
- GitHub 上 YAML 文件的修改会在下次同步时被读取

## 创建 Profile

1. 打开设置页面
2. 点击「新建 Profile」
3. 选择 Profile 类型（本地或 GitHub）
4. 输入名称
5. 对于 GitHub Profile，指定包含 `gleaner.yaml` 文件的配置仓库

## 切换 Profile

在设置页面的 Profile 下拉菜单中选择不同的 Profile。切换时：

1. 当前进行中的同步会被中止
2. 加载新 Profile 的配置
3. 之前已同步仓库的共享缓存（文件内容）会被保留
4. 自动开始同步新 Profile 的仓库

这意味着切换速度很快——在之前 Profile 下已同步的仓库不需要重新下载。

## 删除 Profile

在设置页面中点击 Profile 旁边的删除按钮。这只会移除 Profile 配置，不会删除已缓存的文件数据。引用相同仓库的其他 Profile 仍然可以访问缓存内容。

## YAML 配置格式

对于 GitHub Profile，`gleaner.yaml` 文件使用以下格式：

```yaml
repos:
  - repo: owner/repo-name
    label: 我的知识库
    branch: main
    includePaths:
      - docs/
      - notes/
    excludePaths:
      - docs/drafts/

  - repo: another-owner/another-repo
    label: 参考文档
```

除 `repo` 外所有字段均为可选。各字段的详细说明请参见 [仓库高级配置](../advanced/Repo%20Config.zh.md)。

## 导入与导出

Gleaner 支持多种方式传输 Profile 配置：

- **下载 YAML** — 将当前 Profile 的配置导出为 `.yaml` 文件
- **上传文件** — 从本地文件系统导入 `.yaml` 文件来创建或更新 Profile
- **从 GitHub 导入** — 指定一个包含 `gleaner.yaml` 的 GitHub 仓库，直接导入其配置

---

## 相关文档

- [首次配置](../getting-started/First%20Setup.zh.md) — 创建你的第一个 Profile
- [多仓库管理](../features/Multi-Repo.zh.md) — 在 Profile 中管理多个仓库
- [仓库高级配置](../advanced/Repo%20Config.zh.md) — 详细的仓库配置选项
