**中文** | [English](./Wikilink%20Syntax.md)

# Wikilink 语法参考

本页面记录了所有支持的 `[[wikilink]]` 语法，并使用真实的 wikilinks 来演示每个功能。

## 基本链接

- [[双向链接]] — 通过 frontmatter 标题匹配
- [[Search]] — 通过文件名匹配
- [[Knowledge Graph]] — 带空格的文件名

## 带 .md 扩展名

以下链接应与不带 `.md` 的效果相同：

- [[Backlinks.md]] — 带 .md 后缀
- [[Search.md]] — 带 .md 后缀
- [[Knowledge Graph.md]] — 带 .md 和空格

## 别名链接

- [[Backlinks|了解双向链接]] — 自定义显示文本
- [[Search|全文搜索功能]] — 自定义显示文本

## 基于路径的链接

- [[features/Backlinks]] — 部分路径匹配
- [[getting-started/Quick Start]] — 跨文件夹路径匹配

## 标题锚点

- [[Backlinks#Wikilink Syntax]] — 跳转到其他文件的指定标题
- [[Backlinks#Link Resolution Rules]] — 跳转到另一个标题
- [[Search#Search Tips]] — Search 页面中的标题

## 当前文件内锚点

- [[#基本链接]] — 跳转到上方标题
- [[#带 .md 扩展名]] — 跳转到另一个章节
- [[#标题锚点]] — 跳转到标题锚点章节

## 组合：标题 + 别名

- [[Backlinks#Wikilink Syntax|Wikilink 语法详情]] — 文件 + 标题 + 别名
- [[Search#Search Tips|如何搜索]] — 另一个组合示例

## 跨仓库链接

当同步了多个仓库时，wikilinks 会跨仓库解析：

- 同仓库匹配优先
- 当前仓库无匹配时，搜索其他已同步的仓库

## 未解析链接

- [[不存在的页面]] — 应显示为未解析样式（虚线下划线）
- [[同样不存在|失效链接]] — 带别名的未解析链接

## 边缘情况

- [[README]] — 匹配仓库根目录的 README.md
- [[Backlinks.MD]] — 大小写不敏感的 .md 扩展名
