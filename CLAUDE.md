# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal academic portfolio website for Rashinda Wijethunga, deployed on GitHub Pages at `https://RashindaW.github.io`. This is a zero-build static site using vanilla HTML5, CSS3, and JavaScript — no frameworks, no package manager, no build tools.

## Development

**Local preview:** Open `index.html` directly in a browser. No install or build step required.

**Deployment:** Push to `main` branch; GitHub Pages serves automatically.

## Architecture

### Pages

All pages are standalone HTML files sharing a common navigation bar and footer (duplicated, not templated):

- `index.html` — Homepage with profile, research interests, education summary, featured publications
- `about.html` — Full bio, education, skills, publications, experience, awards
- `projects.html` — Project cards in a 2-column grid; includes image carousel component
- `blogs.html` — Placeholder (Coming Soon)
- `books.html` — Book summary cards
- `philosophy.html` — Research philosophy cards

### Styling

Single stylesheet at `assets/css/styles.css` using CSS custom properties for theming. Dark theme is the default; light theme overrides variables via a `.light` class on `<body>`. Responsive breakpoint at 900px collapses multi-column grids to single column.

### JavaScript (inline in each HTML file)

- **Theme toggle:** `initTheme()` / `toggleTheme()` persist light/dark preference in localStorage
- **Carousel:** `initCarousel()` / `moveCarousel()` / `goToSlide()` — used on projects page for image galleries
- **Footer year:** Dynamic `new Date().getFullYear()`

### Assets

- `assets/css/styles.css` — All styles
- `assets/img/` — Profile photo, project images, placeholders
- `assets/cv/Rashinda.pdf` — Downloadable CV (linked from nav on all pages)

## Key Patterns

- Navigation and footer markup is duplicated across all HTML files. When updating nav links or footer content, update every page.
- Theme toggle uses SVG icons inline in the HTML. The `.light` class on `<body>` triggers CSS variable overrides.
- Adding a new project: copy an existing `.card` block in `projects.html`. For a carousel, use the existing carousel markup pattern with unique IDs and call `initCarousel('id')`.
- Adding a new page: create a new HTML file copying the nav/head/footer from an existing page, then add a nav link to all pages.
