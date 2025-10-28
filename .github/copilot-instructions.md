## Purpose

This file gives concise, actionable guidance for an AI coding agent working on this repository. Focus on immediate, discoverable patterns so you can be productive without human hand-holding.

## Big picture (what this repo is)

- A single-page, static portfolio site: the main file is `indext.html` (note the filename — it is not `index.html`).
- No build system, frameworks, or server-side code present. The site uses plain HTML/CSS/vanilla JS and an image assets folder `images/`.

## Key components & where to look

- `indext.html` — entire app in one file: layout, CSS variables, responsive grid, lightbox script, and example tiles.
  - Gallery grid: the `<main id="gallery" class="grid">` contains `figure.tile` entries.
  - Tile attributes: each tile uses data attributes `data-name`, `data-label`, and `data-full` for the lightbox. Example: `figure.tile[data-full]`.
  - Lightbox: `<dialog id="lightbox">` plus inline script that opens images using `data-full` or falls back to the tile's `<img>` src.
  - CSS conventions: root variables (e.g., `--bg`, `--accent`), inline `style="aspect-ratio: ..."` on tiles for variety.

## Patterns & conventions to follow

- No external dependencies — keep changes dependency-free unless adding a clear reason and a lockfile.
- Maintain the single-file pattern for small UI tweaks (CSS/JS local to `indext.html`). If a feature grows, propose moving code into `assets/` or `src/` and document it.
- Image conventions: multiple formats (AVIF/WebP/JPG) and high-res versions use `@2x` suffix for `data-full` when present.
- Accessibility: keep `alt` text present on `<img>` and preserve `aria-*` attributes (e.g., `dialog[aria-label]`, social nav `aria-label`).

## Common edits an agent may be asked to perform

- Add a new gallery item: duplicate a `figure.tile`, update `data-name`, `data-label`, and `data-full`, and add AVIF/WebP/JPG sources in `images/`.
- Improve lightbox behavior: edit the small vanilla JS at the bottom of `indext.html` — it assumes `const tiles = Array.from(document.querySelectorAll('.tile'))` and uses `data-full` as primary source.
- Style tweaks: use the existing CSS variables in `:root`. Prefer adding rules near the top of the `<style>` block to keep styles centralized.

## Development & testing workflow

- There is no build step. To preview changes locally, open `indext.html` in a browser. For a simple local server (recommended for media loading), use a lightweight static server.
  - Suggested quick server (developer will run locally): e.g., Python's `http.server` or VS Code "Live Server" extension.
- No tests or linters are present; keep changes minimal and run manual browser checks (desktop/mobile/responsive breakpoints) when editing layout or JS.

## Integration points & risks

- Images are the main external dependency — check `images/` for missing files if a tile's `data-full` points to a non-existent file.
- The lightbox script relies on `dialog.showModal()` which is supported in modern browsers; consider a polyfill only if target audience requires legacy browsers.

## Examples (copyable patterns)

- New tile pattern (fill attributes and images):

  <figure class="tile" data-name="Title" data-label="Category" data-full="images/name@2x.jpg" style="aspect-ratio: 4/5">
    <picture>
      <source type="image/avif" srcset="images/name.avif" />
      <source type="image/webp" srcset="images/name.webp" />
      <img src="images/name.jpg" alt="Short description" loading="lazy" />
    </picture>
    <figcaption class="meta"><div class="label">Category</div><div class="name">Title</div></figcaption>
  </figure>

## When to ask the user (instead of guessing)

- Renaming `indext.html` to `index.html` — this is a repo-level decision that can affect hosting and should be confirmed.
- Adding a package manager, build step, or image-processing pipeline — ask before adding new tooling.

If anything above is unclear or you want different granularity (e.g., include exact server commands or propose a small refactor), tell me which areas to expand and I'll iterate.
