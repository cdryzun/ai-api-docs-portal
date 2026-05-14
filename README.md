# AI API Documentation Portal

A Stripe-inspired, production-grade API documentation portal built as a single self-contained HTML file. Zero external dependencies, zero build steps.

**Live Demo**: Deploy to Netlify or open `index.html` directly in a browser.

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

## Project Structure

```
ai-api-docs-portal/
├── index.html        # Complete single-page documentation portal
├── netlify.toml      # Netlify deployment config & security headers
├── README.md         # This file
├── CONTRIBUTING.md   # Contribution guidelines
├── CHANGELOG.md      # Version history
├── LICENSE           # MIT License
└── .gitignore        # Git ignore rules
```

---

## Quick Start

### Local Preview

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

### Deploy to Netlify

1. Fork or clone this repo
2. Log in to [Netlify](https://app.netlify.com/)
3. Click **"Add new site"** → **"Import an existing project"**
4. Select the GitHub repo
5. Build settings are auto-detected from `netlify.toml` — no configuration needed
6. Click **Deploy site**

Or use Netlify Drop for instant deployment: drag & drop the project folder at [app.netlify.com/drop](https://app.netlify.com/drop).

### Deploy to GitHub Pages

1. Go to **Settings → Pages** in your GitHub repo
2. Set source to `main` branch, root directory
3. Your site will be available at `https://<username>.github.io/ai-api-docs-portal/`

---

## Architecture

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

## Customization

### Change Accent Color

Edit the CSS custom property in `:root` and `[data-theme="dark"]`:

```css
:root {
  --accent: #635BFF;        /* Primary accent */
  --accent-hover: #5249e0;  /* Hover state */
  --accent-soft: rgba(99, 91, 255, 0.08);
  --accent-border: rgba(99, 91, 255, 0.25);
}
```

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

## Documentation Sections

The portal includes five major sections:

1. **Introduction** — Overview, base URLs, rate limits
2. **Authentication** — API keys, authorization header, organization scoping
3. **Chat Completions** — Create completion endpoint, streaming, message object
4. **Models** — List/retrieve models, capability matrix
5. **Error Handling** — Error format, status codes, retry strategy

Each section contains parameter tables with type annotations, required markers, and response documentation.

---

## Browser Support

- Chrome 80+
- Firefox 78+
- Safari 14+
- Edge 80+

Uses standard CSS custom properties, `scroll-behavior: smooth`, `backdrop-filter`, and `navigator.clipboard` API. Graceful degradation for older browsers.

---

## Security Headers

Configured in `netlify.toml`:

| Header | Value |
|---|---|
| `X-Frame-Options` | `DENY` |
| `X-XSS-Protection` | `1; mode=block` |
| `X-Content-Type-Options` | `nosniff` |
| `Referrer-Policy` | `strict-origin-when-cross-origin` |

---

## License

[MIT](./LICENSE) — free to use, modify, and distribute.
