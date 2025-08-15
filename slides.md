---
marp: true
size: 16:9
math: katex
paginate: true
color: #0f172a
backgroundColor: #ffffff
keywords: [documentation, marp, technical-writing, version-control]
title: Product Documentation Presentation
description: Maintainable, version-controlled presentation for product documentation using Marp
author: 24f1001136@ds.study.iitm.ac.in
---

<style>
/* @theme techwriter */
:root {
  --brand: #2563eb; /* blue-600 */
  --ink: #0f172a;   /* slate-900 */
  --muted: #475569; /* slate-600 */
  --surface: #ffffff;
  --code-bg: #0b1020;
  --code-fg: #e5e7eb;
}

section {
  font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, "Apple Color Emoji", "Segoe UI Emoji";
  color: var(--ink);
}

section.lead h1, section.lead h2, section.lead p { color: #ffffff; text-shadow: 0 2px 16px rgba(0,0,0,.35); }

h1 { font-size: 2.2rem; letter-spacing: -0.02em; }
h2 { font-size: 1.6rem; letter-spacing: -0.01em; color: var(--brand); }
h3 { font-size: 1.25rem; color: var(--ink); }

ul { line-height: 1.5; }

code, pre code { font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace; }
pre {
  background: var(--code-bg);
  color: var(--code-fg);
  padding: 12px 16px;
  border-radius: 12px;
  box-shadow: 0 10px 20px rgba(2,6,23,.15);
}

/* Pagination (page numbers) */
section::after {
  position: absolute;
  right: 24px;
  bottom: 20px;
  font-size: 12px;
  color: var(--muted);
  content: attr(data-marpit-pagination) " / " attr(data-marpit-pagination-total);
}

/* Utility: two-column layout */
section.two-cols {
  display: grid;
  grid-template-columns: 1.1fr 0.9fr;
  gap: 28px;
  align-items: start;
}

/* Accent callout */
.callout {
  border-left: 6px solid var(--brand);
  padding: 10px 14px;
  background: #eff6ff; /* blue-50 */
  border-radius: 10px;
}

/* Tiny footer note */
footer { color: var(--muted); font-size: 0.8rem; }
</style>

<!--
theme: techwriter
_class: lead
_backgroundImage: url('images/hero.jpg')
_backgroundPosition: 50% 50%
_backgroundSize: cover
-->
# Product Documentation Presentation

**Maintainable slides with Marp**  
24f1001136@ds.study.iitm.ac.in

<footer>Use with marp-cli: <code>marp slides.md --pdf --allow-local-files</code></footer>

---
<!-- _class: two-cols -->
## Why Marp for Product Docs?

- **Version-controlled**: Markdown sits happily in Git.
- **Portable**: Convert to **HTML**, **PDF**, or **PPTX** via marp-cli.
- **Themeable**: Custom brand look via CSS.
- **Automatable**: CI can render on every push.

<div class="callout">
<strong>Tip:</strong> Keep images in an <code>images/</code> folder and use relative paths. Enable <code>--allow-local-files</code> when exporting.
</div>

---
## Project Layout (recommended)

```
repo/
├─ slides.md            # ← this file
├─ images/
│  └─ hero.jpg          # background image used in title slide
├─ .github/workflows/
│  └─ build-slides.yml  # CI to render HTML/PDF
└─ package.json         # marp-cli as a devDependency (optional)
```

---
## Custom Theme & Directives

- Front-matter enables features:
  - `marp: true`, `math: katex`, `paginate: true`, `size: 16:9`
  - `theme: techwriter` (defined inline via CSS `/* @theme techwriter */`)
- Per-slide directives:
  - `_class: lead | two-cols`
  - `_backgroundImage: url('images/hero.jpg')`
  - `_backgroundSize: cover`, `_backgroundPosition: 50% 50%`

---
## Math (Algorithmic Complexity)

Using KaTeX for equations:

Inline: Sorting runs in $O(n \log n)$ for efficient algorithms.

Block:
$$
T(n) = a\,T\!\left(\frac{n}{b}\right) + f(n) \quad \Rightarrow \quad
T(n) =
\begin{cases}
\Theta\!\left(n^{\log_b a}\right) & \text{if } f(n) = O\!\left(n^{\log_b a - \epsilon}\right) \\
\Theta\!\left(n^{\log_b a} \log n\right) & \text{if } f(n) = \Theta\!\left(n^{\log_b a}\right) \\
\Theta\!\left(f(n)\right) & \text{if } f(n) = \Omega\!\left(n^{\log_b a + \epsilon}\right)
\end{cases}
$$

---
## Code Snippet Example

```bash
# Export to HTML and PDF
npx @marp-team/marp-cli slides.md \
  --html --pdf \
  --allow-local-files \
  --theme-set ./themes/*.css
```

```yaml
# .github/workflows/build-slides.yml
name: build-slides
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm i -D @marp-team/marp-cli
      - run: npx marp slides.md --html --pdf --allow-local-files
      - uses: actions/upload-artifact@v4
        with:
          name: slides
          path: "*.{html,pdf}"
```

---
## Branding & Styling

- **Colors & typography** centralized in the theme (CSS variables)  
- **Code blocks** styled for readability  
- **Pagination** (page numbers) shown via CSS pseudo-element  

> Update the theme palette by editing the `:root` variables.

---
## Contact

Questions or PRs welcome!  
**Email:** 24f1001136@ds.study.iitm.ac.in

<footer>© 2025 Your Company — Docs built with Marp</footer>
