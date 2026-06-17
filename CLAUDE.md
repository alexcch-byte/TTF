# CLAUDE.md

Guidance for Claude Code when working in this repository.

## Project

A single-page **Traditional Tang Soo Do** student manual — a self-contained reference
website covering the art's origins, curriculum/rank structure, terminology, techniques,
sparring (one-step, self-defence and free sparring), forms, bunkai (form applications),
and the host school (Britannia Karate, Calgary). Published via GitHub Pages.

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
  **any new section's id suffix must be added there** or navigation won't work. Current value:
  `['origins', 'curriculum', 'terminology', 'techniques', 'sparring', 'freesparring', 'forms', 'bunkai', 'school']`.
- Data-driven blocks render from JS arrays: `dictionary` (terminology table),
  `hyungList` (forms video cards), `matchList` (sparring match video cards), and
  `bunkaiList` (bunkai video cards). Their `populate*()` functions
  (`populateTerms`, `populateForms`, `populateMatches`, `populateBunkai`) run on
  `DOMContentLoaded`. The Britannia Karate section (`sec-school`) is static markup, not
  data-driven.
- Stance/punch diagrams are drawn on `<canvas>` elements via the `draw*` functions,
  rendered lazily the first time the Techniques section is opened.

### Theme / colors

The palette is **midnight blue + maroon + antique gold**, implemented by a `tailwind.config`
script placed immediately after the Tailwind CDN `<script>`. It remaps the Tailwind shades
the markup already uses: `blue-*` → midnight blue, `amber-*` → gold, `red-*` → maroon. To
recolor the site, edit those ramps in the config rather than rewriting classes. A few raw
colors live outside Tailwind and must be changed directly: the `.nav-active` and scrollbar
rules in the `<style>` block, and the radar chart's inline `rgba(...)` slice colors in
`renderChart()`. One literal colour is pinned: the "Red Belt" form swatch in `hyungList`
uses `bg-[#dc2626]` so it stays red despite the red→maroon remap.

### Adding a new section

1. Add a sidebar `<li>` button with `data-nav="NAME"` and `id="nav-NAME"`.
2. Add a `<section id="sec-NAME" class="... hidden">`.
3. Add `'NAME'` to the `sections` array in the `<script>`.
4. If it renders from data, add a `populate*()` and call it in the `DOMContentLoaded` handler.

### YouTube videos

Forms (`hyungList`) and sparring-match (`matchList`) cards link to YouTube **search** URLs
(`youtube.com/results?search_query=...`), not embedded/hard-coded video IDs. This keeps
links from going dead. Follow this pattern by default.

**Exception:** the Bunkai section (`bunkaiList`) links to **specific** curated videos
(`youtube.com/watch?v=...` in a `url` field) from established channels (Iain Abernethy,
Jesse Enkamp, Naka Shihan / Tatsuya Naka), because the user asked for particular videos.
Direct links can eventually rot — if one breaks, swap it for another verified video or a
search-link card.

### Terminology audio

Pronunciation audio (🔊 buttons) is **hot-linked** from `tangsoodoworld.com`
(`audioBase` in the script) — not hosted in this repo, so playback depends on their server.
A credit line at the end of the Terminology section attributes it; keep that citation if
the audio stays.

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
- The Britannia Karate section's **class schedule** and **instructor team** are scraped from
  `britanniakarate.com` and can go stale. A durable scheduled task,
  `refresh-britannia-schedule` (monthly), re-fetches `britanniakarate.com/schedule` and
  updates the Class Schedule table in `sec-school` only if it changed. The team list is not
  auto-refreshed.
- Branding note: the repo/CLAUDE history references both the **Traditional Tang Soo Do
  Federation** and **Britannia Karate** (the host school). If the user clarifies one is
  authoritative, reconcile the wording across the site.
