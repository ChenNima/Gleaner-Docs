**中文** | [English](./Installation.md)

# 安装与部署

Gleaner 是一个纯前端 SPA 应用，无需后端服务器。你可以在本地运行用于开发，也可以部署到任何静态托管服务。

## 前置条件

- [Node.js](https://nodejs.org/) v18 或更高版本
- [pnpm](https://pnpm.io/) v8 或更高版本

## 本地开发

```bash
# 克隆仓库
git clone https://github.com/ChenNima/Gleaner.git
cd Gleaner

# 安装依赖
pnpm install

# 启动开发服务器（支持热更新）
pnpm run dev
```

开发服务器会在 `http://localhost:5173` 启动。源文件的修改会通过热模块替换即时生效。

## 生产构建

```bash
# 类型检查并构建生产版本
pnpm run build
```

构建产物会输出到 `dist/` 目录。这个文件夹只包含静态文件（HTML、JS、CSS），可以由任何 Web 服务器托管。

## 部署方式

### GitHub Pages

1. 使用 `pnpm run build` 构建项目
2. 将 `dist/` 文件夹推送到 `gh-pages` 分支，或配置 GitHub Actions 自动构建和部署
3. 在仓库设置中启用 GitHub Pages，指向正确的分支

### Vercel

1. 在 [Vercel](https://vercel.com/) 上导入仓库
2. 设置构建命令为 `pnpm run build`，输出目录为 `dist`
3. Vercel 会自动处理 SPA 路由

### Netlify

1. 在 [Netlify](https://www.netlify.com/) 上导入仓库
2. 设置构建命令为 `pnpm run build`，发布目录为 `dist`
3. 在 `public/` 文件夹中添加 `_redirects` 文件：
   ```
   /*    /index.html   200
   ```

### Nginx

托管 `dist/` 文件夹，并为 SPA 路由配置回退规则：

```nginx
server {
    listen 80;
    root /path/to/dist;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

## SPA 路由回退

Gleaner 使用客户端路由。如果你部署到静态服务器，**必须**配置回退规则，使所有路由都返回 `index.html`。否则，刷新页面或直接访问 `/file/some-doc` 等 URL 时会返回 404。

以上示例展示了各平台的配置方法。

---

## 接下来

- 参照 [快速开始](./Quick%20Start.zh.md) 添加你的第一个仓库
- 配置 [GitHub Token](../advanced/GitHub%20Token.zh.md) 以获得更高的 API 限额
