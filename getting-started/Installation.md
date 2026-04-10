[中文](./Installation.zh.md) | **English**

# Installation

Gleaner is a pure frontend SPA with no backend server required. You can run it locally for development or deploy it to any static hosting service.

## Prerequisites

- [Node.js](https://nodejs.org/) v18 or later
- [pnpm](https://pnpm.io/) v8 or later

## Local Development

```bash
# Clone the repository
git clone https://github.com/ChenNima/Gleaner.git
cd Gleaner

# Install dependencies
pnpm install

# Start development server with HMR
pnpm run dev
```

The dev server starts at `http://localhost:5173`. Changes to source files are reflected instantly via hot module replacement.

## Production Build

```bash
# Type-check and build for production
pnpm run build
```

The output is written to the `dist/` directory. This folder contains only static files (HTML, JS, CSS) and can be served by any web server.

## Deployment Options

### GitHub Pages

1. Build the project with `pnpm run build`
2. Push the `dist/` folder to a `gh-pages` branch, or configure GitHub Actions to build and deploy automatically
3. Enable GitHub Pages in repository settings, pointing to the correct branch

### Vercel

1. Import the repository on [Vercel](https://vercel.com/)
2. Set the build command to `pnpm run build` and the output directory to `dist`
3. Vercel automatically handles SPA routing

### Netlify

1. Import the repository on [Netlify](https://www.netlify.com/)
2. Set the build command to `pnpm run build` and the publish directory to `dist`
3. Add a `_redirects` file in the `public/` folder with:
   ```
   /*    /index.html   200
   ```

### Nginx

Serve the `dist/` folder and configure a fallback for SPA routing:

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

## SPA Routing Fallback

Gleaner uses client-side routing. If you deploy to a static server, you **must** configure a fallback so that all routes serve `index.html`. Without this, refreshing or directly navigating to a URL like `/file/some-doc` will return a 404.

The examples above show how to configure this for each platform.

---

## What's Next

- Follow the [Quick Start](./Quick%20Start.md) to add your first repository
- Configure a [GitHub Token](../advanced/GitHub%20Token.md) for higher API rate limits
