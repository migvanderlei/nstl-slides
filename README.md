# Shared HTML slide decks

This repository holds separate **Reveal.js** presentations—one folder per deck—so you can version, link, and host them together.

## Layout

```
decks/
  _template/     # copy this folder to start a new talk
  <your-slug>/   # one directory per event or topic
    index.html
    assets/      # optional: images, diagrams, local files
```

Naming tips for `<your-slug>`: use lowercase, hyphens, and a date or venue if useful (for example `qcon-london-2026-04`).

## Viewing locally

From the repository root:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000/decks/<your-slug>/` in a browser (trailing slash avoids broken relative paths on some servers).

## Publishing (optional)

Any static host works (GitHub Pages, Netlify, Cloudflare Pages). Point the site root at this repository (or a `public/` copy) so each deck stays under `/decks/<slug>/`. Decks use CDN-hosted Reveal.js, so you only upload HTML and `assets/`.

## Cursor skill

Agent guidance for authoring these decks lives in `.cursor/skills/html-slides/`. Anyone cloning the repo gets the same conventions in Cursor.
