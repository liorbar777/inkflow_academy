<div align="center">
  <img src="images/calligraphy-scroll.png" alt="Inkflow Academy" width="130">

  # 墨流 · Inkflow Academy of Calligraphy
</div>

A single-page marketing site for **Inkflow Academy**, a Chinese calligraphy and brush-arts studio in Chengdu. The entire experience — layout, styling, animation, storefront, ambient audio, and an **AI chat assistant** — lives in one self-contained `index.html` with no build step and no backend.

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

## AI chat assistant — Inkling (墨童)

The site ships with a built-in **conversational assistant** that behaves like a real website concierge — it greets visitors, answers questions, and guides them toward booking or the store.

- **Knowledge-base driven.** Inkling answers from a curated, bilingual knowledge base of **~70 topics** covering the whole academy: courses and pricing, the four class formats — including the **worldwide Online Live Brush Class** for students outside Chengdu — brushes and materials (goat / wolf / rabbit hair), the store products, the ink-garden, our story and teachers, visiting hours and location, contact, booking, and cancellation policy. Every answer is grounded in the site's real content.
- **Natural-language matching.** A lightweight matcher resolves each question to the best topic using word-boundary keyword matching, plural tolerance, and length-weighted scoring, so specific questions (*"tell me about the private critique"*) beat broad ones (*"what courses?"*).
- **Fully bilingual (EN / 中文).** Every reply, label, greeting, and suggestion follows the site's language toggle — even mid-conversation.
- **Noticeable by design.** A gold floating launcher (bottom-right) with a soft attention ping, plus a greeting bubble that slides in shortly after load inviting *"Ask me anything about the academy."*
- **Friendly UX.** Typing indicator, suggested-question chips, `Esc` to close, and click-anywhere-outside to dismiss.

All of it is self-contained vanilla JS — no API keys, no backend, no external calls.

## Project structure

```
inkflow_academy/
├── index.html          # the entire site — markup, styles, and scripts
├── images/             # photography used across the page
├── audio/              # ambient instrumental theme
├── skills-lock.json    # Wix skills pin (tooling metadata; not used at runtime)
├── .agents/            # Wix skill references (tooling metadata; not used at runtime)
└── README.md
```

## Page sections

A single vertical scroll:

Hero → Ink Garden ("The Practice") → Video → Our Story → Gallery → Store → Testimonials → Courses → FAQ → Footer — with the **Inkling assistant** floating above every section.

## Features

- **AI chat assistant (Inkling / 墨童)** — a bilingual, knowledge-base-backed site concierge answering ~70 topics about the academy. See the section above.
- **Bilingual EN / 中文** — the nav toggle swaps copy in place; Chinese text activates `Noto Serif SC` via a `lang-zh` class.
- **Ambient music** — a looped Chinese instrumental theme (`audio/theme.mp3`), gently faded in, toggled from the nav; the button beats like a heart for the first 10 seconds to draw the eye.
- **Shopping cart** — add/remove/adjust store items with a running total and slide-out panel. Checkout composes an order-summary `mailto:`.
- **Course reservation** — four class formats (Group Kai-Shu, Private Critique, Weekend Brand Lettering, and a **worldwide Online Live Brush Class**), reserved via a prefilled `mailto:` from the "Book a Session" CTA.
- **Live ink background** — a canvas flow-field animation plus spawned calligraphy characters.
- **Scroll reveals** — driven by `IntersectionObserver`, including a fanning gallery interaction.
- **Custom brush cursor** — a gold SVG brush replaces the default pointer.

## Theme

The palette is defined as CSS custom properties at the top of the `<style>` block:

```css
--paper:#F0E8D5; --ink:#100E1C; --seal:#D43B20; --gold:#C9A028;
--dark:#0C0A18;  --on-ink:#F0E8D5; --muted:#6A6258; --wash:#D8CFBA;
```

Most of the site is driven by these variables, so adjusting them re-themes the whole page — assistant included.

## Deployment

Static site — host `index.html` and `images/` on any static host (Netlify, GitHub Pages, S3, Wix, etc.). No server runtime required.
