---
name: html-slides
description: Interviews the user on topic and goals, proposes a table of contents for approval, captures styling preferences, then produces a single standalone local HTML deck (Reveal.js) themed to match; slide copy defaults to Brazilian Portuguese (pt-BR). Use when creating slides, presentations, talks, pitch decks, lesson decks, or when the user wants structured slide authoring with outline approval.
---

# HTML slides

## Outcome

Deliver **one self-contained `index.html`** meant to open **directly in the browser** (`file://` is enough; do not require a local HTTP server). Use **Reveal.js 5** from a CDN (jsDelivr). No build step, no npm, unless the user already uses one.

Do **not** write the full deck until the **table of contents is approved** and **styling choices are captured**.

### Language

Unless the user explicitly asks for another language, write the **approved TOC, all slide titles and body copy, speaker notes, and UI labels you add** in **Brazilian Portuguese** (norma-padrão clara, natural no Brasil). Use `lang="pt-BR"` on `<html>`. Technical **identifiers, APIs, and code** stay as-is; short glosses next to them may be in Portuguese if helpful. If part of the deck must be English (quotes, compliance text), keep that block in English and note it briefly.

---

## Phase 1 — Interview (topic)

Conduct a short interview before proposing structure. Use chat; use **AskQuestion** when it is available for multiple-choice speedups.

Cover at least:

- Working title; subtitle or tagline; optional author / affiliation / date  
- **Audience** (who they are, prior knowledge, what they care about)  
- **Purpose** (inform, persuade, teach, status update, pitch, etc.)  
- **Length** (minutes or approximate slide count)  
- **Must-include** points, facts, examples, demos, or stories  
- **Out of scope** or sensitive topics to avoid  
- **Tone** (formal, conversational, bold, academic, …)  
- **Ending** (Q&amp;A, CTA, recap, next steps)  
- Whether they need **code samples**, **diagrams placeholders**, or **speaker notes**

Infer reasonable defaults only for minor details; ask when unsure.

---

## Phase 2 — Table of contents (proposal)

Draft a **numbered outline** of slides (not HTML yet). For each item include:

1. Slide title (as it will appear)  
2. One line: what that slide accomplishes  

Example shape:

```markdown
1. Title — hook + who this is for
2. Context — why this matters now
3. Problem — current pain (concise)
...
N. Summary + next steps
```

Present the TOC clearly and ask for **approval or edits**.

---

## Phase 3 — Approval gate

- If the user requests changes: **revise the TOC** and present again.  
- **Only after explicit approval** (“approved”, “looks good”, “proceed”, or they edit the TOC and confirm) may you generate HTML.

Do not skip this gate to save time.

---

## Phase 4 — Styling interview (theme)

After TOC approval, ask **styling** questions (chat and/or AskQuestion). Capture concrete choices:

| Area | Ask / options |
|------|----------------|
| **Mode** | Light, dark, or high-contrast |
| **Mood** | e.g. corporate minimal, playful, academic, bold/startup, elegant |
| **Colors** | Primary, accent, background (hex or named); optional link to brand guidelines |
| **Type** | Sans vs serif; system stack vs named **Google Fonts** (one heading + one body max) |
| **Density** | Spacious vs information-dense |
| **Shape** | Sharp vs rounded; shadows none / subtle / strong |
| **Motion** | Restrained (`fade`/`none`) vs standard vs energetic transitions |

Map answers into the deck: pick the **closest built-in Reveal theme** as a base, then override with a `<style>` block using **CSS variables** and `.reveal` / `.reveal .slides section` rules (see [reference.md](reference.md)).

---

## Phase 5 — Build

1. Produce **one `index.html`** with embedded theme CSS (and optional `<link>` to Google Fonts only if the user agreed).  
2. Implement **exactly the approved TOC**; adjust heading text only if needed for clarity—do not add major sections without asking.  
3. Reveal structure, script **order**, plugins, and accessibility rules below still apply.

### Technical defaults

- Wrap slides: `<div class="reveal"><div class="slides">` … `</div></div>`  
- One main idea per `<section>`; nested `<section>` only for vertical stacks.  
- **Scripts:** `reveal.js` → `highlight.min.js` (hljs) → Reveal plugins (`markdown`, `highlight`, `notes` as needed).  
- **Semantic headings**; code in `<pre><code class="language-…">` with Highlight plugin; notes in `<aside class="notes">`.  
- **Images:** prefer none in the first pass unless the user supplied paths or URLs; if they add files later, use relative paths beside the HTML.

### Quality checklist

- [ ] TOC matches what was approved  
- [ ] Theme reflects stated colors, type, density, motion  
- [ ] Deck opens by opening the HTML file in a browser (`file://`); keyboard navigation works  
- [ ] Contrast is readable on laptop and projector  

## When not to use Reveal

If the user forbids external scripts, use the vanilla pattern in [reference.md](reference.md) and still follow the same interview → TOC → approval → styling flow.

## Additional resources

- Reveal options, PDF, math, **theme variable overrides**: [reference.md](reference.md)
