# nstl-slides

Shared **Reveal.js** presentations—one folder per deck—so you can version, link, and host them together.

**GitHub:** intended remote is `git@github.com:migvanderlei/nstl-slides.git` (SSH user was detected from your GitHub login). The remote `origin` is already set in this clone. Create the empty repository on GitHub (no README, no license, no `.gitignore`), then run:

```bash
git push -u origin main
```

Or, after a one-time `gh auth login` (GitHub CLI is installed at `~/.local/bin/gh`):

```bash
export PATH="$HOME/.local/bin:$PATH"
gh repo create nstl-slides --public
git push -u origin main
```

`origin` is already `git@github.com:migvanderlei/nstl-slides.git`.

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
