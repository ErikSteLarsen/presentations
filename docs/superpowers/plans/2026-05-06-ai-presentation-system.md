# AI Presentation System Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create a folder-based AI presentation system with a forest theme, shared defaults, and a Claude Code skill for generating Reveal.js decks.

**Architecture:** Three static files power the system — `CONTEXT.md` (defaults), `_template/template.html` (Reveal.js + forest theme), and `_skill/create-presentation.md` (generation instructions). Claude reads these as context, generates `<topic>/slides.md`, then renders it into `<topic>/index.html` by embedding the markdown into the template's placeholder.

**Tech Stack:** Reveal.js 5.x (CDN), Nunito font (Google Fonts CDN), vanilla HTML/CSS, no build step.

---

## Task 1: Create CONTEXT.md

**Files:**
- Create: `CONTEXT.md`

- [ ] **Step 1: Write CONTEXT.md**

```markdown
# Presentation System — Context & Defaults

## Theme
- Background: `#f5f7f0` (soft warm white with green tint)
- Primary text: `#1a2e1a` (deep forest)
- Headings: `#2d6a4f` (dark forest green)
- Accent: `#52b788` (mid forest green)
- Highlight: `#7bc67e` (bright leaf green)
- Surface/card bg: `#e9f5ee` (pale green)
- Font: Nunito (rounded sans-serif)
- Code font: JetBrains Mono
- Generous whitespace, rounded corners (12px) on cards and callouts

## Presentation Defaults
- **Slide count:** 10 (unless the user specifies otherwise)
- **Tone:** Professional but approachable — clear, not stiff
- **Audience:** No default — ask the user if not provided in the prompt
- **Language:** Match the language of the user's prompt (Norwegian or English)
- **Speaker notes:** Always generate, 2–4 sentences per slide

## Available Slide Types
Use these types when deciding how to structure each slide:

| Type | Use for |
|---|---|
| `title` | Opening slide — big heading, subtitle, optional presenter name |
| `section-header` | Marks a new section — large centered text, minimal content |
| `bullets` | Main content — heading + up to 5 bullet points |
| `two-column` | Side-by-side comparison or split content |
| `quote` | Highlighted quote with attribution |
| `image-placeholder` | Use `[IMAGE: description]` when a visual is needed |
| `closing` | Final slide — thank you, questions, contact info |

## Output Format
- **Folder name:** kebab-case from topic, e.g. `zero-trust-intro/`
- **Source file:** `<folder>/slides.md` — editable Reveal.js markdown
- **Rendered file:** `<folder>/index.html` — template with slides embedded
- **Slide separator:** `---` (blank line, three dashes, blank line)
- **Speaker notes:** `Note:` block after slide content

## Slide Markdown Format

```
# Slide Title

- Bullet one
- Bullet two
- Bullet three

Note: Speaker notes go here. Keep them to 2–4 sentences. Focus on what to say, not what's on screen.

---

## Next Slide Title

Content here.

Note: Notes for this slide.
```

