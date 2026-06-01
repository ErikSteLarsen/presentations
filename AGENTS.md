# Presentation System

This folder is a Reveal.js presentation workspace. When the user asks to create a presentation, generate slides, or add/edit slides, follow the instructions below.

> **Note:** `CLAUDE.md` and `AGENTS.md` are kept byte-identical. When you change one, make the same change to the other.

## Theme

| Element | Value |
|---|---|
| Background | `#f5f7f0` (soft warm white with green tint) |
| Primary text | `#1a2e1a` (deep forest) |
| Headings | `#2d6a4f` (dark forest green) |
| Accent | `#52b788` (mid forest green) |
| Highlight | `#7bc67e` (bright leaf green) |
| Surface/card bg | `#e9f5ee` (pale green) |
| Font | Nunito (rounded sans-serif) |
| Code font | JetBrains Mono |

All colors are available as CSS variables in the template: `--c-bg`, `--c-deep`, `--c-heading`, `--c-accent`, `--c-bright`, `--c-surface`, `--c-muted`, `--c-white`. Reuse them in any custom markup instead of hardcoding hex values.

## Themes

A theme is a template file in `_template/`. All themes share the **same component classes**, so any `slides.md` renders under any theme without changes — only the look differs. To switch a deck's theme, just re-render its `index.html` from a different template.

| Theme | File | Look |
|---|---|---|
| Forest (default) | `_template/template.html` | Soft warm-white base, forest-green accents, Nunito |
| Bouvet | `_template/template-bouvet.html` | Palette sampled from Bouvet's "Designtilnærming" artwork — warm orange `#f0a86c` (primary accent, legible `#c96f2e`), pale blue-grey `#c0ccd8`, bright mint `#78fc9c`, cream `#f0e4cc` on warm paper `#fbf9f5`, with near-black navy `#14143a` ink. Circle/"rounding" motifs (Heydays/Red Dot nod) sit in corners, always behind text. Space Grotesk + Inter. Airier than Forest: smaller base text (30px) and larger slide margin (0.12). |

When the user asks for a Bouvet-styled deck (or says they work at Bouvet), render from `template-bouvet.html`. The color values in the table at the top describe the Forest theme; each template defines its own palette via the same `--c-*` variables.

**Decorative shapes must never cover text.** Any decorative circle/figure is a `::before`/`::after` pseudo-element with `z-index: 0`, anchored into a corner (often partly off-slide); real content is lifted above with `z-index: 2`. Keep this rule when adding motifs to any theme.

**Whitespace & density.** Decks should breathe. Favor a smaller base font with generous slide margin over cramming text. Keep ≤ 5 bullets per slide, prefer one primary component per slide, and lean on speaker notes for detail rather than packing the slide. The Bouvet theme encodes this (30px base, 0.12 margin, roomier component spacing); apply the same restraint when authoring content for any theme.

To make a new reusable theme: copy a template, change only the `:root` variables and component styling, keep every component class name and the `<!-- SLIDES_CONTENT -->` placeholder intact, and add a row to this table.

## Defaults

- **Slide count:** 10 unless specified
- **Tone:** Professional but approachable — clear, not stiff
- **Audience:** No default — ask if not provided
- **Language:** Match the language of the user's prompt (Norwegian or English)
- **Speaker notes:** Always generate, 2–4 sentences per slide

## Slide Types

| Type | Use for |
|---|---|
| `title` | Opening slide — big heading, subtitle, optional presenter name (first slide, auto-centered) |
| `section-header` | Marks a new section — large centered white text on a green gradient |
| `bullets` | Main content — heading + up to 5 bullet points |
| `quote` | Highlighted quote with attribution (markdown `>` blockquote) |
| `closing` | Final slide — thank you, questions, contact info |

## Layout components

These are reusable, themed building blocks defined in `_template/template.html`. Use raw HTML inside `slides.md` to invoke them. **Prefer a structured component over a plain bullet list whenever the content has structure** (a process, a comparison, a set of stats, a progression).

### Kicker (eyebrow label)

Put a small section label above almost every content heading for consistent slide chrome:

