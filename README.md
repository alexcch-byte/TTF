# Traditional Tang Soo Do — Student Manual

A complete, single-page reference manual for **Traditional Tang Soo Do Moo Duk Kwan**
students, covering the art's history, curriculum, terminology, techniques, sparring,
forms, and bunkai.

🥋 **Live site:** https://alexcch-byte.github.io/TTF/

## Sections

- **Origins & Philosophy** — history of the art, the Eight Key Concepts, the Ten
  Articles of Faith, notable practitioners, and a development-balance chart.
- **Curriculum & Rank** — belt progression (Gup to Dan), forms rotation, breaking
  requirements, and flying-kick syllabus.
- **Terminology Dictionary** — searchable Korean ↔ English glossary across stances,
  hand/leg techniques, commands, anatomy, and more, with pronunciation audio.
- **Techniques & Visuals** — illustrated stances and punches, kicking and advanced
  hand/foot combinations, plus stretching & flexibility for kicks.
- **Sparring & Self-Defence** — one-step sparring (Il Soo Sik) and Ho Sin Sool
  self-defence grabs by rotation.
- **Free Sparring & Matches** — free-sparring levels, tournament scoring, rules,
  equipment, etiquette, sparring tips, and reference match footage.
- **Forms (Hyung) Library** — demonstration videos for each required form.
- **Bunkai (Applications)** — curated videos breaking down the practical applications of
  the hyung (Pyung Ahn / Pinan, Bassai / Passai, Naihanchi / Tekki).
- **Britannia Karate** — the host school: location, class schedule, and instructor team.

## Viewing locally

No build step or dependencies. Just open the file in a browser:

```
index.html
```

Everything (markup, styles, data, and logic) lives in `index.html`. Styling uses Tailwind
CSS (with a midnight-blue / maroon / gold theme set via the Tailwind config), charts use
Chart.js, and fonts use Inter — all loaded from CDN, so an internet connection is required
for full rendering.

## Project structure

| File | Purpose |
|------|---------|
| `index.html` | The entire website — the only file you need to edit. |
| `a6dd21_71ed77483b6f4be7b7faf1ac57663145.gif` | Logo (referenced by relative path). |
| `traditional_tang_soo_do (1).html` | Original/legacy copy, not served. |
| `CLAUDE.md` | Guidance for the Claude Code assistant. |

## Deploying

The site is hosted on **GitHub Pages** from the `main` branch (root folder). Pushing to
`main` rebuilds and publishes automatically:

```bash
git add index.html
git commit -m "Describe your change"
git push origin main
```

Build status is visible under the repository's **Actions** tab.

## Disclaimer

This manual is a study aid and supplement to instruction — **not a replacement for
training under a qualified instructor**. Sparring rules, scoring, and grading requirements
vary between federations; always follow your own organisation's official syllabus and your
instructor's guidance. Free sparring must only be practised under supervision with proper
protective equipment.
