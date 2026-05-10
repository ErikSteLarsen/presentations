# Presentation System

A Reveal.js presentation workspace powered by Claude Code. Describe the deck you want, and Claude generates browser-ready slides with a forest-green theme.

## Quick Start

1. Open Claude Code in this folder
2. Tell Claude what presentation you want:
   ```
   Create a presentation about zero trust security for IT managers, 8 slides
   ```
3. Open the generated `<folder>/index.html` in your browser:
   ```
   xdg-open zero-trust-security/index.html
   ```

That's it. Claude creates a `slides.md` (editable source) and `index.html` (rendered deck) in a new folder.

## What You Can Specify

| Input | Required | Default |
|---|---|---|
| Topic / title | Yes | -- |
| Audience | Yes | Claude will ask |
| Slide count | No | 10 |
| Tone | No | Professional but approachable |
| Per-slide direction | No | Claude decides structure |
| Language | No | Matches your prompt |

Per-slide direction can be loose ("3 slides on X"), specific ("Slide 4: micro-segmentation -- 3 bullets, one analogy"), or mixed.

## Slide Types

- **Title** -- opening slide with heading and subtitle
- **Section header** -- marks a new section, large centered text
- **Bullets** -- heading + up to 5 bullet points
- **Two-column** -- side-by-side comparison or split content
- **Quote** -- highlighted blockquote with attribution
- **Image placeholder** -- `[IMAGE: description]` where a visual is needed
- **Closing** -- thank you, questions, contact info

## Editing Slides

Ask Claude to make changes:

```
Add a slide about budget impact after slide 3
```

```
Change the closing slide to include my email
```

Or edit `slides.md` directly and ask Claude to re-render:

```
Re-render zero-trust-security
```

## Project Structure

```
presentations/
  _template/
    template.html    # Reveal.js template with theme styles
  test-deck/         # Example presentation
    slides.md        # Slide content (markdown)
    index.html       # Rendered presentation (open in browser)
  CLAUDE.md          # Instructions for Claude Code
```

## Theme

The built-in theme uses a forest-green palette with Nunito font and JetBrains Mono for code. All styling lives in `_template/template.html`.

| Element | Color |
|---|---|
| Background | `#f5f7f0` soft warm white |
| Headings | `#2d6a4f` dark forest green |
| Accent | `#52b788` mid forest green |
| Highlight | `#7bc67e` bright leaf green |

## Presenting

Reveal.js keyboard shortcuts work out of the box:

- **Arrow keys** -- navigate slides
- **S** -- open speaker notes
- **F** -- fullscreen
- **O** -- slide overview
- **Esc** -- exit overview/fullscreen

No installation or build step required. The HTML files load Reveal.js from a CDN.