```
<span class="kicker">Del 1 · Verifisering</span>

## Slide heading
```

### Stat callouts

For big numbers (percentages, counts, multipliers). Use 2–3 per row.

```
<div class="stats">
<div class="stat"><span class="num">82 %</span><span class="label">use AI assistants</span></div>
<div class="stat"><span class="num">76 %</span><span class="label">don't trust output</span></div>
</div>
```

### Card grid

Titled cards. Plain `cards` auto-fits; `cards two` forces two columns (use for 2 or 4 cards → 2×2).

```
<div class="cards two">
<div class="card">

#### Card title

Body text or markdown bullets.

</div>
<div class="card">

#### Card title

More content.

</div>
</div>
```

### Pyramid

Layered diagram, narrow on top → wide at the bottom. Tiers `t1`–`t5` (t1 = top/narrowest).

```
<div class="pyramid">
<div class="tier t1">Top layer</div>
<div class="tier t2">…</div>
<div class="tier t3">…</div>
<div class="tier t4">…</div>
<div class="tier t5">Bottom layer (widest)</div>
</div>
```

### Process flow (horizontal steps with arrows)

For pipelines, sequences, before/during/after steps.

```
<div class="flow">
<div class="step">Step one<br><strong>2 s</strong></div>
<div class="step">Step two</div>
<div class="step">Step three</div>
</div>
```

### Contrast (from → to)

Two panels with an arrow between. `.from` is reddish (the bad/old state), `.to` is green (the good/new state). Panels accept paragraphs or markdown bullet lists.

```
<div class="contrast">
<div class="panel from">

#### Before

Bad state description.

</div>
<div class="arrow">→</div>
<div class="panel to">

#### After

Good state description.

</div>
</div>
```

### Loop (2×2 cycle)

Numbered nodes for a repeating cycle. Order nodes so they read clockwise: top-left, top-right, then bottom-RIGHT, bottom-LEFT (i.e. HTML order 1, 2, 4, 3).

```
<div class="loop">
<div class="node"><span class="n">1</span><p>First</p></div>
<div class="node"><span class="n">2</span><p>Second</p></div>
<div class="node"><span class="n">4</span><p>Fourth</p></div>
<div class="node"><span class="n">3</span><p>Third</p></div>
</div>
```

### Timeline / maturity stages

Horizontal stages connected by a line — for roadmaps and progressions.

```
<div class="timeline">
<div class="stage"><span class="dot"></span><h4>Day 1</h4><p>First milestone</p></div>
<div class="stage"><span class="dot"></span><h4>Week 1</h4><p>Next milestone</p></div>
<div class="stage"><span class="dot"></span><h4>Month 1</h4><p>Later milestone</p></div>
</div>
```

### Mini pyramid (focused layer)

A small, horizontally-centered pyramid for per-layer slides: add `bv-mini` to `.pyramid`, keep the focused tier as-is and add `dim` to the others to grey them out, so the active layer stands out in its real pyramid colour.

```
<div class="pyramid bv-mini">
<div class="tier t1">E2E-tester</div>
<div class="tier t2 dim">Integrasjonstester</div>
<div class="tier t3 dim">Enhetstester</div>
<div class="tier t4 dim">Statisk analyse</div>
<div class="tier t5 dim">Kode- & plangjennomgang</div>
</div>
```

### Tables

Plain GitHub-flavored markdown tables are styled automatically (green header, zebra rows). Good for symptom → solution, comparison matrices, "each layer catches X".

### Two-column (generic split)

`<div class="cols">` — a simple 1:1 grid for side-by-side markdown content when no richer component fits.

### Lead line

`<p class="lead">One emphasized sentence.</p>` — a large lead-in under a heading.

### Image placeholder

`<div class="img-placeholder">[IMAGE: description]</div>` when a real visual is needed later.

### Bouvet figures (Bouvet theme only)

