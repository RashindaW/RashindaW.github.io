# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal academic portfolio website for Rashinda Wijethunga, deployed on GitHub Pages at `https://RashindaW.github.io`. Zero-build static site using vanilla HTML5, CSS3, and JavaScript — no frameworks, no package manager, no build tools.

## Development

**Local preview:** Open any `.html` file directly in a browser. No install or build step.

**Deployment:** Push to `main` branch; GitHub Pages serves automatically.

## Architecture

### Pages

All pages are standalone HTML files with duplicated navigation and footer (not templated — intentional for zero dependencies). When updating nav links or footer content, **every HTML file must be edited**.

- `index.html` — Homepage: profile section, stats strip, research interests, featured publications
- `about.html` — Full bio, education, skills, experience, awards
- `projects.html` — Project cards (2-col grid) with image carousels and filter tags
- `publications.html` — Publication entries with year badges, abstracts, BibTeX copy buttons, filter tags
- `blogs.html` — Blog index (some entries are "Coming Soon" placeholders)
- `blog-gnn-time-series.html` — Full blog post with MathJax equations, table of contents, code blocks
- `books.html` — Book summary cards
- `philosophy.html` — Research philosophy cards

### Styling

Single stylesheet: `assets/css/styles.css`. Uses CSS custom properties for theming.

- **Dark theme** is default (variables on `:root`)
- **Light theme** toggled via `.light-theme` class on `<html>` element (i.e., `document.documentElement`)
- **Responsive breakpoints:** 900px (multi-column → single column), 600px (tablet adjustments)

### JavaScript (inline in each HTML file)

- **Theme toggle:** `initTheme()` / `toggleTheme()` — persists preference in `localStorage` key `"theme"`
- **Carousel:** `initCarousel()` / `moveCarousel()` / `goToSlide()` — image galleries on projects page
- **Filter tags:** `data-filter` on buttons + `data-tags` on cards/entries — used on projects and publications pages
- **BibTeX copy:** `copyBibtex(id)` — copies citation text to clipboard on publications page
- **Footer year:** Dynamic `new Date().getFullYear()`

### External Dependencies (CDN only)

- **MathJax 3** (`cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js`) — LaTeX rendering in blog posts
- All icons are **inline SVGs** (no icon library)
- System font stack (no external fonts)

### Assets

- `assets/css/styles.css` — All styles
- `assets/img/` — Profile photo, project images, placeholders
- `assets/cv/Rashinda.pdf` — Downloadable CV (linked from nav)

### SEO & Metadata

Each page includes Open Graph tags, Twitter Card metadata, and JSON-LD structured data (Person schema on homepage, ScholarlyArticle on blog/publications). `sitemap.xml` must be updated manually when adding new pages.

## Key Patterns

- **Adding a project:** Duplicate an existing `.card` block in `projects.html`. For a carousel, use the existing markup pattern with a unique ID and call `initCarousel('id')`. Add the project's tags to `data-tags` and ensure matching `filter-tag` buttons exist.
- **Adding a publication:** Duplicate a `.pub-entry` block in `publications.html`. Set `data-tags` for filtering. Include a `<pre id="bib-...">` block for BibTeX.
- **Adding a blog post:** Create a new HTML file (copy nav/head/footer from an existing page). Use the `.blog-article` container and related classes (`.blog-callout`, `.blog-equation`, `.blog-code`, `.blog-figure`). Add a link in `blogs.html`.
- **Adding a new page:** Copy nav/head/footer from an existing file, then add a nav link to **all** pages. Update `sitemap.xml`.
- **CSS component classes:** `.card` (gradient-background card), `.badge`/`.tech-badge` (inline tags), `.btn` (gradient button), `.grid.g2`/`.grid.g3` (responsive grid), `.pub-entry` (publication card).
