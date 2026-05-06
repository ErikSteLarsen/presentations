# AI Presentation System — Design Spec

**Date:** 2026-05-06  
**Status:** Approved

---

## Overview

A folder-based presentation system for `/home/forsvaret/testprojects/presentations/`. The user describes a deck to Claude Code (with per-slide content direction), and Claude generates a self-contained Reveal.js HTML presentation using shared defaults and a custom theme. No web UI, no build step — open the output HTML in a browser and present.

---

## Folder Structure

```
presentations/
├── CONTEXT.md                  ← shared defaults, theme description, prompting rules
├── _template/
│   └── template.html           ← Reveal.js + forest theme CSS (fully embedded, no CDN deps)
├── _skill/
│   └── create-presentation.md  ← Claude Code skill: instructions for generating decks
└── <topic-name>/               ← one folder per generated presentation
    ├── slides.md               ← editable Reveal.js markdown source
    └── index.html              ← rendered output (template + slides merged)
```

---

## CONTEXT.md Defaults

Loaded by the skill at the start of every presentation session. Contains:

- **Theme**: forest palette (greens, bright accent), Nunito rounded font, clean whitespace, light background
- **Tone**: professional but approachable (adjustable per presentation)
- **Audience**: no default — must be specified per presentation prompt; if omitted, skill asks
- **Default slide count**: 10 (overridable)
- **Available slide types**: title, section-header, bullets (up to 5 items), two-column, quote, image-placeholder, closing
- **Speaker notes**: always generated per slide, kept concise (2–4 sentences)
- **Output format**: `slides.md` using Reveal.js horizontal separator (`---`) and vertical separator (`--`)
- **Folder naming**: kebab-case from the topic, e.g. `zero-trust-intro/`

---

## Skill: create-presentation

Located at `_skill/create-presentation.md`. Invoked by including it as context when starting Claude Code in this directory (or via a future Claude Code skill registration).

**Skill responsibilities:**
1. Read `CONTEXT.md` for all defaults
2. Parse the user's prompt for: topic, audience, slide count, per-slide content direction
3. Ask for audience if not provided
4. Generate `<topic>/slides.md` — one slide per `---` block, with speaker notes in `Note:` blocks
5. Inject slides into `_template/template.html` → write `<topic>/index.html`
6. Confirm output path so the user can open it immediately

**Per-slide input flexibility:**
- Loose: `"3 slides on zero-trust principles"` → Claude decides structure and content
- Specific: `"Slide 4: micro-segmentation — explain the concept, 3 bullets, one analogy"` → Claude fills content to spec
- Mixed: any combination across a single deck

---

## Theme: Forest / Bright / Rounded

Embedded directly in `_template/template.html` — no external CDN, fully offline-capable.

| Element | Value |
|---|---|
| Background | `#f5f7f0` (soft warm white with green tint) |
| Primary text | `#1a2e1a` (deep forest) |
| Accent / headings | `#3d8b5f` (mid forest green) |
| Highlight / CTA | `#7bc67e` (bright leaf green) |
| Font | Nunito (Google Fonts, embedded via `@import`) |
| Code font | JetBrains Mono |
| Slide padding | generous — 48px sides minimum |
| Border-radius | 12px on cards/boxes |
| Bullet style | custom green dot, no default disc |

---

## Workflow

```
1.  cd ~/testprojects/presentations/
2.  claude (include _skill/create-presentation.md as context, or register as skill)
3.  Prompt: "Create a presentation: 8 slides — intro, zero-trust concepts x3,
             roadmap x2, Q&A, thank you. Audience: IT leadership."
4.  Claude: reads CONTEXT.md + skill rules
            → generates zero-trust-intro/slides.md
            → renders zero-trust-intro/index.html
5.  Open zero-trust-intro/index.html in browser → present
```

To edit after generation: modify `slides.md` and ask Claude to re-render, or edit `index.html` directly.

---

## Out of Scope

- No web UI for generation (Claude Code is the interface)
- No per-presentation npm setup
- No PDF export (can be added later via Reveal.js print-pdf mode)
- No image generation (image-placeholder slide type used instead)