The Bouvet template ships a sprite of reusable Bauhaus characters (separated from Bouvet's "Designtilnærming" artwork), defined once as SVG `<symbol>`s in `<body>`. Use them to make slides feel alive — sparingly, where there's whitespace.

Figures are geometric (quarter-circles, rectangles, squares, triangles, flat circles). Heads have **two dot-eyes only — no mouths** (matches the source artwork).

People:
| Figure id | Motif | Fits slides about |
|---|---|---|
| `#bv-person` | head on quarter-circle body | generic human touch |
| `#bv-explorer` | head + magnifying glass | research, verification, investigation |
| `#bv-board` | board with shapes + head | planning, defining, structure |
| `#bv-ideate` | speech bubbles + head | ideas, brainstorming, communication |
| `#bv-test` | reviewer + head + triangle | testing, review, feedback |

Objects (pure geometry):
| Figure id | Motif | Fits slides about |
|---|---|---|
| `#bv-computer` | monitor with UI | building, prototypes, frontend |
| `#bv-bulb` | circle + base | ideas, insight |
| `#bv-building` | stacked rectangles | scale, organisation, the city |
| `#bv-book` | cover + pages | docs, domain memory, learning |
| `#bv-cloud` | overlapping circles | cloud, infrastructure |
| `#bv-shapes` | circle/square/triangle cluster | abstract, compounding, systems |
| `#bv-quarter` | single quarter-circle | pure decoration / accent |

Nature (great for title / section / closing scenes):
| Figure id | Motif | Fits slides about |
|---|---|---|
| `#bv-tree` | quarter-circle canopy + trunk | growth, sustainability, nature |
| `#bv-leaf` | two quarter-circles + stem | growth, calm, sustainability |
| `#bv-hills` | layered hills + sun | landscape, journey, the big picture |
| `#bv-river` | wavy water bands + sun | flow, pipelines, continuity |
| `#bv-flower` | petal circles + center | optimism, blossoming, results |
| `#bv-mountain` | triangles + sun | goals, challenge, the road ahead |
| `#bv-sun` | circle + accent shapes | optimism, energy, a fresh start |
| `#bv-plant` | leaves + pot | growth, compounding, care |

**Decorative corner** (sits behind text, tucked in a corner — preferred default):

```
<div class="bv-corner bv-br"><svg class="bv-fig"><use href="#bv-explorer"/></svg></div>
```

Corner classes: `bv-br` (bottom-right), `bv-bl`, `bv-tr`, `bv-tl`. Place the `<div>` as a direct child of the slide (anywhere in its markdown, e.g. just before `Note:`).

**Scene** (a larger cluster of 2–3 figures for slides with lots of room — title, `section-header`, `closing`). Sits behind the text:

```
<div class="bv-scene bv-center"><svg class="bv-fig" style="width:170px"><use href="#bv-mountain"/></svg><svg class="bv-fig" style="width:120px"><use href="#bv-hills"/></svg></div>
```

Position class: `bv-center` (bottom third, horizontally centered — **use this for low-content title/section/closing slides** so the illustration stays clear of the heading), or `bv-right` / `bv-left` to anchor a scene to a side edge on a content slide. Size each figure inline with `style="width:…"`. Title/section/closing slides have **no built-in decoration** — add a scene to give them an illustration.

**Inline** (part of the content flow, sized as you like):

```
<svg class="bv-fig" style="width:170px"><use href="#bv-tree"/></svg>
```

Sizes: add `bv-sm` (small) or `bv-lg` (large) to a `bv-corner`. Corner and scene figures are anchored into the empty margin band (negative offsets) at `z-index:0`, so they sit **clear of and behind** the text — no overlap.

Guidance: at most one corner figure (or one scene) per slide; only where there's clear empty space (avoid slides already full of cards/tables); pick a side away from where the text sits. Use **scenes on the title/section/closing slides** — they have the most room and benefit most from a richer illustration tied to the slide's theme. To add a new figure, add another `<symbol>` to the sprite using the palette hexes and give it a `bv-` id. A live gallery of all figures renders at `figurer.html` (re-generate it when you add figures).

### Progress bar (Bouvet theme)

The Bouvet theme replaces Reveal's built-in progress/slide-number chrome with a custom thin line at the very bottom (`.bv-progress`) that fills left→right and reaches full width on the last slide. It is wired in the template's init script (Reveal's own `progress` and `slideNumber` are turned off). Nothing to do per deck — it works automatically. To recolor it, change `.bv-progress-fill` background (defaults to `--c-skyink`). The navigation arrows (`.reveal .controls`) are scaled to half size.

### Section-header slide (Bouvet theme)

In the Bouvet theme a `section-header` slide is **not** a full-bleed navy block. It's a soft on-theme gradient backdrop (cool blue-grey → cream) with a **smaller centered navy card** holding the heading, and room beneath it for a `bv-scene bv-center` figure. The card centering uses `display: flex !important` to beat Reveal's inline `display:block` on the active section — keep the `!important` if you edit it.

## Content placement & structure guidance

- **One idea per slide.** A heading, an optional kicker, one primary visual element (component), and ≤ 5 supporting bullets. Don't stack two heavy components on one slide.
- **Lead with structure, not prose.** If the content is a sequence → use `flow`. A comparison → `contrast` or `cards two`. Numbers → `stats`. A progression → `timeline`. A hierarchy → `pyramid`. Only fall back to a bullet list when nothing more specific fits.
- **Kicker on every content slide.** It orients the audience (which part/section they're in) and gives the deck a consistent rhythm.
- **Section dividers.** Use a `section-header` slide between major parts of the deck.
- **Keep components shallow.** Short labels in `flow`/`pyramid`/`timeline`; put the detail in speaker notes, not on the slide.
- **Max 5 bullets** per slide. If you need more, split the slide or switch to cards/a table.

### Markdown-inside-HTML gotcha

Reveal's markdown plugin only renders markdown inside a raw HTML block if there are **blank lines** separating the markdown from the surrounding tags. Always write:

```
<div class="card">

#### Heading

- bullet

</div>
```

Not `<div class="card">#### Heading</div>` on one line. Components that hold only plain text/`<span>`/`<strong>` (stats, flow, pyramid, loop, timeline) don't need the blank lines.

## How to create a presentation

**1. Collect inputs**

| Input | Required | Default |
|---|---|---|
| Topic / title | Yes | — |
| Audience | Yes | Ask if missing |
| Slide count | No | 10 |
| Tone | No | Professional but approachable |
| Per-slide content direction | No | You decide structure |
| Language | No | Match prompt language |

Per-slide direction can be loose ("3 slides on X"), specific ("Slide 4: micro-segmentation — 3 bullets, one analogy"), or mixed.

**2. Create output folder**

Name: kebab-case from topic. Examples: `zero-trust-intro/`, `budsjett-2027/`, `team-onboarding-q3/`

**3. Write `<folder>/slides.md`**

Use Reveal.js markdown format:
- Slide separator: blank line + `---` + blank line
- Speaker notes: `Note:` block after each slide's content
- First slide: `title` type. Last slide: `closing` type.
- Add a `kicker` and choose the most fitting layout component for each slide (see above).
- Set per-slide classes with an HTML comment: `<!-- .slide: class="section-header" -->` or `class="closing"`.

**4. Render `<folder>/index.html`**

Replace the exact string `<!-- SLIDES_CONTENT -->` in `_template/template.html` with the full contents of `slides.md`, and write the result to `<folder>/index.html`. Do not modify anything else in the template.

A reliable way to do the injection (handles special characters and Unicode cleanly):

```
python3 -c "
tpl = open('_template/template.html', encoding='utf-8').read()
slides = open('<folder>/slides.md', encoding='utf-8').read()
open('<folder>/index.html','w', encoding='utf-8').write(tpl.replace('<!-- SLIDES_CONTENT -->', slides))
"
```

After rendering, verify: the output should no longer contain `<!-- SLIDES_CONTENT -->`, and its size should be roughly template + slides.

**5. Confirm to the user**

- Files created: `<folder>/slides.md` and `<folder>/index.html`
- How to open: `xdg-open <folder>/index.html` or right-click → open in browser
- They can edit `slides.md` and ask you to re-render at any time

## Editing slides

To add or change a slide: read `slides.md`, make the targeted edit, re-render `index.html` using the same injection process.

To re-render only: read template, replace placeholder with updated `slides.md`, write `index.html`.
