# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.0.0] - 2025-05-14

### Added

- Single-file AI API documentation portal (`index.html`)
- Three-column layout: collapsible sidebar, main content, code panel
- Five documentation sections: Introduction, Authentication, Chat Completions, Models, Error Handling
- Dark/light theme toggle with `localStorage` persistence
- Stripe-inspired design system (purple accent `#635BFF`, blue-tinted shadows, conservative radii)
- Multi-language code tabs: Python, JavaScript, cURL
- Regex-based syntax highlighting (JSON, Python, JavaScript, Bash)
- One-click copy button with visual feedback
- Smooth scroll navigation with active link tracking
- Responsive design: code panel collapses at ≤1024px, sidebar drawer at ≤768px
- API endpoint blocks with HTTP method badges, parameter tables, response documentation
- Info boxes: info, success, warn, error variants
- Netlify deployment configuration (`netlify.toml`) with security headers
