**中文** | [English](./Mermaid.md)

# Mermaid 图表

Gleaner 支持渲染 [Mermaid](https://mermaid.js.org/) 代码块为图表，与 Obsidian 和 GitHub 的行为一致。图表会自动跟随深色/浅色主题切换。

## 流程图

```mermaid
flowchart LR
    A[Markdown 文件] --> B{包含 mermaid?}
    B -->|是| C[渲染 SVG]
    B -->|否| D[普通代码块]
    C --> E[显示图表]
```

## 时序图

```mermaid
sequenceDiagram
    participant 用户
    participant Gleaner
    participant GitHub

    用户->>Gleaner: 打开文件
    Gleaner->>GitHub: 获取内容
    GitHub-->>Gleaner: Markdown + mermaid
    Gleaner-->>用户: 渲染后的图表
```

## 类图

```mermaid
classDiagram
    class MdFile {
        +string path
        +string content
        +string repoFullName
    }
    class MermaidBlock {
        +string code
        +render()
    }
    class CodeBlock {
        +ReactNode children
        +detectLanguage()
    }
    CodeBlock --> MermaidBlock : 委托 mermaid
    MermaidBlock ..> MdFile : 读取自
```

## 状态图

```mermaid
stateDiagram-v2
    [*] --> 空闲
    空闲 --> 同步中 : 用户打开应用
    同步中 --> 已缓存 : 同步完成
    已缓存 --> 同步中 : 手动刷新
    同步中 --> 错误 : API 失败
    错误 --> 同步中 : 重试
```

## 甘特图

```mermaid
gantt
    title Gleaner 功能路线图
    dateFormat YYYY-MM-DD
    section 核心
        MVP 发布          :done, 2025-01-01, 2025-03-01
        双向链接           :done, 2025-03-01, 2025-04-01
    section 增强
        PWA 支持         :done, 2025-04-01, 2025-04-10
        Mermaid 图表     :active, 2025-04-10, 2025-04-15
        本地配置          :2025-04-15, 2025-05-01
```

## 饼图

```mermaid
pie title 知识库文件类型分布
    "Markdown" : 85
    "图片" : 10
    "配置" : 5
```

## 实体关系图

```mermaid
erDiagram
    REPO ||--o{ FILE : 包含
    FILE ||--o{ LINK : 拥有
    LINK }o--|| FILE : "指向"
    REPO {
        string fullName
        string treeSha
        string label
    }
    FILE {
        string path
        string content
        int repoId
    }
```

## 错误处理

当 mermaid 代码块包含无效语法时，Gleaner 会回退显示原始代码并附带错误提示：

```mermaid
这不是有效的 mermaid 语法
  --> 应该显示错误回退
```