## Rendering Instructions
To create `<folder>/index.html` from `<folder>/slides.md`:
1. Read `_template/template.html`
2. Read the generated `slides.md`
3. Replace the exact string `<!-- SLIDES_CONTENT -->` with the full contents of `slides.md`
4. Write the result to `<folder>/index.html`
```

- [ ] **Step 2: Confirm file exists**

Run: `ls -la /home/forsvaret/testprojects/presentations/CONTEXT.md`  
Expected: file listed with non-zero size

---

## Task 2: Create the Reveal.js Forest Theme Template

**Files:**
- Create: `_template/template.html`

- [ ] **Step 1: Create the `_template/` directory**

Run: `mkdir -p /home/forsvaret/testprojects/presentations/_template`

- [ ] **Step 2: Write `_template/template.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Presentation</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reveal.js@5.1.0/dist/reveal.css">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reveal.js@5.1.0/plugin/highlight/monokai.css">
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Nunito:wght@300;400;600;700;800&family=JetBrains+Mono:wght@400;600&display=swap');

    :root {
      --c-bg:        #f5f7f0;
      --c-deep:      #1a2e1a;
      --c-heading:   #2d6a4f;
      --c-accent:    #52b788;
      --c-bright:    #7bc67e;
      --c-surface:   #e9f5ee;
      --c-muted:     #6a8f6a;
      --c-white:     #ffffff;
      --radius:      12px;
      --font-main:   'Nunito', sans-serif;
      --font-mono:   'JetBrains Mono', monospace;
    }

    /* ── Base ── */
    .reveal-viewport { background: var(--c-bg); }

    .reveal {
      font-family: var(--font-main);
      font-size: 36px;
      font-weight: 400;
      color: var(--c-deep);
    }

    .reveal .slides { text-align: left; }

    /* ── Headings ── */
    .reveal h1, .reveal h2, .reveal h3, .reveal h4 {
      font-family: var(--font-main);
      font-weight: 800;
      color: var(--c-heading);
      text-transform: none;
      letter-spacing: -0.02em;
      line-height: 1.15;
      margin-bottom: 0.4em;
    }

    .reveal h1 { font-size: 2em; }
    .reveal h2 { font-size: 1.5em; }
    .reveal h3 { font-size: 1.15em; color: var(--c-accent); }

    /* ── Title slide (first section) ── */
    .reveal .slides > section:first-child {
      text-align: center;
    }
    .reveal .slides > section:first-child h1 {
      font-size: 2.2em;
      color: var(--c-heading);
    }
    .reveal .slides > section:first-child p {
      color: var(--c-muted);
      font-size: 0.75em;
      font-weight: 600;
    }

    /* ── Body text ── */
    .reveal p {
      line-height: 1.6;
      margin: 0 0 0.5em;
    }

    /* ── Lists ── */
    .reveal ul, .reveal ol {
      display: block;
      margin: 0 0 0 1.2em;
    }

    .reveal ul li {
      list-style: none;
      position: relative;
      padding-left: 1.2em;
      margin-bottom: 0.45em;
      line-height: 1.5;
    }

    .reveal ul li::before {
      content: '';
      position: absolute;
      left: 0;
      top: 0.55em;
      width: 0.5em;
      height: 0.5em;
      background: var(--c-bright);
      border-radius: 50%;
    }

    .reveal ol li { margin-bottom: 0.45em; line-height: 1.5; }

    /* ── Code ── */
    .reveal code {
      font-family: var(--font-mono);
      background: var(--c-surface);
      color: var(--c-heading);
      padding: 0.05em 0.3em;
      border-radius: 6px;
      font-size: 0.85em;
    }

    .reveal pre {
      border-radius: var(--radius);
      box-shadow: 0 4px 24px rgba(0,0,0,0.08);
      width: 100%;
    }

    .reveal pre code {
      background: transparent;
      padding: 0;
      border-radius: 0;
      font-size: 0.75em;
      line-height: 1.5;
    }

    /* ── Blockquote ── */
    .reveal blockquote {
      background: var(--c-surface);
      border-left: 5px solid var(--c-bright);
      border-radius: 0 var(--radius) var(--radius) 0;
      padding: 0.8em 1.2em;
      font-style: normal;
      font-weight: 600;
      color: var(--c-heading);
      box-shadow: none;
      width: 100%;
    }

    /* ── Links ── */
    .reveal a {
      color: var(--c-accent);
      text-decoration: none;
      border-bottom: 2px solid var(--c-bright);
    }

    /* ── Two-column layout: use <div class="cols"> ── */
    .reveal .cols {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 2em;
      align-items: start;
    }

    /* ── Image placeholder ── */
    .reveal .img-placeholder {
      background: var(--c-surface);
      border: 2px dashed var(--c-accent);
      border-radius: var(--radius);
      padding: 2em;
      text-align: center;
      color: var(--c-muted);
      font-size: 0.7em;
      font-weight: 600;
    }

    /* ── Section header slide: add class="section-header" to section ── */
    .reveal section.section-header {
      background: linear-gradient(135deg, #2d6a4f 0%, #52b788 100%);
      border-radius: var(--radius);
    }
    .reveal section.section-header h2 {
      color: var(--c-white);
      font-size: 2em;
      text-align: center;
    }

    /* ── Closing slide ── */
    .reveal section.closing {
      text-align: center;
    }
    .reveal section.closing h2 {
      font-size: 2em;
    }

    /* ── Progress bar ── */
    .reveal .progress { color: var(--c-bright); }

    /* ── Slide number ── */
    .reveal .slide-number {
      font-family: var(--font-main);
      font-size: 0.5em;
      color: var(--c-muted);
      background: transparent;
    }

    /* ── Controls ── */
    .reveal .controls { color: var(--c-accent); }
  </style>
</head>
<body>
  <div class="reveal">
    <div class="slides">
      <section data-markdown
               data-separator="^\n---\n$"
               data-separator-vertical="^\n--\n$"
               data-separator-notes="^Note:">
        <script type="text/template">
<!-- SLIDES_CONTENT -->
        </script>
      </section>
    </div>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/reveal.js@5.1.0/dist/reveal.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/reveal.js@5.1.0/plugin/markdown/markdown.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/reveal.js@5.1.0/plugin/notes/notes.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/reveal.js@5.1.0/plugin/highlight/highlight.js"></script>
  <script>
    Reveal.initialize({
      hash: true,
      slideNumber: 'c/t',
      progress: true,
      transition: 'fade',
      backgroundTransition: 'fade',
      center: false,
      margin: 0.08,
      plugins: [RevealMarkdown, RevealNotes, RevealHighlight]
    });
  </script>
</body>
</html>
```

- [ ] **Step 3: Verify placeholder is present**

Run: `grep -c 'SLIDES_CONTENT' /home/forsvaret/testprojects/presentations/_template/template.html`  
Expected output: `1`

---

## Task 3: Create the Presentation Skill

**Files:**
- Create: `_skill/create-presentation.md`

- [ ] **Step 1: Create `_skill/` directory**

Run: `mkdir -p /home/forsvaret/testprojects/presentations/_skill`

- [ ] **Step 2: Write `_skill/create-presentation.md`**

```markdown
# Skill: Create Presentation

Use this skill when the user asks to create, generate, or add slides for a presentation.

## Before you start

1. Read `/home/forsvaret/testprojects/presentations/CONTEXT.md` — all defaults live there.
2. If the user has not specified an **audience**, ask: *"Who is the audience for this presentation?"* before generating anything.

## Inputs to collect from the user prompt

| Input | Required | Default |
|---|---|---|
| Topic / title | Yes | — |
| Audience | Yes | Ask if missing |
| Slide count | No | 10 |
| Tone | No | Professional but approachable |
| Per-slide content direction | No | Claude decides structure |
| Language | No | Match prompt language |

**Per-slide direction examples:**
- Loose: `"3 slides on zero-trust principles"` — Claude decides content
- Specific: `"Slide 4: micro-segmentation — 3 bullets, one analogy"` — fill content to spec
- Mixed: any combination is valid

## Output folder

Name: kebab-case from the topic.  
Examples: `zero-trust-intro/`, `budsjett-2027/`, `team-onboarding-q3/`

Create the folder before writing files.

## Step 1: Generate slides.md

Write `<folder>/slides.md` using Reveal.js markdown format:
- Horizontal slide separator: blank line + `---` + blank line
- Speaker notes: `Note:` block immediately after slide content
- Keep bullets to 5 or fewer per slide
- Use slide types from CONTEXT.md to vary the deck structure
- First slide is always `title` type
- Last slide is always `closing` type
- Every slide gets speaker notes (2–4 sentences)

**slides.md example structure:**
```
# Presentation Title

Subtitle or brief framing line

Note: Welcome the audience. Introduce yourself and the topic in one sentence.

---

## Agenda

- Topic one
- Topic two
- Topic three

Note: Walk through what you'll cover today. Keep it brief — this is a map, not a journey.

---

<!-- more slides -->

---

## Thank You

Questions? Contact: [name]

Note: Open the floor for questions. Remind the audience of your contact info.
```

## Step 2: Render index.html

1. Read `_template/template.html`
2. Replace the exact string `<!-- SLIDES_CONTENT -->` with the full contents of `slides.md`
3. Write the result to `<folder>/index.html`

Do not modify anything else in the template.

## Step 3: Confirm to the user

Tell the user:
- Where the files were created (`<folder>/slides.md` and `<folder>/index.html`)
- How to open: `open <folder>/index.html` (macOS) or right-click → open in browser
- That they can edit `slides.md` and ask you to re-render at any time

## Adding or editing individual slides

If the user says "add a slide about X" or "update slide 3":
1. Read the existing `slides.md`
2. Make the targeted change
3. Re-render `index.html` using the same template injection process
4. Confirm what changed

## Re-rendering only

If the user edits `slides.md` manually and asks to re-render:
1. Read `_template/template.html`
2. Read the updated `slides.md`
3. Replace `<!-- SLIDES_CONTENT -->` and write `index.html`
```

- [ ] **Step 3: Verify skill file exists**

Run: `ls -la /home/forsvaret/testprojects/presentations/_skill/create-presentation.md`  
Expected: file listed with non-zero size

---

## Task 4: Validate with a Test Presentation

**Files:**
- Create: `test-deck/slides.md`
- Create: `test-deck/index.html`

- [ ] **Step 1: Generate a test slides.md**

Create `test-deck/slides.md` with the following content to verify the full theme renders correctly:

```markdown
# AI Presentation System

Your forest-themed slide generator — ready to use.

Note: This is the title slide. Welcome the audience and introduce the system.

---

## What This Is

- Generate presentations by describing what you want
- Custom forest theme — clean, rounded, bright
- Reveal.js — open in any browser, no installation needed
- Editable markdown source per presentation

Note: Walk through the four core value props. Emphasize that there's zero setup per presentation.

---

## How to Use It

1. Start Claude Code in this folder
2. Include `_skill/create-presentation.md` as context
3. Describe your deck — topic, audience, slides
4. Open the generated `index.html` in your browser

Note: Demonstrate the workflow. The user describes the deck, Claude generates slides.md and index.html.

---

## Slide Types Available

- **Title** — opening slide
- **Bullets** — up to 5 points per slide
- **Two-column** — side-by-side content
- **Quote** — highlighted blockquote
- **Image placeholder** — for visuals
- **Closing** — thank you / Q&A

Note: You can mix and match these types. When giving Claude per-slide direction, just describe what you want — it picks the right type.

---

> "A good presentation is a story, not a list."

— Every speaker coach, ever

Note: Use quote slides sparingly — one or two per deck for impact.

---

## Code Looks Like This

```bash
# Generate a new deck
claude --context _skill/create-presentation.md
# Then prompt: "Create 8 slides on X for Y audience"
```

Note: Show the exact command the user will run. Keep code examples minimal and clear.

---

## You're Ready

Questions? Edit `CONTEXT.md` to change defaults anytime.

Note: Close with a clear next step. Remind the audience that all defaults live in CONTEXT.md and can be adjusted at any time.
```

- [ ] **Step 2: Render test-deck/index.html**

Read `_template/template.html`, replace `<!-- SLIDES_CONTENT -->` with the content of `test-deck/slides.md`, write to `test-deck/index.html`.

- [ ] **Step 3: Verify structure**

Run: `grep -c 'SLIDES_CONTENT' /home/forsvaret/testprojects/presentations/test-deck/index.html`  
Expected output: `0` (placeholder was replaced)

Run: `grep -c 'AI Presentation System' /home/forsvaret/testprojects/presentations/test-deck/index.html`  
Expected output: `1` (slide content is present)

- [ ] **Step 4: Verify final file tree**

Run: `find /home/forsvaret/testprojects/presentations -not -path '*/docs/*' | sort`

Expected output includes:
```
.../CONTEXT.md
..._skill/create-presentation.md
..._template/template.html
...test-deck/index.html
...test-deck/slides.md
```

- [ ] **Step 5: Open in browser to verify theme**

Run: `xdg-open /home/forsvaret/testprojects/presentations/test-deck/index.html 2>/dev/null || echo "Open manually: test-deck/index.html"`

Visually verify:
- Forest green headings on light background
- Rounded Nunito font
- Green bullet dots
- Clean whitespace
- Slide counter visible bottom-right

---

## Done

The system is live. To use it:

```bash
cd ~/testprojects/presentations/
claude
# Include _skill/create-presentation.md as context, then:
# "Create a 10-slide presentation on X for Y audience"
```
