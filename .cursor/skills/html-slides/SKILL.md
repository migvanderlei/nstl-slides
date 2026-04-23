---
name: html-slides
description: Builds self-contained HTML presentation decks with Reveal.js (sections, themes, code highlighting, speaker notes, PDF export). Use when creating slides, decks, talks, Reveal.js presentations, HTML exports from Markdown, or speaker-note layouts.
---

# HTML slides

## Default approach

Use **Reveal.js 5** loaded from a CDN (jsDelivr). Ship a single `index.html` per deck.

## File layout

**Multi-deck shared repo** (this project’s convention):

```
decks/<slug>/index.html   # one folder per talk or version
decks/<slug>/assets/      # optional images and local files
decks/_template/          # copy to start a new deck; do not edit in place for real talks
```

**Single-deck repo** (elsewhere):

```
index.html
assets/                   # optional
```

Avoid npm unless the user already uses a bundler in the project.

**Highlight plugin:** load `highlight.min.js` (hljs) **before** Reveal’s `plugin/highlight/highlight.js`.

## HTML skeleton

- Wrap all slides in:

```html
<div class="reveal">
  <div class="slides">
    <section>...</section>
  </div>
</div>
```

- One logical slide per `<section>`. Nested `<section>` elements create vertical stacks.
- Title slide first: event name, title, author, date.

## Scripts and plugins (CDN)

Typical head/body includes:

- `reveal.js` CSS: `dist/reveal.css` + one theme from `dist/theme/`
- `reveal.js` JS: `dist/reveal.js`
- Plugins as needed from `plugin/` (markdown, notes, highlight, math)

Initialize after DOM ready:

```javascript
Reveal.initialize({
  hash: true,
  slideNumber: true,
  plugins: [ RevealMarkdown, RevealHighlight, RevealNotes ]
});
```

Match plugin script tags to the `Reveal.*` symbols passed into `plugins`.

## Content rules

- Prefer **semantic headings** (`h1`–`h3`) inside sections for outline and accessibility.
- **Code**: `<pre><code class="language-ts">` and enable the Highlight plugin rather than pasting pre-styled spans.
- **Speaker notes**: separate `<aside class="notes">` inside the same `<section>`; open presenter mode with `s` when Notes plugin is loaded.
- **Images**: local paths under `assets/`; set explicit `width` or constrain with CSS so layouts do not jump between slides.
- **Fragments**: use `class="fragment"` for incremental reveals; avoid abusing animations for essential information.

## Styling

- Start from a built-in Reveal theme; add a short `<style>` block only for accents, logos, or typography tweaks.
- Keep contrast high; assume both projector and laptop viewing.

## Markdown option

If the user supplies Markdown, either:

1. Embed it in a `<section data-markdown>` with a `<textarea data-template>` pattern and the Markdown plugin, or  
2. Convert to HTML sections in-repo when a build step already exists.

Do not introduce a build tool solely for Markdown unless requested.

## Quality checklist

- [ ] Deck opens locally via `file://` or a static server without errors
- [ ] Arrow keys and overview (`Esc`) work
- [ ] Title and major sections have clear headings
- [ ] Code blocks specify a language for highlighting
- [ ] Notes (if used) are in `<aside class="notes">`

## When not to use Reveal

If the user forbids external scripts, needs a trivial handout, or wants a single scrolling page, use the **vanilla full-page sections** pattern in [reference.md](reference.md).

## Additional resources

- Reveal options, math, and PDF export: [reference.md](reference.md)
