# HTML slides — reference

## Language

Default decks: `<html lang="pt-BR">` and Portuguese (Brazil) copy. Reveal’s UI chrome follows the library language; slide content is what you control.

## Reveal.js: useful `Reveal.initialize` options

```javascript
Reveal.initialize({
  hash: true,                 // deep links to slides
  slideNumber: 'c/t',         // current/total
  controls: true,
  progress: true,
  center: false,              // often better for dense tech slides
  transition: 'slide',        // none | fade | slide | convex | concave | zoom
  backgroundTransition: 'fade',
  width: 1280,
  height: 720,
  margin: 0.04,
  pdfSeparateFragments: false // set true if PDF should show each fragment as its own page
});
```

Enable **scroll view** only when the user explicitly wants scrollable slides instead of fullscreen stepping (`Reveal.initialize({ scrollActivationWidth: null })` — consult current Reveal docs for the exact option name in the version you pin).

## PDF export

Reveal’s PDF export relies on print CSS and a `?print-pdf` query parameter on the deck URL. Flow:

1. Add `print-pdf` class to `<html>` when `location.search` includes `print-pdf` (Reveal docs snippet).
2. Open the deck in Chrome/Chromium with the print dialog; choose “Save as PDF”.

Verify against the Reveal version’s official print instructions—details change slightly between minors.

## Math (KaTeX)

Load KaTeX CSS/JS before Reveal, then enable the Math plugin with `katex` configuration. Prefer KaTeX over MathJax for load time unless the user needs MathJax-specific features.

## Vanilla fallback (no Reveal)

Use one wrapper and full-viewport sections:

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Talk title</title>
  <style>
    html, body { height: 100%; margin: 0; }
    body { font-family: system-ui, sans-serif; }
    main { height: 100%; overflow-y: scroll; scroll-snap-type: y mandatory; }
    section.slide {
      min-height: 100vh; scroll-snap-align: start;
      box-sizing: border-box; padding: 6vh 8vw;
    }
    h1 { font-size: clamp(1.8rem, 4vw, 3rem); }
  </style>
</head>
<body>
  <main id="deck">
    <section class="slide"><h1>Title</h1><p>Subtitle</p></section>
    <section class="slide"><h2>Point</h2><ul><li>One</li></ul></section>
  </main>
  <script>
    const main = document.getElementById('deck');
    addEventListener('keydown', (e) => {
      if (e.key !== 'ArrowDown' && e.key !== 'ArrowUp' && e.key !== 'PageDown' && e.key !== 'PageUp') return;
      const slides = [...main.querySelectorAll('.slide')];
      const h = window.innerHeight;
      const i = Math.round(main.scrollTop / h);
      const j = e.key === 'ArrowDown' || e.key === 'PageDown' ? i + 1 : i - 1;
      slides[Math.max(0, Math.min(slides.length - 1, j))]?.scrollIntoView({ behavior: 'smooth' });
      e.preventDefault();
    });
  </script>
</body>
</html>
```

Extend with print CSS (`@media print { section.slide { min-height: auto; break-after: page; } }`) if they need PDF without Reveal.

## Version pinning

Pin CDN URLs to a specific Reveal **patch** version once the deck works, so future CDN updates do not break plugins.

## Theming (single `index.html`)

1. Pick a **Reveal built-in theme** CSS (`dist/theme/white.css`, `black.css`, `league.css`, …) closest to the user’s light/dark and mood.  
2. Add overrides **after** the theme link:

```html
<style>
  :root {
    --r-background-color: #0f1115;
    --r-main-color: #e8eaef;
    --r-heading-color: #7ee787;
    --r-link-color: #79c0ff;
    --r-heading-font: "DM Sans", system-ui, sans-serif;
    --r-main-font: "Source Sans 3", system-ui, sans-serif;
  }
  .reveal .slides section {
    text-align: left;
  }
</style>
```

Reveal 4/5 themes expose `--r-*` variables; tweak heading/body sizes in `.reveal h1, .reveal h2` if the user asked for dense or spacious layouts. Match **transitions** in `Reveal.initialize({ transition: 'fade' | 'slide' | … })` to the motion level they chose.

For **Google Fonts**, add a `<link href="https://fonts.googleapis.com/css2?family=…" rel="stylesheet">` before Reveal CSS, then reference the same family names in `--r-heading-font` / `--r-main-font`.

## Multi-deck repository (optional)

If several decks live in one repo (for example under `decks/<slug>/`), keep each deck self-contained: relative `assets/`, CDN scripts only, no shared `../` dependencies between decks unless the team explicitly maintains a common partial.
