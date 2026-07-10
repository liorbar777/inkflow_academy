# 墨流 · Inkflow Academy of Calligraphy

A single-page marketing site for **Inkflow Academy**, a Chinese calligraphy and brush-arts studio in Chengdu. The entire experience — layout, styling, animation, storefront, and audio — lives in one self-contained `index.html` with no build step and no backend.

## Quick start

No dependencies to install. Open the file directly:

```bash
open index.html          # macOS
```

Custom fonts and audio behave best over HTTP rather than `file://`. To serve locally:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Tech stack

- **Plain HTML + CSS + vanilla JavaScript** — everything inline in `index.html` (one `<style>` block, one `<script>` block).
- **Google Fonts** — the only external dependency (Ma Shan Zheng, Cormorant Garamond, Hanken Grotesk, Noto Serif SC).
- **HTML5 Audio** — an ambient Chinese instrumental theme (`audio/theme.mp3`) loops in the background, faded in/out and toggled from the nav.
- **HTML Canvas + IntersectionObserver** — for the ink-flow background and scroll-triggered reveals.

No framework, no bundler, no package manager.

## Project structure

```
inkflow_academy/
├── index.html          # the entire site — markup, styles, and scripts
├── images/             # photography used across the page
├── skills-lock.json    # Wix skills pin (tooling metadata; not used at runtime)
├── .agents/            # Wix skill references (tooling metadata; not used at runtime)
└── README.md
```

## Page sections

A single vertical scroll:

Hero → Ink Garden ("The Practice") → Video → Our Story → Gallery → Store → Testimonials → Courses → FAQ → Footer.

## Features

- **Bilingual EN / 中文** — the nav toggle swaps copy in place; Chinese text activates `Noto Serif SC` via a `lang-zh` class.
- **Ambient music** — a looped Chinese instrumental theme (`audio/theme.mp3`), gently faded in, toggled from the nav.
- **Shopping cart** — add/remove/adjust store items with a running total and slide-out panel. Checkout composes an order-summary `mailto:`.
- **Course reservation** — the "Book a Session" CTA opens a prefilled `mailto:`.
- **Live ink background** — a canvas flow-field animation plus spawned calligraphy characters.
- **Scroll reveals** — driven by `IntersectionObserver`, including a fanning gallery interaction.
- **Custom brush cursor** — a gold SVG brush replaces the default pointer.

## Theme

The palette is defined as CSS custom properties at the top of the `<style>` block:

```css
--paper:#F0E8D5; --ink:#100E1C; --seal:#D43B20; --gold:#C9A028;
--dark:#0C0A18;  --on-ink:#F0E8D5; --muted:#6A6258; --wash:#D8CFBA;
```

Most of the site is driven by these variables, so adjusting them re-themes the whole page.

## Deployment

Static site — host `index.html` and `images/` on any static host (Netlify, GitHub Pages, S3, Wix, etc.). No server runtime required.
