# CLAUDE.md

Guidance for Claude Code when working in this repository.

## Project

A single-page **Traditional Tang Soo Do** student manual — a self-contained reference
website covering the art's origins, curriculum/rank structure, terminology, techniques,
sparring, and forms. Published via GitHub Pages.

- **Repo:** https://github.com/alexcch-byte/TTF
- **Live site:** https://alexcch-byte.github.io/TTF/ (GitHub Pages, `main` branch, root)

## Structure

- `index.html` — **the entire site.** All markup, styles, data, and logic live in this one
  file. This is what GitHub Pages serves and the only file to edit for site changes.
- `a6dd21_71ed77483b6f4be7b7faf1ac57663145.gif` — logo, referenced by relative path in
  `index.html`. Must stay in the repo root or the logo breaks.
- `traditional_tang_soo_do (1).html` — original/legacy copy, not served. Leave untouched
  unless asked.

## Architecture (inside index.html)

A no-build, CDN-only SPA. No package manager, no bundler, no local dev server needed —
open the file in a browser to preview.

- **Tailwind CSS** via CDN (`cdn.tailwindcss.com`) for styling.
- **Chart.js** via CDN, lazy-loaded, for the radar chart on the Origins section.
- **Inter** font via Google Fonts.
- Content sections are sibling `<section id="sec-NAME">` blocks; only one is visible at a
  time. The sidebar `[data-nav]` buttons drive `nav(target)` which toggles `hidden`/`block`.
- The `sections` array (in the `<script>`) is the source of truth for which sections exist —
  **any new section's id suffix must be added there** or navigation won't work.
- Data-driven blocks render from JS arrays: `dictionary` (terminology table),
  `hyungList` (forms video cards), `matchList` (sparring match video cards). Their
  `populate*()` functions run on `DOMContentLoaded`.
- Stance/punch diagrams are drawn on `<canvas>` elements via the `draw*` functions,
  rendered lazily the first time the Techniques section is opened.

### Adding a new section

1. Add a sidebar `<li>` button with `data-nav="NAME"` and `id="nav-NAME"`.
2. Add a `<section id="sec-NAME" class="... hidden">`.
3. Add `'NAME'` to the `sections` array in the `<script>`.
4. If it renders from data, add a `populate*()` and call it in the `DOMContentLoaded` handler.

### YouTube videos

Video cards (forms, sparring matches) link to YouTube **search** URLs
(`youtube.com/results?search_query=...`), not embedded/hard-coded video IDs. This keeps
links from going dead. Follow this pattern unless the user supplies specific video URLs.

## Deploying

Changes go live by committing to `main` and pushing — GitHub Pages rebuilds automatically.

```
git add index.html
git commit -m "..."
git push origin main
```

Then check the repo's **Actions** tab for the "pages build and deployment" run.

**Do not** commit nested folders as git submodules — a stray `TTF` gitlink (mode 160000)
previously broke the Pages build with `No url found for submodule path 'TTF'`. Keep all
site files as normal tracked files in the repo root.

## Notes

- Sparring rules, scoring, and belt requirements vary by federation. Content is framed as
  "typical"/general where appropriate. If the user provides the Traditional Tang Soo Do
  Federation's official ruleset, make the relevant tables exact.
- Keep everything in `index.html` — do not introduce a build step or split into multiple
  files unless the user explicitly asks.
