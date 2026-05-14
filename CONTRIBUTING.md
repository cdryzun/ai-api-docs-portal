# Contributing to AI API Docs Portal

Thank you for your interest in contributing! This document outlines the process and conventions.

---

## How to Contribute

### Report Issues

- Open a [GitHub Issue](https://github.com/cdryzun/ai-api-docs-portal/issues/new)
- Include browser version, screen size, and steps to reproduce

### Submit Changes

1. **Fork** the repository
2. **Create a branch**: `git checkout -b feat/your-feature-name`
3. **Make changes** — edit `index.html` (the single source file)
4. **Test locally**: open `index.html` in a browser, check both themes and all breakpoints
5. **Commit**: use [Conventional Commits](https://www.conventionalcommits.org/) format
   ```
   feat: add embeddings API section
   fix: code panel scroll sync on Safari
   docs: update customization guide
   ```
6. **Push** and open a Pull Request

---

## Design Conventions

### CSS

- All styles inlined in `<style>` — no external stylesheets
- Use CSS custom properties (`--var-name`) for any color, spacing, or shadow value
- Follow the existing section comment format: `/* ====== SECTION ====== */`
- Border-radius: 4px (tight) → 8px (large) — never pill-shaped

### JavaScript

- All scripts inlined in `<script>` — no external JS
- Use `const` / `let` (no `var`)
- DOM queries cached at the top of each logical block
- Event listeners use named functions for readability

### HTML Structure

- Semantic elements: `<header>`, `<main>`, `<section>`, `<aside>`, `<nav>`
- API endpoints use `.endpoint` wrapper with `.endpoint-header`, `.params-table-wrap`, `.response-block`
- Code blocks use `.code-block-wrapper[data-code="key"]` for scroll sync mapping

---

## Adding Content

### New API Section

1. Add a `<section class="section" id="section-id">` block in `<main>`
2. Add corresponding `.code-block-wrapper[data-code="section-id"]` in the code panel `<aside>`
3. Add navigation link in sidebar
4. Update the `codeMap` JS object for scroll synchronization
5. If mobile code inline needed, add `<div class="mobile-code" data-endpoint="section-id"></div>`

### New Language Tab

1. Add `<button class="lang-tab" data-lang="lang">Label</button>`
2. Add `<pre><code class="code-content hidden" data-lang="lang">...</code></pre>`
3. Implement `highlightLang()` function
4. Wire into `highlightElement()` switch statement

---

## Testing Checklist

Before submitting a PR, verify:

- [ ] Both dark and light themes render correctly
- [ ] Theme toggle persists after page reload
- [ ] All sidebar navigation links scroll to correct sections
- [ ] Active nav link updates on scroll
- [ ] Code language tabs switch correctly
- [ ] Copy button works and shows feedback
- [ ] Syntax highlighting applies to all visible code
- [ ] Responsive layout works at: 1440px, 1024px, 768px, 375px
- [ ] Mobile sidebar drawer opens/closes
- [ ] Mobile code blocks render inline
- [ ] No console errors in Chrome, Firefox, Safari

---

## Commit Message Format

Follow [Conventional Commits](https://www.conventionalcommits.org/):

| Type | Usage |
|---|---|
| `feat:` | New feature or section |
| `fix:` | Bug fix |
| `docs:` | Documentation changes |
| `style:` | CSS/visual adjustments |
| `refactor:` | Code restructuring without behavior change |
| `chore:` | Build, config, or tooling changes |

---

## Code of Conduct

Be respectful, constructive, and inclusive. We're all here to make great documentation.
