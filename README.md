# AI API Documentation Portal

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](./CONTRIBUTING.md)
[![Zero Dependencies](https://img.shields.io/badge/dependencies-zero-orange.svg)]()
[![Built with WorkBuddy](https://img.shields.io/badge/Built%20with-WorkBuddy-635BFF.svg)](https://github.com/cdryzun/ai-api-docs-portal)

A Stripe-inspired, production-grade API documentation portal built as a single self-contained HTML file. Zero external dependencies, zero build steps.

> 🤖 本项目由 [WorkBuddy](https://workbuddy.ai) AI 搭档协作完成，从页面设计、代码生成到文档编写与部署，全程人机协作。

**仓库**: [github.com/cdryzun/ai-api-docs-portal](https://github.com/cdryzun/ai-api-docs-portal)

**在线预览**: [www.treesir.pub/ai-api-docs-portal/](http://www.treesir.pub/ai-api-docs-portal/)

---

## 简介

这是一个面向 AI 服务的 API 文档门户页面，采用 Stripe 官方文档的设计风格，以单文件 HTML 实现，无需任何构建工具或外部依赖。

核心特点：

- **三栏布局** — 左侧可折叠导航菜单、中间文档内容区、右侧代码示例区
- **深色/浅色主题** — 默认深色，一键切换，选择自动持久化
- **多语言代码示例** — 支持 Python / JavaScript / cURL Tab 切换，内置语法高亮与一键复制
- **响应式设计** — 小屏自动适配，代码区折叠到内容下方
- **零依赖** — 所有 CSS 和 JS 内联，不依赖任何 CDN 或外部资源

---

## Features

| Feature | Details |
|---|---|
| **Three-column layout** | Collapsible sidebar navigation + main documentation + code examples panel |
| **Dark / Light theme** | Toggle with persistence via `localStorage`; defaults to dark |
| **Stripe design language** | Purple accent `#635BFF`, blue-tinted shadows, conservative border-radius |
| **Multi-language code tabs** | Python · JavaScript · cURL — with syntax highlighting and one-click copy |
| **Responsive design** | Code panel collapses below content at ≤1024px; sidebar becomes a drawer at ≤768px |
| **Smooth scroll navigation** | Click sidebar links to scroll to sections; active link tracking on scroll |
| **Zero dependencies** | No CDN, no build tooling, no external fonts — all CSS/JS inlined |

---

## Project Structure / 项目结构

```
ai-api-docs-portal/
├── index.html                    # 完整的单页面文档门户
├── netlify.toml                  # Netlify 部署配置 & 安全响应头
├── .github/workflows/deploy.yml  # GitHub Pages 自动部署工作流
├── README.md                     # 本文件
├── CONTRIBUTING.md               # 贡献指南
├── CHANGELOG.md                  # 版本更新日志
├── LICENSE                       # MIT 开源协议
└── .gitignore                    # Git 忽略规则
```

---

## Quick Start / 快速开始

### Local Preview / 本地预览

No build step required — just open the file:

```bash
# macOS
open index.html

# Linux
xdg-open index.html

# Or use a local server for better scroll behavior
python3 -m http.server 8080
# Then visit http://localhost:8080
```

### Deploy to Netlify / 部署到 Netlify

1. Fork or clone this repo
2. Log in to [Netlify](https://app.netlify.com/)
3. Click **"Add new site"** → **"Import an existing project"**
4. Select the GitHub repo
5. Build settings are auto-detected from `netlify.toml` — no configuration needed
6. Click **Deploy site**

Or use Netlify Drop for instant deployment: drag & drop the project folder at [app.netlify.com/drop](https://app.netlify.com/drop).

### Deploy to GitHub Pages / 部署到 GitHub Pages

1. Go to **Settings → Pages** in your GitHub repo
2. Set source to `main` branch, root directory
3. Your site will be available at `https://<username>.github.io/ai-api-docs-portal/`

---

## Architecture / 技术架构

### Design System

The visual design follows the [Stripe design system](https://stripe.com/docs), incorporating:

- **Color system**: CSS custom properties for light/dark themes, toggled via `data-theme` attribute
- **Typography**: System font stack (`-apple-system`, `Segoe UI`, etc.) for body; monospace stack for code
- **Shadows**: Multi-layer, blue-tinted shadows (`rgba(50,50,93,…)`) — Stripe's signature elevation style
- **Border radius**: Conservative 4px–8px range
- **Spacing**: 8px base unit

### Syntax Highlighting

Custom regex-based highlighter supporting four languages:

| Language | Function | Highlights |
|---|---|---|
| `json` | `highlightJSON()` | Keys, strings, numbers, booleans, null |
| `python` | `highlightPython()` | Keywords, functions, strings, comments, numbers |
| `javascript` | `highlightJavaScript()` | Keywords, classes, functions, strings, comments, numbers |
| `curl` | `highlightBash()` | Commands, flags, strings, comments, variables |

CSS classes: `.sh-keyword`, `.sh-string`, `.sh-number`, `.sh-comment`, `.sh-function`, `.sh-class`, `.sh-bool`, `.sh-null`, `.sh-operator`, `.sh-property`, `.sh-punctuation`

### Theme System

```css
/* Theme toggle mechanism */
html[data-theme="dark"]  { /* dark palette */ }
html[data-theme="light"] { /* light palette */ }
```

Persistence: `localStorage.setItem('docs-theme', 'dark'|'light')`

### Responsive Breakpoints

| Breakpoint | Behavior |
|---|---|
| >1024px | Full three-column layout |
| 768–1024px | Code panel hidden; inline code blocks appear in content area |
| <768px | Sidebar becomes slide-out drawer; hamburger menu appears |

---

## Customization / 自定义

### Change Accent Color

Edit the CSS custom property in `:root`:

```css
:root {
  --accent: #635BFF;        /* Primary accent */
  --accent-hover: #5249e0;  /* Hover state */
  --accent-soft: rgba(99, 91, 255, 0.08);
  --accent-border: rgba(99, 91, 255, 0.25);
}
```

> **Note:** The accent color is defined only in `:root` and shared across both themes. If you want different accent colors for dark/light, add overrides in the `[data-theme="dark"]` or `[data-theme="light"]` block.

### Add API Endpoints

1. Add a new `.endpoint` block in the main content `<main>` section
2. Add a corresponding `.code-block-wrapper` in the code panel `<aside>`
3. Add a nav link in the sidebar
4. Update the `codeMap` object in the JS section for scroll sync

### Add a New Language Tab

1. Add a `<button class="lang-tab" data-lang="go">Go</button>` in the `.lang-tabs`
2. Add a `<pre><code class="code-content hidden" data-lang="go">...</code></pre>` in the `.code-block`
3. Add a `highlightGo()` function and wire it into the `highlightElement()` switch

---

## Documentation Sections / 文档章节

The portal includes five major sections:

1. **Introduction** — Overview, base URLs, rate limits
2. **Authentication** — API keys, authorization header, organization scoping
3. **Chat Completions** — Create completion endpoint, streaming, message object
4. **Models** — List/retrieve models, capability matrix
5. **Error Handling** — Error format, status codes, retry strategy

Each section contains parameter tables with type annotations, required markers, and response documentation.

---

## Browser Support / 浏览器兼容

- Chrome 80+
- Firefox 78+
- Safari 14+
- Edge 80+

Uses standard CSS custom properties, `scroll-behavior: smooth`, `backdrop-filter`, and `navigator.clipboard` API. Graceful degradation for older browsers.

---

## Security Headers / 安全响应头

Configured in `netlify.toml`:

| Header | Value |
|---|---|
| `X-Frame-Options` | `DENY` |
| `X-XSS-Protection` | `1; mode=block` |
| `X-Content-Type-Options` | `nosniff` |
| `Referrer-Policy` | `strict-origin-when-cross-origin` |

---

## License / 开源协议

[MIT](./LICENSE) — 自由使用、修改和分发。

---

## Acknowledgements / 致谢

本项目由 [WorkBuddy](https://workbuddy.ai) AI 搭档「小悟」协作完成。设计参考 [Stripe 官方文档](https://stripe.com/docs)风格，通过 [awesome-design-md](https://github.com/anthropics/awesome-design-md) 的 Stripe DESIGN.md 规范指导实现。
