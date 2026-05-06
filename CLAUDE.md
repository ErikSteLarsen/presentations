# Presentation System

This folder is a Reveal.js presentation workspace. When the user asks to create a presentation, generate slides, or add/edit slides, follow the instructions below.

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

## Defaults

- **Slide count:** 10 unless specified
- **Tone:** Professional but approachable — clear, not stiff
- **Audience:** No default — ask if not provided
- **Language:** Match the language of the user's prompt (Norwegian or English)
- **Speaker notes:** Always generate, 2–4 sentences per slide

## Slide Types

| Type | Use for |
|---|---|
| `title` | Opening slide — big heading, subtitle, optional presenter name |
| `section-header` | Marks a new section — large centered text, minimal content |
| `bullets` | Main content — heading + up to 5 bullet points |
| `two-column` | Side-by-side comparison or split content |
| `quote` | Highlighted quote with attribution |
| `image-placeholder` | Use `[IMAGE: description]` when a visual is needed |
| `closing` | Final slide — thank you, questions, contact info |

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
- Max 5 bullets per slide
- First slide: `title` type. Last slide: `closing` type.

Example:
```
# Presentation Title

Subtitle line

Note: Welcome the audience. Introduce yourself and the topic in one sentence.

---

## Agenda

- Topic one
- Topic two
- Topic three

Note: Walk through what you'll cover. Keep it brief.

---

## Thank You

Questions? Contact: [name]

Note: Open the floor for questions.
```

**4. Render `<folder>/index.html`**

1. Read `_template/template.html`
2. Replace the exact string `<!-- SLIDES_CONTENT -->` with the full contents of `slides.md`
3. Write result to `<folder>/index.html`

Do not modify anything else in the template.

**5. Confirm to the user**

- Files created: `<folder>/slides.md` and `<folder>/index.html`
- How to open: `xdg-open <folder>/index.html` or right-click → open in browser
- They can edit `slides.md` and ask you to re-render at any time

## Editing slides

To add or change a slide: read `slides.md`, make the targeted edit, re-render `index.html` using the same injection process.

To re-render only: read template, replace placeholder with updated `slides.md`, write `index.html`.
